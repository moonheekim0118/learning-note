# 내 코드의 품질을 높여주는 Type-Driven Development

<iframe src="https://www.youtube.com/embed/M3pMCZqPvzI" width="950" height="534" frameborder="0" allowfullscreen=""></iframe>

## 타입 주도 개발

- 타입을 우선 작성한다.
- 컴파일러에 깊게 의존한다.
- 일부 테스트를 대체한다.

## 컴파일 타임에 타입을 체크하는 언어가 대세가 될 것 이다.

### 전제 1

피드백은 빠를 수록 좋기 때문에.

### 원칙 1. 타입을 먼저 작성한다.

- 왜? 타입은 컴파일 시간에, 테스트보다 빠르게 피드백을 줄 수 있는 도구
- 코드의 의도를 쉽게 볼 수 있다.
- 단점: 코드가 길어진다?
  - 하지만, 타입을 통해서 단순한 타입레벨의 테스트는 작성 할 필요가 없어져서 코드가 줄어들게 된 것!
  - 작성한 타입만큼 테스트를 줄였다.

## 함수형 프로그래밍과 타입

- 함수형프로그래밍은 프로그램을 일련의 데이터 변환 과정으로 정의합니다.
  - 데이터변환: 입력을 받아서, 다른 출력으로 전환하는 함수 f 를 프로그램이라고 부르는 것 과 같다.
  - 고차함수를 이용해서, 프로그램의 연쇄를 구현하는 것
- 함수형으로 만들었다 = 부수효과가 없이 순수하게 만들었다.
- 즉, 프로그램은 아래로 구성되어 있다.
  - 데이터 구조 (Data Structure)
  - 변환과정 (State Machine)
- 프로그램의 모든 부분은 타입 시스템으로 검증 가능하다.

### 하지만..드러나지 않는 부분도 있다.

- Mutable State
- Side-Effect

### 전제 2

- 암묵적인 것 보다 명시적인 것이 낫다.
  - 암묵적으로 존재하던 mutable 한 state 나 부수효과를 명시적으로 타입수준으로 끌어리기

### 원칙 2. 가능한 모든 맥락을 명시적으로 선언한다.

- 불변객체가 더 좋다.
  - 즉, 뮤테이션하지 말고 새로 변경된 객체를 반환해라.
- 데이터 뿐만 아니라 상태도 타입으로 기술하기 좋다.
- `type State = { todoList: TodoList; isLoading: boolean; }`
- 근데, 로딩 중에 `newTodo()` `updateTodo()` 호출하면 어떡하지?

### 원칙 3. 불가능한 것을 불가능하게 만들자

- 로딩 중에 todoList 객체에 액세스 할 수 없게 만들기
- `type State = { | { kind: 'Loading' } | { kind: 'Ready', tdoList:TodoList } }`
- 로딩 중에는 todoList 객체에 액세스 할 수 없을 것이라는 것은, 컴파일러가 검증해준다.

## 브라우저에는.. Mutable State 가 난무하는 DOM API가 있는데..

### 원칙4. 가능한 일찍 순수한 데이터로 변환한다.

- 리덕스에서 action 을통한 객체 뮤테이션
- `fetch('어쩌구').then(res => res.json()) .then(TodoList.fromJson) .then(todoList => dispatch({kind:'Init', todoList});`

```
function parseEvent(e:Event):Action{
const text = e.target.value;
return { kind:'AddTodo', text };
}

const handleSubmit = dispatch => e = > {
// 가능한 일찍 호출해서, 시스템 지식인 Event 타입이 프로그램까지
// 전파되지 않도록 한다.
const action = parseEvent(e);
dispatch(action);
}
```

### 원칙 5. 프로그램을 시스템으로부터 격리한다.

[##_Image|kage@dWpjAO/btrWggsh3KC/KojXMbTr9vMkJIKiAqfmI0/img.png|CDM|1.3|{"originWidth":816,"originHeight":512,"style":"alignCenter","caption":"null"}_##]

- 우리가 통합하고 있는 시스템과, 우리가 만들고있는 프로그램(State) 는 격리
- 그 격리 사이에 SandBox 계층이 존재 (리액트와 같은 프로그램)

### 원칙 6. 가능한 타입을 단순하게 유지하기

- 애초에 아주 복잡한 타입이 왜 필요했는지 봐라
- 복잡한 타입이 필요한 함수를 만들지 말라
- 즉 다형성이 아니라, 단형성을 유지해라

## 성능

### 불변성

- 더 일관적인 성능을 보인다.
- 더 최적화하기 쉽다.Monomorphism vs Polymorphism 단형성 vs 다형성
- 모노모픽하게 타입을 유지할 수록 성능이 더 좋다.

## 생각

- 테스트코드를 최소화하고 컴파일 시 타입체크에 최대한 의존한다는 생각 자체가 매우 좋은 것 같다. 컴파일러가 제일 좋은 테스트도구다.
- 다형성보다 단형성을 추구하는게 제일 신기한 포인트였다. 굉장히 함수형프로그래밍적인 사고인데, 다른 타입-같은 동작을 하게 된다면 하나의 함수에서 처리하는게 아니라, 여러 함수를 만드는게 예기치 못한 예외를 방지할 수도 있기에 더 좋다. 물론 case by case 이겠지만..
