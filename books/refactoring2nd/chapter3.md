# 리팩터링 chp3. 코드에서 나는 악취

## 1. 기이한 이름

- 이름만 잘 지어도 나중에 문맥을 파악하느라 헤매는 시간을 크게 절약 할 수 있다.
- 이름 바꾸기는 단순히 이름을 다르게 표현하는 연습이 아니다. 마땅한 이름이 떠오르지 않는다면 설계에 더 근본적인 문제가 숨어 있을 가능성인 높다.

## 2. 중복 코드

- 똑같은 코드 구조가 여러 곳에서 반복되면 하나로 통합하여 더 나은 프로그램을 만들 수 있다.
- 함수 추출하기로 양쪽 모두 추출된 메서드를 호출하게 한다.
- 문장슬라이드하기로 비슷한 부분을 한 곳에 모아 함수추출하기를 더 쉽게 적용한다.
- 같은 부모로부터 파생되었을 경우 메서드 올리기를 적용한다.

## 3. 긴 함수

- 짧은 함수 => 간접 호출의 효과, 즉 코드를 이해하고 공유하고, 선택하기 쉬워진다.
- 짧은 함수로 구성된 코드를 이해하기 쉽게 만드는 방법은 좋은 이름이다.
- 함수 이름은 동작 방식이 아니라 **의도**가 드러나게 짓는다.
- 함수의 길이가 아닌, 함수의 목적(의도)과 구현 코드의 괴리가 얼마나 큰가이다. 즉, 무엇을 하는지를 코드가 잘 설명해주지 못할 수록, 함수로 만드는게 유리하다.

## 4. 긴 매개변수 목록

- 매개변수 목록이 길어지면 그 자체로 이해하기 어렵다.

## 5. 전역 데이터

- 전역 데이터는 코드베이스 어디에서든 건드릴 수 있고, 값을 누가 바꿨는지 찾아낼 메커니즘이 없다.
- 변수를 캡슐화 하여, 다른 코드에서 오염시킬 가능성이 있는 데이터를 보호하자.

## 6. 가변 데이터

- 데이터를 변경했더니, 예상치 못한 결과가 나올 수 있다. 특히 이 문제가 아주 드문 조건에서만 발생한다면 원인을 알아내기도 어렵다.
- 이러한 이유로 함수형 프로그래밍에서는 데이터는 절대 변하지 않고, 데이터를 변경하려면 반드시 변경하려는 값에 해당하는 복사본을 만들어 반환한다. (불변성)

## 7. 뒤엉킨 변경

- 뒤엉킨 변경은 단일 책임 원칙이 지켜지지 않을 때 나타난다.
- 즉, 하나의 모듈이 서로 다른 이유들로 인해 여러 가지 방식으로 변경되는 일이 많을 때 발생한다.
- (문제) 하나의 모듈에 여러 코드가 뭉쳐진 현상
- (해결) 맥락별로 분리하여 해결하자.

## 8. 산탄총 수술

- (문제) 하나의 모듈이 여러 코드에 흩뿌려진 현상
- (해결) 맥락별로 모아서 해결하자

## 9. 기능 편애

- 어떤 함수가 자기가 속한 모듈의 함수나 데이터보다 다른 모듈의 함수나 데이터와 상호작용 할 일이 더 많을 때 풍기는 냄새다.

## 10. 데이터 뭉치

- 데이터 뭉치인지 판별하려면 값 하나를 삭제해보자. 그랬을 때 나머지 데이터만으로는 의미가 없다면 객체로 환생하기 갈망하는 데이터 뭉치다.

## 11. 기본형 집착

- 기본형을 객체로 바꾸기를 적용하면, 기본형만이 거주하는 구석기 동굴을 의미있는 자료형들이 사는 최신 온돌식 코드로 탈바꿈 할 수 있다.

## 12. 반복되는 switch 문

- switch 문은 조건부 로직을 다형성으로 바꾸기로 개선 가능하다.

## 13. 반복문

- 반복문을 파이프라인으로 바꾸기를 적용하여, 시대에 걸맞지 않은 반복문을 제거할 수 있게 된다.

## 14. 성의없는 요소

- 코드 구조 잡을 때 프로그램 요소를 이용하는걸 좋아한다. 그래야 그 구조를 변형하거나 재활용할 기회가 생기고, 혹은 단순히 더 의미있는 이름을 가졌기 때문이다.
- 그렇지만, 그 구조가 필요 없을 때도 있다.

## 15. 추측성 일반화

- '나중에 필요할 거야'라는 생각으로 당장은 필요 없는 모든 종류의 후킹 포인트와 특이 케이스 처리 로직을 작성해둔 로직에서 풍기는 냄새다.

## 16. 임시 필드

- 특정 상황에서만 값이 설정되는 필드를 가진 클래스가 있다.
- 하지만, 객체를 가져올 때는 보통 모든 필드가 채워져있는 것을 기대하므로 임시 필드를 갖도록 하는 것은 이해하기 어렵다.
- 그래서 사용처에서는 쓰이지 않는 것 처럼 보이는 필드가 존재하는 이유를 파악하느라 머리를 싸맨다.

## 17. 메시지 체인

- 메시지 체인은 클라이언트가 한 객체를 통해 다른 객체를 얻은 뒤, 방금 얻은 객체에 또 다른 객체를 요청하는 식으로, 다른 객체를 요청하는 작업이 연쇄적으로 이어지는 코드를 말한다.

- 이는 클라이언트가 객체 내비게이션 구조에 종속됐음을 의미한다.
- 내비게이션 중간단계를 수정하면, 클라이언트 코드도 수정해야하는 문제점이 있다.

## 18. 중개자

- 클래스가 제공하는 메서드 중 절반이 다른 클래스에 구현을 위임하고 있다면? 이럴 때는 중개자 제거하기를 활용하여 실제로 일을 하는 객체와 직접 소통하게 하자.

## 19. 내부자 거래

- 모듈 사이의 데이터 거래가 많으면 결합도가 높아진다. 따라서, 그 양을 최소로 줄이고 모두 투명하게 처리해야 한다.

## 20. 거대한 클래스

- 한 클래스가 너무 많은 일을 하려다 보면 필드 수가 상당히 늘어난다. 그리고 클래스에 필드가 너무 많으면 중복코드가 생기기 쉽다.

## 21. 서로 다른 인터페이스의 대안 클래스

- 클래스를 사용할 때 큰 장점은 필요에 따라 언제든 다른 클래스로 교체할 수 있다는 것.
- 단, 교체하려면 인터페이스가 같아야 한다. 따라서, 함수 선언 바꾸기로 메서드 시그니쳐를 일치시킨다.
- 위로 부족하다면, 함수 옮기기를 이용하여 인터페이스가 같아질 때 까지 필요한 동작들을 클래스 안으로 밀어넣는다. 그러다 대안클래스들 사이에 중복코드가 생기면 ㅊ슈퍼 클래스 추출하기를 적용할지 고민하자.
