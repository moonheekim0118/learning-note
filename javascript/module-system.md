### CommonJs 란

https://yceffort.kr/2023/05/what-is-commonjs#%EC%84%9C%EB%A1%A0
https://yceffort.kr/2020/08/commonjs-esmodules

### CommonJs 란

- nodejs 에서 자바스크립트 패키지를 불러올 때 사용하는 근본있는 방식
- 현재는 esmodule을 지원하지만, 태초에는 commonjs 방식만 있었음

### 모듈이란

- nodejs 에서 모듈은 각각의 분리된 파일을 모듈이라고 칭한다.

```javascript
const { PI } = Math;
exports.sum = (a, b) => a + b;
exports.circumference = (r) => 2 * PI * r;
```

- nodejs 는 `exports` 라는 특별한 객체를 통해 함수나 변수를 모듈의 루트에 추가할 수 있다.
- But, 상단의 Math 객체에서 구조분해 할 당 한 PI 는 로컬변수로서 아래의 두 함수와 다르게 비공개가 된다. (즉 다른 모듈에서 참조 불가능함)
  - moduleWrapper 로 감싸져있어서.

#### module.exports

- 함수나 객체와 같은 새로운 값을 선언 할 수 있다.

```js
module.exports = class Square {
  constructor(width) {
    this.width = width;
  }
  area() {
    return this.width ** 2;
  }
};
```

- module exports와 exports는 다르다.
- exports는 module.exports 를 가리키고 있다.
- 즉, exports는 module.exports의 숏컷이라고 볼 수 있다.
- module.exports는 모듈이 평가 되기 전에 미리 할당 되는 값이다. 따라서 module.exports를 사용해야한다.

### node.js는 언제 commonjs를 사용할까?

- 파일 확장자가 cjs 인 경우
- 파일 확장자가 js 이며
  - 가장 가까운 부모의 package.json 파일의 type 필드 값이 commonjs 이거나 명시되어 있지 않을 때
- 기본값은 commonjs 다.
  - commonjs 와 esmodule 간에 호환 불가
  - 이미 많은 패키지가 commonjs 로 되어있음

### Module Wrapper

```js
;(function (exports, require, module, __filename, __dirname) { // 내부 모듈 코드는 실제로 여기에 들어감 })

```

- 모듈 래퍼 함수는 위와 같이 생김
- 모듈 최상단에 있는 var const let 등으로 선언 된 변수가 글로벌 객체 (gloabl) 에 등록 되는 것을 막는다.
- 모듈에서 글로벌 객체에 있는 `exports, require, module, __finename, __dirname` 을 사용 할 수 있다.
  - esmodule 에서 `exports, require, module, __finename, __dirname` 을 사용하지 못하는 이유는 모듈 래퍼가 없기 때문이다!

### 순환참조

- a.js 가 b.js 를 불러오고 b.js 가 a.js 를 불러올 때
- 하지만 실제 실행결과에서는 무한루프에 빠지지 않음. 캐싱 덕분에. 이미 캐싱되어있으면 다시 모듈을 불러오지 않고 모듈 불러오기를 종료함

### 동기적으로 실행됨

- commonjs 는 모듈을 동기적으로 불러온다.
  - 즉 모듈을 하나씩 순서대로 불러오고 처리한다.
- require 를 선언하면 디스크 또는 네트워크로 해당 모듈을 읽어서 스크립트를 실행한다.
- 따라서 require를 실행하면 그 자체만으로 I/O 나 부수효과를 발생시키고 이후의 module.exports를 실행함

### 트리쉐이킹이 되지 않는다

- commonjs 는 Nodejs 환경에서만 사용될 목적으로 만들어짐. 그 당시만 해도 브라우저에서는 복잡한 모듈 시스템을 만들 필요가 없었고, (복잡한 자스 필요 X) 서버에서만 필요
- 근데 서버는 브라우저처럼 사용자가 다운로드하거나 그럴 필요가 있는것이 아니어서 모듈크기가 커지는게 상관없음

- commonjs 는 파일단위 모듈을 모듈 래퍼라는 함수로 감싸서 실행함.
- 모듈 래퍼로 인해 생성된 개별 함수 클로저에 의해 래핑되서 실행된다는 점은, 브라우저에서 자바스크립트 성능을 안좋게 만들었다.
  - 서버는 어느정도 컴퓨팅 속도/성능이 보장되어 있으나, 브라우저의 경우 이러한 사용자의 성능을 담보할 수 없다.
- 각종 모듈이 얽혀서 불러오는 과정에서 매번 클로저가 생성되서 참조되는 것은 성능상 문제를 야기함
- 따라서 그 당시 라이브러리 (Closure Complier 나 rollupjs )는 모든 모듈을 하나의 클로저로 호이스팅하거나 연결해서 require 로 인한 성능저하현상을 방지함
  - 웹팩에서도 MoudleConcatenationPlugin 이라는 플러그인으로 여러 모듈을 하나로 연결하여 클로져 생성을 최소화하는 작업을 함

### 하지만..모든 클로져를 합치는 것은 좋지 않다.

- module.exports 가 객체방식이어서

```js
// test.js
module.exports = { [globalThis.hello]: "world" };

// index.js

const hello = "hello";
globalThis[hello] = hello;
const test = require("./test.js");
console.log(test[hello]); // 'world'
```

- module.exports의 객체라는 특성 때문에 빌드 타임에서는 모듈에서 어떤 값이 불러와서 사용되는지 가늠 할 수 없다.
- 따라서 번들러들은 commonjs 로 되어있는 모듈 성능을 위해 하나의 거대한 클로저로 합쳐버린 대신 무엇이 실행될지 결정하는 작업을 포기한셈임
- 그에 반해 esmodule 은 export 라는 명확한 키워드를 사용하여 사용 여부를 결정할 수 있어서 트리쉐이킹 가능

### ESM 과 CJS 의 차이점 간략 요약

- CJS 는 동기적으로 / ESM 은 비동기로 실행
  - ESM 은 가져온 스크립트 바로 실행하지 않고 import, export 구문 찾아서 스크립트 파싱
  - 파싱단계에서 ESM 로더는 종속성이 있는 코드 실행하지 않고도 named imports에 있는 오타를 감지하여 에러 발생 가능
  - ESM 모듈 로더는 가져온 스크립트를 비동기로 다운 -> import 된 스크립트를 가져오고 -> 더 이상 import 할 것이 없어질 때 까지 import를 찾은 다음에 -> 디펜던시의 모듈 그래프를 만든다. -> 스크립트 실행 준비 마치고 -> 해당 스크립트에 의존하는 스크립트 실행 준비 마치고 -> 실행
  - ESM 모듈 내 모든 자식스크립트들은 병렬로 다운 되지만, 실행은 순차적으로!
