# Command-Query Separation (CQS)

- 한마디로 말하자면.. “질문이 답변을 수정해서는 안된다”
- CQS 패턴에서는 Command 와 Query 를 구분한다.
- Command 는 상태를 변경한다. 대신, 객체의 상태를 반환해서는 안된다.
- Query 는 객체의 상태를 반환한다. 대신, 값을 변경해서는 안된다.
  ​

## why?

- 부수효과의 영향을 최소화 하기 위해, 부수효과를 가진 함수(프로시져)-Command 와 부수효과를 가지지 않은 함수-Query 를 분리한다.
- 즉, 부수효과 발생 여부에 따라서 객체의 메서드를 Command , Query 로 구분한다.
- 이렇게 함으로써, 명령형 프로그래밍에서 함수형의 이점을 가질 수 있다.
  ​

## 함수가 부수효과를 가진다면

- 참조 투명성 (referential transparency)을 만족하지 못한다.
  - 참조 투명성이란, 함수가 함수 외부의 영향을 받지 않고, 함수의 결과는 입력 파라미터에만 의존한다는 것이다.
  - 즉, 함수 외부 값을 변경하지 않고, 외부에 의존적이지 않아야 한다.
- 참조투명성을 만족하지 못한다면, 함수가 예기치 않은 동작을 할 수 있고, 이에 따라서 디버깅이 어려워지며, 가독성을 해친다.
  ​

## 참고

- [http://aeternum.egloos.com/m/1125381](http://aeternum.egloos.com/m/1125381)
- [https://jinwooe.wordpress.com/2017/12/21/%EB%B6%80%EC%88%98-%ED%9A%A8%EA%B3%BC-side-effect-%EC%B0%B8%EC%A1%B0-%ED%88%AC%EB%AA%85%EC%84%B1-referential-transparency/](https://jinwooe.wordpress.com/2017/12/21/%EB%B6%80%EC%88%98-%ED%9A%A8%EA%B3%BC-side-effect-%EC%B0%B8%EC%A1%B0-%ED%88%AC%EB%AA%85%EC%84%B1-referential-transparency/)
