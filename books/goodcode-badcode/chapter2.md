# 추상화 계층

- 코드의 작성 목적은 문제해결이다.
- 스스로 인지를 못하지만, 우리는 상위 수준의 문제를 풀 때 보통 문제를 여러 개의 작은 하위 문제들로 나눈다.
- 코드를 잘 구성한다는 것은 간결한 추상화계층을 만드는 것으로 귀결된다.

## 왜 추상화 계층을 만드는가?

- 코드 작성은 복잡한 문제를 계속해서 더 작은 하위 문제로 세분화하는 작업이다.
- 어떤 문제를 하위 무제로 계속해서 나누어 내려가면서 추상화 계층을 만든다면, 같은 층위 내에서는 쉽게 이해할 수 있는 몇 개의 개념만을 다루기 때문에 개별 코드는 특별히 복잡해보이지 않을 것이다.
- 비록 문제가 엄청 복잡할지라도 하위 문제를 식별하고 올바른 추상화 계층을 만듦으로써 그 복잡한 문제를 쉽게 다룰 수 있다.

## 추상화 계층 및 코드 품질의 핵심 요소

### 1. 가독성

- 깨끗하고 두렷한 추상화 계층을 만드는 것은 개발자가 한 번에 한 두개 정도의 계층과 몇 개의 개념만 다루면 된다는 것을 의미한다.
- 따라서, 코드의 가독성이 크게 향상한다.

### 2. 모듈화

- 추상화 계층이 하위 문제에 대한 해결책을 깔끔하게 나누고 구현 세부사항이 외부로 노출 되지 않도록 보장할 때, 다른 계층이나 코드의 일부에 영향을 미치지 않고 계층 내에서만 구현을 변경하기가 매우 쉬워진다.
- 상위수준 코드에서는 다양한 상황에 대처하기 위해 특별한 작업을 수행 할 필요가 없다.

### 3. 재사용성 및 일반화성

- 하위 문제에 대한 해결책이 간결한 추상화 계층으로 제시되면, 해당 하위 문제에 대한 해결책을 재사용하기 쉬워진다.
- 문제가 적절히 추상적인 하위문제로 세분화 된다면, 해결책은 여러 가지 다른 상황에서 유용하게 일반화될 가능성이 크다.

### 4. 테스트 용이성

- 코드가 추상화 계층으로 깨끗하게 분할되면 각 하위 문제에 대한 해결책을 완벽하게 테스트하는 것이 더 쉬워진다.

## 코드의 계층

- 추상화 계층을 생성하는 방법은?
  - 코드를 서로 다른 단위로 분할하여 단위 간의 의존 관계를 보여주는 의존성 그래프를 생성하는 것이다.

### 1. API 및 구현 세부사항

코드를 작성 할 때 고려해야 할 두가지 측면이 있다.

- 코드를 호출 할 때 볼 수 있는 내용
  - 퍼블릭 클래스, 인터페이스 및 함수
  - 이름, 입력 매개변수 및 반환 유형이 표현하고자 하는 개념
  - 코드 호출 시 코드를 올바르게 사용하기 위해서 알아야하는 추가정보 (ex. 호출 순서)
- 코드를 호출 할 때 볼 수 없는 내용: 구현 세부 사항

- API는 서비스를 사용할 때 알아야 할 것들에 대한 개념을 형식화 하고, 서비스의 모든 구현 세부사항은 이 API 뒤로 가뭋ㄴ다.
- 코드의 일부를 작성하거나 수정할 때 (매개변수, 반환유형 등등을 통해) API 의 수정사항에 대한 구현 세부 정보가 세어나간다면, 추상화 계층이 명확하게 구분되어 이루어진 것이 아니다.

### 2. 함수

함수가 하는 일을 다음 중하나로 제한하면 이해하기 쉽고 단순한 한 문장으로 표현되는 함수를 작성하기 위한 좋은 전략이 된다.

1. 단일 업무 수행
2. 잘 명명된 다른 함수를 호출해서 더 복잡한 동작 구성

- 하지만, 단일 업무라는 것은 해석하기 나름이고, 다른 함수를 호출해서 더 복잡한 동작을 구성할 때도 여전히 약간의 제어 흐름(if문, for문)이 필요할 수 있다.
- 일단 함수를 작성했으면, 작성된 코드를 문장으로 만들어보면 좋다.
- 문장을 만들기 어렵거나 너무 어색하면 함수가 너무 길다는 것을 의미하고, 더 작은 함수로 나누는 것이 유익할 것이다.

### 3. 클래스

- 응집도

  - 하나의 클래스 내에 모든 요소들이 얼마나 잘 속해있는지 보여주는 척도이다.
  - 좋은 클래스는 매우 응집도가 강하다.
  - `순차적 응집도`: 이것은 한 요소의 출력이 다른 요소에 대한 입력으로 필요할 때 발생한다.ex 커피마시기
  - `기능적 응집도`: 몇가지 요소들이 모여서 하나의 일을 성취하는데 기여할 때 발생한다. ex. 케이크를 만들기 위한 모든 장비를 부엌의 전용서랍에 보관하는 것.

- 관심사의 분리

  - 시스템이 각각 별개의 문제(관심사)를 다루는 개별 구성요소로 분리되어야 한다는 것.
  - ex. 게임 콘솔이 TV와 동일한 제품으로 묶이지 않고 TV와 분리되는 방식..

- 응집도와 관심사의 분리에 대해 생각할 때는 서로 관련된 여러가지 사항을 하나의 사항으로 간주하는 것을 어느 수준에서 해야 유용할지 결정해야 한다.
- 이것은 매우 주관적일 수 있어서, 종종 보기보다 까다로울 수 있다. 어떤 사람에게는 원두를 갈고 커피를 추출하는 것을 하나로 묶는 것이 매우 합리적이지만, 요리를 위해 향신료를 갈고 싶어하는 다른 사람에게는 이렇게 묶는 것이 매우 도움이 되지 않는 것으로 비춰질 수 있다. (왜냐하면 향신료를 갈고 나서 커피처럼 그것을 우려내지 않을 것이므로..!)

### 4. 인터페이스

- 계층 사이를 뚜렷이 구분하고 구현 세부사항이 계층 사이에 유출되지 않도록 하기 위해서 사용 할 수 있는 한 가지 접근법은, 어떤 함수를 외부로 노출 할 것인지를 인터페이스를 통해결정하는 것이다.
- 그 다음 인터페이스에 정의된 대로, 클래스가 해당 계층에 대한 코드를 구현한다.
- 이보다 위에 있는 계층은 인터페이스에 의존할 뿐, 로직을 구현하는 구체적인 클래스에 의존하지 않는다.

## 층이 너무 얇아질 때

- 코드를 별개의 계층으로 세분화하면 장점이 많지만 다음과 같은 추가 비용이 들어간다.

1. 클래스를 정의하거나 의존성을 새 파일로 임포트하려고 반복적으로 사용하는 코드(보일러플레이트)로 인해 코드의 양이 늘어난다.
2. 로직의 이해를 위해 파일이나 클래스를 따라갈 때 더 많은 노력이 필요하다.
3. 인터페이스 뒤에 계층을 숨기게 되면 어떤 상황에서 어떤 구현이 사용되는지 파악하는데 더 많은 노력이 필요하다.
   이로 인해 로직을 이해하거나 디버깅하는 것이 더 어려워질 수 있다.

- 코드를 서로 다른 계층으로 분할해서 얻는 장점과 비교하면, 이 비용이 상당히 낮지만 분할을 위한 분할은 의미가 없다는 것을 명심해야 한다.
- 계층을 너무 얇게 만들면 단일 계층으로 만들어도 될 것을 둘로 분해한 것이고, 이것은 불필요한 복잡성을 초래 할 수 있다.
