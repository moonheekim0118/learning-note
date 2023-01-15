# 프론트엔드 DDD 를 만나다

​
[프론트엔드, DDD를 만나다 - 박세문 - Google Slides](https://docs.google.com/presentation/d/1SW6tbChxThzmn70GB5nH160O9ktoA5MmSr87wARwObE/edit#slide=id.g15d750e36b5_0_391)
​

## 왜 DDD

​

- 복잡함 -> 단순함
- 커뮤니케이션을 위해
- 백엔드에서 DDD 와 프론트엔드에서 DDD의 유사성 - 리덕스 동작방식/사용방식이랑 매우 비슷하다.
  ​

## 어떻게 DDD 를 도입할 수 있을까?

​

### DDD 란?

​

- 실제 세상의 Product를 나타내는 소프트웨어를 만드는데 포커스를 둔다.
- Strategic Design
  - Bounded Context : 하나의 이름이 통용되는 범위를 정할 것.
    - 이 범위로 인해서 중복되는 문제의 범위를 지정해주고, 이를 통해 팀간 Conflic 발생 가능성을 줄여준다.
  - Ubiquitous Language : Bounded Context 안에서 사용되는 개념들에 대해 개발자-비개발자 사이에 공통적인 언어를 만들어서 커뮤니케이션 비용을 줄인다.
- Tactical Design : 시스템 구현 그 자체에 대해 , 시스템이 다양한 장소에서 다양한 서비스 간에 커뮤니케이션 하는 것에 초점을 둔다.
  - Event Sourcing, CQRS 와 같은 패턴을 사용하게 된다.
- Hexagonal Architecture - 위의 두가지를 바탕으로 도메인 모델을 어떻게 동작하는 소프트웨어로 만들지 설계
  ​

## Layered 구조

​
[##_Image|kage@dspt1g/btrWitrgMWz/LQ4efeoEjvevIJZBBkw4tK/img.png|CDM|1.3|{"originWidth":1040,"originHeight":582,"style":"alignCenter","caption":"null"}_##]
​

## Hexagonal 구조

​
[##_Image|kage@lpD5J/btrWeYyFtL4/Vkvro0DKioEmkEZHupKSn0/img.png|CDM|1.3|{"originWidth":1042,"originHeight":572,"style":"alignCenter","caption":"null"}_##][##_image|kage@ga5il/btrwdfohvjn/24vc7zr67emdcytce3exik/img.png|cdm|1.3|{"originwidth":1042,"originheight":596,"style":"aligncenter","caption":"null"}_##]
​

- adapter 가 하는 일은 상태관리 라이브러리들이 하는 일을 떠올리면 된다.
  ​

### 생각

​

- 리덕스를 생각하면 쉬울 것 같다.
- 결국 발표에서도 말씀해주시듯, 컴포넌트를 분리할 때는 Common 계층과 Domain에 종속적인 계층을 분리하는 것만으로도 큰 효과를 얻을 수 있을듯?

#

태그입력
