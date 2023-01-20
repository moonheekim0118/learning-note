# 📍 전송 계층 (Transport Layer)

[전송계층](https://velog.io/@moonheekim0118/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-OSI-7%EA%B3%84%EC%B8%B5#4-%EC%A0%84%EC%86%A1-%EA%B3%84%EC%B8%B5-transport-layer)은 엔드포인트간 **신뢰성** 있는 데이터 **전송**을 담당하는 계층이다.

- 신뢰성 : 데이터를 순차적 , 안정적으로 전달한다.
- 전송 : *포트 번호*에 해당하는 프로세스에 데이터를 전달한다.

## 전송계층이 없다면 ?

- 데이터의 순차 전송이 원활하지 않다.
- **흐름 문제 (Flow)** : 송수신자 간 데이터 처리 속도 차이가 존재 할 수 있으며, 수신자가 데이터 한계량을 초과했는데 송신자 측에서 데이터를 전송하려고 할 경우 데이터가 누락되는 문제가 발생한다.
- **혼잡 문제 (Congestion)** : 네트워크 데이터 처리 속도에 의해서 데이터가 제대로 전송되지 않을 수 있다.

**데이터의 손실이 발생한다. **
_이런 문제를 해결하기 위해서 TCP가 등장한다. _

<br/>
<br/>

# 📍 TCP (Transmission Control Protocol)

- 신뢰성 있는 데이터 통신을 가능하게 해주는 프로토콜
- 양방향 통신을 통해 Connection 을 연결한다 (3-way handshake)
- 데이터 순차 전송을 보장한다.
- Flow Control, 흐름을 제어 한다.
- Congestion Control, 혼잡을 제어한다.
- Error Detection , 오류를 감지한다.

## 세그먼트 (Segment)

![](https://images.velog.io/images/moonheekim0118/post/b9944aab-adb4-4402-b433-df339706338d/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3.jpeg)

- TCP 프로토콜 내부 데이터 단위
- 상위 레이어에서 전송된 데이터를 TCP 내부에서 자르고 **TCP 헤더**를 추가한 것

## TCP 헤더

![](<https://images.velog.io/images/moonheekim0118/post/8e0009e3-d4d2-464d-bc51-2204fae812e2/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20(1).jpeg>)

- `SYN` : 커넥션 연결
- `FIN` : 커넥션 연결 종료
- `ACK` : 데이터 수신자의 응답 제어

## TCP 3-way handshake (Connection 연결)

![](<https://images.velog.io/images/moonheekim0118/post/71958a89-52aa-453d-9158-1374231f644b/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20(2).jpeg>)

1. 클라이언트 측에서 SYN 비트를 1로 설정하여 패킷을 전송한다.
2. 서버 측에서 응답을 알리기 위해 SYN, ACK 비트를 1로 설정하여 패킷을 전송한다.
3. 클라이언트측에서 다시 ACK 비트를 1로 설정하여 패킷을 전송한다.

이렇게 해서 양방향 커넥션이 연결되면 아래와 같이 데이터 전송을 한다.

## 데이터 전송 과정

![](<https://images.velog.io/images/moonheekim0118/post/c3404afe-b044-48bd-bf97-3acfa9fc0b54/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20(3).jpeg>)

1. 클라이언트 측에서 패킷을 송신한다.
2. 서버 측에서 응답을 알리기 위해 ACK를 송신한다.
   _3. ACK 를 수신하지 못했을 경우 , 클라이언트 측에서 패킷을 재전송한다._

## 4 way-handshake (Connection close)

![](<https://images.velog.io/images/moonheekim0118/post/008370b8-ac19-44d9-a03a-b3c9d90c5f7f/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20(4).jpeg>)

1. 클라이언트 측에서 FIN 비트를 1로 설정하고 서버측에 전송한다.
2. 서버측에서 응답을 알리기 위해 ACK 를 전송한다.
   **_(TIME_WAIT) 서버측에서 남은 패킷을 클라이언트 측에 전송한다._**
3. 서버측에서 남은 패킷을 모두 전송한 후, 클라이언트 측에 FIN을 전송한다.
4. 클라이언트 측에서 응답을 알리기 위해 ACK를 전송한다.

## TCP 의 문제점

- 매번 커넥션을 연결해서 시간 손실 발생
- 패킷을 조금만 손실해도 재전송하는 문제점

_이러한 TCP의 단점을 보완하기위해 나온 것이 UDP_

<br/>
<br/>

# 📍 UDP (User Datagram Protocol)

- TCP보다 신뢰성이 떨어지지만 전송 속도가 일반적으로 빠른 프로토콜 ( 순차전송 X, 흐름제어 X, 혼잡 제어 X)
- 무연결성
- Error Detection
- 비교적 데이터의 신뢰성이 중요하지 않을 때 사용한다. (ex) 영상 스트리밍)

## User Datagram

![](<https://images.velog.io/images/moonheekim0118/post/e9d5d87d-24a7-45ef-a4d8-d01203971205/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20(5).jpeg>)

- UDP 프로토콜 내부 데이터 단위
- TCP와 달리, 데이터를 자르지 않고 데이터에 UDP 헤더를 추가한다. (따라서 데이터를 쪼개야 할 경우 응용 계층에서 데이터를 직접 잘라야 한다.)

## UDP 헤더

![](data:image/png;base64,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)

## UDP 데이터 전송 과정

![](<https://images.velog.io/images/moonheekim0118/post/e730a3bf-3057-48ad-818b-798aafc1ea5a/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3%20(6).jpeg>)

<br/>
<br/>

# 참고 / 이미지 출처

- [gatevidyalay - TCP header](https://www.gatevidyalay.com/wp-content/uploads/2018/09/TCP-Header-Format.png)
