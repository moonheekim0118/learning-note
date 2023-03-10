# 나는 왜 리액트를 사랑하는가

https://www.youtube.com/watch?v=dJAEWhR83Ug

출근길 지하철에서 본 영상이다. 영상을 보면서 아주 빠르게 바뀌는 프론트엔드 생태계에서 왜 여전히 리액트의 위치가 견고한지 이유를 알 수 있었다. 또한, 내가 왜 리액트를 좋아하는지에 대한 멘탈모델도 단단하게 만들 수 있었다.  
영상초반에서는 리액트를 하나의 UI 프로그래밍 언어로 바라보고 설명한다.  
짤막하게 설명하자면

- 프로그래밍 언어의 값 : React Element
- 프로그래밍 언어의 함수 : React Component
- 프로그래밍 언어의 try-catch : Error Boundary
- 프로그래밍 언어의 정적타입 체크 : Prop-Types
- 프로그래밍 언어의 엔진 : Reconciler
- 프로그래밍 언어의 어셈블리 : 호스트 환경

또한 리액트를 사용 할 때 react 와 react-dom 이 분리되어 있는 이유도 설명된다. 나도. 처음에는 이 두개의 패키지가 분리되어 있는 이유가 납득이 되지 않았지만, 이렇게 함으로써 같은 언어 (리액트) 를 다른 호스트 환경 (브라우저, 네이티브 앱, 터미널)에서 사용 할 수 있게 된다.  
따라서 리액트는 하나의 호스팅 환경에 제한 된 프레임워크가 아니라, 같은 문법으로 여러 호스팅 환경에서 구동 가능한 프로그래밍 언어처럼 동작할 수 있다.

## 리액트의 환원

환원(還元, Reduction)이란?

- 본디의 상태로 다시 돌아감. 또는 그렇게 되게 함.
- 잡다한 사물이나 현상을 어떤 근본적인 것으로 바꿈. 또는 그런 일.

새로운 문제 A 가 생겼는데,  
이러이러한 면에서  
답안지가 존재하는 문제 B 랑 되게 비슷한데 ?

를 알 수 있다면, B 라는 문제의 해결책을 A 라는 문제의 해결책으로 사용 할 수 있다.

영상의 후반부에서는 리액트의 환원을 설명하면서, 리액트가 어떻게 계속해서 직면한 문제를 우아하게 해결하고자 하는지 설명한다.

설명되는 환원의 사례는 아래와 같다.

- Context API  
  “컴포넌트가 트리 저 위쪽에 정의 된 무언거로부터 값을 꺼내올 수단이 필요한데..”  
  “근데 이게 참조 시점에 둘러싼 환경을 기준으로 평가되는 변수니까..”  
  “프로그래밍 언어의 동적 스코핑이랑 비슷한데..?”
- Fiber Reconciler  
  “JavaScript 싱글 스레드 환경에서 느린 컴포넌트가 우선순위 높은 업데이트를 막아 생기는 반응성 저해를 방지할 수단이 필요한데..”  
  “ 하나의 실행 주체로 우선순위가 다른 여러 작업이 동시에 잘 실행되게 만드는 일이니까..”  
  “운영체제의 스케쥴링이랑 되게 비슷한데?”
- Hooks  
  “ 함수 컴포넌트의 제약을 제거하고, 상태 로직의 응집성, 재사용성을 개선 하고 싶은데..”  
  “특정 효과(상태,라이프사이클 이펙트..)의 처리를 리액트에게 위임할 수단을 찾아야하는거니까..”  
  “대수적 효과랑 되게 비슷한데?”

### 대수적 효과란?

- 대수적 효과는 컴퓨터 효과의 접근 방식 중 하나로, 특정 연산 집합이 불순한 부수 효과를 불러 일으키는 것으로 전제합니다. 이런 접근 방법에서 부수 효과는 어떤 연산이 무언가를 불러 일으키는 방식으로 표현됩니다.  
  컴퓨터 효과(Computational Effect)란 컴퓨터 동작에 대한 기술(記述)입니다. 함수가 값을 리턴하는 것도, 변수에 값을 집어넣는 것도 모두 컴퓨터 효과입니다. 어떤 컴퓨터적 효과가 대수적이라면 그것을 하나의 특정한 연산자로 묶는게 가능합니다. 대수학의 군(group)처럼, 어떤 집합에 대한 조건에 맞는 연산을 정의하고 식으로 표현하듯 부수효과를 나타낼 수 있습니다.  
  대수적 효과는 Effects(특정 연산)과, Effect Handlers(연산이 일으키는 부수효과)로 이루어져 있습니다. Effect Handler는 Effect가 발생하는 것에 대응해 호출되는 로직으로 특정 동작을 실행하거나 특정 값을 리턴합니다.  
  [김맥스 기술 블로그 | Suspense for Data Fetching의 작동 원리와 컨셉 (feat.대수적 효과)](https://maxkim-j.github.io/posts/suspense-argibraic-effect)

이렇게 환원이 무엇이고, 리액트에서 환원의 사례들을 살펴보다보니, 결국 ‘환원’이 리액트 자체의 동작원리 뿐만 아니라 프로그래밍, 혹은 엔지니어링 자체에서 중요한 개념 혹은 방법론이 될 수 있겠다고 생각했다.  
개발 할 때 마다 새로운 문제들을 직면하게 되는데 그 때 문제를 단순하게 현재의 관점에서만 바라보지 않고, 환원시켜 바라봄으로써, 기존에 존재하는 답안지를 참고하여 해결책을 보다 더 우아하게 찾을 수 있지 않을까? 하는 생각을 했다.  
발표 후반에도 이렇게 팀에서 처한 문제를 환원시켜 바라보고 기존의 답안지를 해결책으로 도입하여 문제를 해결하는 예시가 나온다.

개발 할 때 늘 느끼는 건데, 우리가 개발을 하면서 직면하는 문제들의 대부분은 형태만 다르지 그 문제의 핵심은 이미 누군가가 발견하고, 해결책까지 발견해놓았다는 것이다. 리액트 역시도 이러한 개념을 통해서 끊임 없이 우아하게 문제들을 해결해나가고 있는 중인 것이고.
