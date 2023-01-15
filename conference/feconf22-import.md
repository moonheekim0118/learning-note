# 내 import 문이 그렇게 이상했나요?

## 이전의 자바스크립트

- 모듈 시스템이 없었다.
- 라이브러리를 사용 할 땐 스크립트 태그를 사용해야했다.
- 그러다보니 전역변수/객체를 정의하니 문제가있었다. - 변수명이 겹친다.
  ​

## CommonJS 모듈 시스템

- require 문 도입
- 파일 단위의 개발
  - 수백개, 수천개의 js 파일로 분리 가능
- 손쉬운 라이브러리 함수 재사용
  ​

## 가짜 import 의 비밀 : TS, babel

- TSC/babel 은 import-로 작성하면 commonJS 로 변환한다.
  ​

## CommonJS 의 문제점

​

- Common JS 는 언어 표준이 아니다.
  - node, deno 환경이 없으면 돌아가지 않는다.
- 정적 분석의 어려움
  - 조건적으로 호출하거나..삼항연산자를쓰거나..이런것들이 가능해서
  - 조용한 require 함수 재정의 가능 (덮어쓰기)
- 비동기 모듈 정의 불가능
  ​

## ESM

- 정적 분석 쉬움
- 쉬운 비동기 모듈
- esm은 언어표준 - node.js 뿐 아니라 브라우저,deno 등 다양한 런타임에서 사용가능
  ​
- ESM 도입으로 해결하쟈~
  ​

## ESM 으로 옮기기 어려운 이유

- 우리가 사용하는 가짜 ESM’
- 성숙하지 않은 생태계
  ​

## 가짜 import 진짜 import 차이

```
​
// 가짜
​
import { Component } from './MyComponent';
​
// 진짜
​
import { Component } from './MyComponent.js';
```

​

## 생각

- 생각못해본 부분이네ㅎㅎ..우리가 지금 쓰고 있는 import문은 tsloader나 바벨이 require문으로 돌려주는..그냥 가짜 import문이었구나
