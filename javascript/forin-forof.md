# for...in 과 for...of 의 차이점

`for...in`과 `for...of` 은 둘다 기존의 `for loop`을 대체하여 자료구조를 순회하는 역할을 한다.
그렇다면 두 방법은 어떤 차이가 있는지 알아보자

## for...of

```javascript
const arr = ["a", "b", "c"];
for (let value of arr) {
  console.log(value); // 출력 결과 : a, b, c
}
```

1. `Iterable Object`를 순회 한다. 즉 해당 자료구조의 [**Object Iterator**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)를 사용한다.
   - 배열 , String, Set, Map, 유사배열 (NodeList) 등
2. 해당 자료구조의 **값 (value)** 을 순회한다.

## for...in

```javascript
cosnt arr = ['a','b','c'];
for (let key in arr) {
  console.log(key); // 출력 결과 : 0, 1, 2
}

```

1. **열거 가능한 (Enumerable) Non-Symbol 속성의 키 값**을 순회 한다.
   - `for..in`문은 객체 자체의 모든 열거 가능한 속성들과 프로토타입 체인으로부터 상속받은 속성들의 키 값을 순회한다.
   - Symbol 로 키(key)가 지정된 속성은 무시한다.
   - 배열, 객체, String, Set, Map, 유사배열 (NodeList) 등
2. 객체의 `key` 값을 순회한다. 따라서 값(value)에 접근하기 위해서는 key를 이용하여 참조해야한다.

<br/>
<br/>

## 배열 순회 시 어떤걸 사용해야하나?

결론부터 말하자면 `for...of`를 사용하는 편이 좋다.
`for...in` 순회시에는 아래와 같은 문제점이 있다.

### 1. 순회 순서를 보장하지 못한다.

```javascript
// IE 에서는 아래와 같은 끔찍한 결과가 도출된다.
const arr = [];
arr[2] = "two";
arr[1] = "one";
arr[0] = "zero";

for (let i in arr) {
  console.log(i);
}
// 출력 : 2, 1, 0
```

`for...in`문은 **임의의 순서**로 객체의 속성들을 순회한다. `length 를 지정해 for - loop` 을 실행하는 것과, `Object Iterator`를 사용해 순회하는 것과 달리 `객체의 속성`을 순회하기 때문이다.
따라서 반복하는 동안 객체의 속성이 변경 (추가, 수정, 제거) 될 때 문제가 생길 수 있다.
_예를 들어 반복 중 속성을 수정 시, 수정된 속성을 수정 이전 혹은 이후에 방문 할 것인지 보장 할 수 없고
반복 중 속성을 삭제 할 시에 삭제된 속성을 삭제 이전에 방문할 것인지 보장 할 수 없기 때문이다. _

따라서 순회의 순서와 index가 중요한 배열에서는 `for...in`을 사용하지 않는 것이 좋다.

<br/>

### 2. 배열의 크기를 제대로 반영하지 못한다.

```javascript
const arr = [];
arr[5] = "foobar";
```

위와 같이 크기를 resize 한 배열의 `for...of` 와 `for...in` 실행 결과는 아래와 같다.

#### for..of 실행 결과

```javascript
for (let i of arr) {
  console.log(i);
}
// 출력
// undefined
// undefined
// undefined
// undefined
// "foobar"
```

#### for..in 실행결과

```javascript
for (let i in arr) {
  console.log(i);
}
// 출력
// 5
```

왜 이런 결과가 나오는걸까?
`for..of` 는 위에서도 설명했듯이 `Object Iterator`를 사용하기 때문에 resize 된 배열의 전체를 올바르게 순회한다.

`for..in` 은 단순히 객체의 속성을 순회하기 때문에, 명시적으로 지정된 속성인 _5:foobar_ 만 순회한다.

<br/>

### 3. 상속받은 속성도 순회한다.

```javascript
Array.prototype.foo = "hello";
const arr = ["foo", "bar"];

for (let i in arr) {
  console.log(i);
}
// 출력
// 0
// 1
// foo
```

위에서 언급했듯이, `for..in`은 단순히 해당 객체의 속성 뿐만 아니라 상속받은 속성도 순회한다. 따라서 위와 같은 문제가 생길 수 있고, 만약 사용중인 자바스크립트 라이브러리로부터 `Array.prototype`에 추가된 속성이 있다면, 원치 않는 결과를 도출 할 수도 있다.

<br/>
<br/>

## 그러면 for..in은 언제 사용해야할까?

키-값으로 맵핑되어 저장되는 데이터의 경우 객체에 특정 값을 가진 키가 있는지 확인하려는 경우에 `for...in`을 사용하면 좋다.

<br/>
<br/>

## 참고

- [What is the difference between ( for… in ) and ( for… of ) statements?](https://stackoverflow.com/questions/29285897/what-is-the-difference-between-for-in-and-for-of-statements)
- [MDN JavaScript for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)
- [Why is using “for…in” for array iteration a bad idea?](https://stackoverflow.com/questions/500504/why-is-using-for-in-for-array-iteration-a-bad-idea)
