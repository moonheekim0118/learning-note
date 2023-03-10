## HTTP와 HTTPS 비교

- HTTP 는 서로 다른 시스템들 사이에서 통신을 주고받게 하는 가장 기본적인 프로토콜
- 이 프로토콜은 서버에서 브라우저로 데이터를 전송하는 용도로 가장 많이 사용한다.
- 이 때 문제점은, 서버에서 브라우저로 전송되는 정보가 암호화 되지 않는다는 것이다.
- 따라서 데이터가 쉽게 도난 당할 수 있다.

### HTTPS 는?

- HTTPS는 HTTP 에 SSL 을 사용한 프로토콜이다.
- HTTPS 는 전송되는 정보가 암호화되지 않는 문제점을 SSL(보안소켓계층)을 사용하여 해결하고자 했다.
- SSL 은 서버와 브라우저 사이에 안전하게 암호화 된 연결을 만들 수 있게 도와주고, 서버와 브라우저가 민감한 정보를 주고 받을 때 해당 정보가 도난당하는 것을 막아준다.
- HTTPS 는 HTTP 자체를 암호화 하는 것은 아니다.
- HTTP 를 사용하여 운반하는 내용, 즉 HTTP 바디 메시지를 암호화 한다.
- 이 때 HTTP 헤더는 암호화 되지 않는다.

### 왜 HTTPS 를 사용해야 하는가?

1. 보안성
2. SEO

- 구글은 https 를 사용하는 웹사이트에 가산점을 부여한다.
- AMP(가속화 된 웹페이지)를 만들때는 HTTPS 를 사용해야만 함

## SSL/ TLS 이란?

- SSL 의 업그레이드 버전이 TLS 이다. 일반적으로 두 단어를 동일하게 사용한다.
- Secure Sockets Layer 의 약자
- 넷스케이프사에서 웹서버와 웹브라우저간의 보안을 위해 만든 프로토콜이다.
- 공개키/개인키 방식과 대칭키 방식을 혼합해서 사용한다.

### 대칭키 방식?

- 동일한 키로 암호화와 복호화를 수행하는 방식
- 그래서 암호화에 이용된 키를 가지고 있다면 해당 데이터를 쉽게 복호화 할 수 있다.
- 따라서..대칭키 방식은 암호화 복호화가 쉽다는 장점을 가지고 있다.
- 하지만 따라서 중간에 키가 해커한테 노출되면 문제가 된다. 왜냐하면 암호화->복호화 시에는 무조건 키가 배송되기 때문에..!

### 공개키/개인키 방식

- 서로 다른 키로 암호화/복호화를 수행하는 방식이다. 따라서 비대칭키라고도 불린다.
- 데이터 암호화 시에는 공개키를 사용하고, 복호화시에는 개인키를 사용한다.
- 공개키로 암호화한 데이터는 오직 개인키로만 복호화할 수 있기 때문에 누구든지 공개키를 가져도 상관없다. 공개키는 말 그대로 공개키이기 때문에 중간에 해커가 가로채가도 문제가 되지 않는다.
- 따라서 키 배송에 문제가 없다.
- 하지만 공개키 방식은 대칭키 방식보다 암호화 연산시간이 더 소요되어 비용이 더 크다.

따라서.. SSL 은 공개키 & 대칭키 기반으로 사용한다.

### SSL 은 왜 필요한가?

- 서버-브라우저간 전송되는 데이터를 외부의 공격자로부터 보안하기 위해서.
- 암호화의 대상은 내용이 유출되었을 때 악용하여 사용될수 있는 비밀정보,개인정보 등이 해당된다.

### SSL 통신 과정

- 공개키 방식으로 대칭키를 전달한다.
- 이 대칭키를 활용하여 암호화와 복호화를 하고, 서버와 브라우저간 통신을 진행한다.

## SSL 인증서의 역할

1. 클라이언트가 접속한 서버가 신뢰 할 수 있는 서버임을 보장한다.
2. SSL 통신에 사용할 공개키를 클라이언트에게 제공한다. (이 공개키는 서버가 가지고 있는 공개키!, 이 인증서 안에는 서버의 공개키가 들어있어서 클라이언트는 나중에 서버와 통신을 할 때 이 공개키를 사용하면 된다.)

### CA (Ceritificate Authority)

- 어떤 사이트가 신뢰 할 수 있는 사이트인지, 인증해주는 기업들
- SSL 을 통해서 암호화된 통신을 제공하려는 서비스는 CA 를 통해서 인증서를 구입해야한다.

### 인증서에 들어있는 정보

1. 서비스의 정보 (인증서를 발급한 CA, 서비스의 도메인 등)
2. 서버 측 공개키 (공개키의 내용, 공개키의 암호화 방법)

### 이 인증서는 어떻게 클라이언트에게 전송?

- 웹브라우저가 ssl 프로토콜로 접속하면, 해당 서비스는 내부적으로 서비스의 인증서를 브라우저에게 전송해준다.

### 그럼 인증서는 어떻게 만드나?

- CA 로 해당 인증서를 구입하면 된다.

### CA 를 브라우저는 알고 있다.

- 브라우저는 CA 리스트를 가지고 있다.

## 인증서가 서비스를 보증하는 방법

- 웹브라우저가 서버에 접속 할 때, 서버는 제일 먼저 인증서를 제공한다.
- 브라우저는 이 인증서를 발급한 CA 가 자신이 내장한 CA 리스트에 있는지 확인한다.
- 확인 결과 서버를 통해서 다운받은 인증서가 내장된 CA 리스트에 포함되어 있다면 해당 CA 의 공개키를 이용해서 인증서를 복호화 한다.
- CA 의 공개키를 이용해서 인증서를 복호화 할 수 있다는 것은, 이 인증서가 CA 의 비공개키에 의해서 암호화 된 것을 의미한다.
- 해당 CA 의 비공개키를 가지고 있는 CA 는 해당 CA 밖에 없기 때문에 서버가 제공한 인증서가 CA 에 의해서 발급된 것이라는 것을 의미한다.
- CA 의 검토를 통과했다는 것은 해당 서비스가 신뢰할 수 있다는 것을 의미한다. 이것이 CA와 브라우저가 특정 서버를 인증하는 과정이다.

## SSL 동작 방식

### 공개키 방식만을 사용하지 않은 이유?

- 공개키 방식은 컴퓨팅 파워를 많이 사용해서 사용하지 않고 공개키-대칭키를 혼합해서 사용한다.
- 따라서 성능상의 이점 & 보안상의 이점을 동시에 취하게 된다.

- 실제 데이터 : 대칭키 방식으로 암호화
- 대칭키의 키 : 공개키 방식으로 암호화
  - 대칭키 방식으로 서버와 클라이언트가 통신하기 위해서는 양쪽 다 대칭키를 공유하고 있어야한다. 이 때 대칭키를 공유 할 때 사용하는 암호화 기법으로 공개키를 사용한다.

<br/>

- 공개키 & 대칭키 혼합해서 사용
- 클라이언트와 서버가 주고받는 실제 정보는 대칭키 방식으로 암호화 하고,
- 대칭키 방식으로 암호화된 실제 정보를 복호화 할 때 사용할 대칭키는 공개키방식으로 암호화 해서 클라이언트와 서버가 주고 받는다.

## 컴퓨터와 컴퓨터가 네트워크를 이용해서 통신 할 때의 단계

> 악수 -> 전송-> 세션종료
> 이것은 은밀하게 일어나므로 사용자에게 노출되지 않는다. 이 과정에서 SSL 이 어떻게 데이터를 암호화해서 전달하는지 살펴보자!

### 악수 (handshake)

- 상호탐색이라고 생각하면 된다.
- 실제 데이터를 주고 받기 전에 클라이언트-서버는 일종의 인사를 한다.
- 이 과정을 통해서 서버,클라이언트는 서로 상대방이 존재하는지, 또 상대방과 데이터를 주고 받기 위해서 어떤 방법을 사용해야하는지 파악한다.
- SSL 방식을 이용해 핸드쉐이크를 거치는데, 이 때 가장 중요한 것은 서버의 인증서를 클라이언트에게 전송하는 것이다.

1. 클라이언트가 서버에 접속한다. Client Hello
   - 클라이언트 측에서 생성한 랜덤 데이터 전송
   - 클라이언트가 지원하는 암호 방식들을 전송
   - 세션 아이디를 전송 (이미 SSL 핸드 쉐이크를 했다면 비용과 시간을 절약하기 위해서 기존의 세션을 재활용한다. )
2. 서버는 Client Hello 에 대한 응답으로 Server Hello를 하게 된다.

   - 서버 측에서 생성한 랜덤 데이터 전송
   - 서버가 선택한 클라이언트의 암호화 방식 전송 (클라이언트가 전달한 암호화 방식 중에서 서버쪽에서도 사용 할 수 있는 암호화 방식을 선택해서 클라이언트에 전송한다. 이로써 암호화 방식에 대한 협상이 종료되고, 서버와 클라이언트는 이 암호화 방식을 이용해 정보를 교환한다.)
   - 인증서를 전송

3. 클라이언트는 서버의 인증서가 CA 에 의해서 발급된 것인지 확인하기 위해서 클라이언트에 내장된 CA 리스트를 확인한다. CA 리스트에 인증서가 없다면 사용자에게 경고메시지를 출력한다. 인증서가 CA 에 의해서 발급된 것인지를 확인하기 위해 클라이언트에 내장된 CA 의 공개키를 이용해 인증서를 복호화한다. 복호화에 성공했다면 인증서는 CA의 개인키로 암호화된 문서임이 암시적으로 보증된 것이다. 즉 인증서를 전송한 서버를 믿을 수 있게 되었다!

- 클라이언트는 1번을 통해서 받은 서버의 랜덤 데이터와 클라이언트가 생성한 랜덤데이터를 조합하여 pre master secret 이라는 키를 생성한다. 이 키는 뒤에서 살펴볼 세션 단계에서 데이터를 주고 받을 때 암호화하기 위해서 사용 된다. 이 때 사용할 암호화 기법은 대칭키이기 때문에 pre master secret 값은 제 3자에게 절대로 노출되어서는 안된다.
- 그럼 문제는 이 pre master secret 값을 어떻게 서버에 전송 할 것인가이다. 그냥 보내면..! 위험하다! 이 때 사용하는 방법이 바로 공개키 방식이다. 서버의 공개키로 pre master secret 값을 암호화 해서 서버로 전송하면 서버는 자신의 비공개키로 안전하게 복호화 할 수 있다.
- 그러면 서버의 공개키는 어떻게 구하는가..? 아까 서버로부터 받은 인증서 안에 들어있던 서버의 공개키를 사용하여 pre mastesr secret 을 암호화한다!

4. 서버는 클라이언트가 전송한 pre master secret 값을 자신의 비공개키로 복호화 한다. 이로서 서버와 클라이언트가 모두 pre master secret 값을 공유하게 된다. 그리고 서버와 클라이언트는 모두 일련의 과정을 거쳐서 pre master secret 값을 mster secret 값으로 만든다. master secret 은 session key 를 생성하는데 이 session key 값을 이용해 서버와 클라이언트는 데이터를 대칭키 방식을 암호화 한 후에 주고 받는다. 이렇게 해서 세션키를 클라이언트와 서버가 모두 공유하게 된다.

### 세션

- 세션은 실제로 서버와 클라이언트가 데이터를 주고받는 단계이다.
- 이 단계에서 핵심은 정보를 상대방에게 전송하기 전에 session key 값을 이용해 대칭키 방식으로 암호화 한다는 것이다.
- 암호화된 정보는 상대방에게 전송될 것이고, 상대방도 세션키 값을 알고 있기 때문에 암호를 복호화 할 수 있다.

<br/>
