# IPC 통신 방법 (Socket과 RPC)

## 1. Socket

![](https://media.geeksforgeeks.org/wp-content/uploads/20200509144309/1406-4.png)

- 통신을 위한 양종단 (endpoints)을 의미하며, 파이프 형태의 연결이다.
- A 컴퓨터와 B 컴퓨터를 연결 할 때, 각 컴퓨터를 특정하는 것이 **IP 주소**이고 A컴퓨터와 B컴퓨터를 연결하는 파이프를 특정한 것이 **Port** 이며, 이 IP 주소와 Port를 하나로 묶어서 특정한 것이 **소켓**이다.
- 하지만, 원격지에 있는 컴퓨터와 bit가 다르다면 소켓을 일일이 지정해줘야하는 문제점이 있다.

<br/>

<br/>

## 2. RPC (Remote Procedure Calls)

![](https://media.geeksforgeeks.org/wp-content/uploads/operating-system-remote-procedure-call-1.png)

- 연결된 컴퓨터에 있는 프로세스 간의 원격 호출을 추상화한 것을 RPC 라고 한다.
- 원격 프로세스 간 통신 기능을 쉽게 구현할 수 있어서, 분산 처리 환경에서 주로 사용된다.
  - 분산 처리 환경 : 네트워크 상 여러 요소들을 하나의 시스템처럼 활용 가능한 환경
- 클라이언트에서 서버의 프로시저를 호출하는 기능 제공
- 원격에 있는 프로그램을 로컬에 있는 것 처럼 사용할 수 있다.
  - 다시 말해서, 연결된 시스템간의 관계가 너무 돈독해지며 독립적인 REST 방식보다 CRUD에 있어서 신속하지 못한 단점으로 작용한다.
    <br/>
    <br/>

### RPC 과정

![복](https://media.geeksforgeeks.org/wp-content/uploads/operating-system-remote-call-procedure-working.png)

1. 클라이언트가 클라이언트 스텁 프로시저를 작동시키고, 파라미터를 전송한다
2. 클라이언트 스텁이 메세지에 파라미터를 `Marshall (pack)` 한다.
   - Marshall : 파라미터 값을 표준화 된 형식으로 변환시키고, 각 파라미터를 메시지에 복사하는 과정
3. 클라이언트 스텁이 메시지를 전송 계층에 넘겨준다. 전송계층은 해당 메시지를 원격 서버 기계에 보낸다.
4. 서버 측에서 전송 계층이 받아온 메시지를 서버 스텁에 넘겨준다. 이 때 서버 스텁은 메시지를 `deMarshall (unpack)` 한다.
5. 서버 프로시저가 종료되면, 서버 스텁을 반환하고 서버 스텁은 반환 값을 Marshall 하여 메시지에 담는다. 그리고 이 메세지를 전송 계층에 전달한다.
6. 전송 계층은 반환 값을 다시 클라이언트 측 전송 계층에 전달하고 , 클라이언트 측 전송 계츠은 ㅂ받은 메시지를 클라이언트 스텁에 전달한다.
7. 클라이언트 스텁은 받아온 반환 파라미터값을 demashall 하고, 실행한다.

<br/>
<br/>

### 헷갈리는 점

1. 프로시저와 함수의 차이
   - 함수 : 특정 값을 계산하며 리턴 값이 있다. 함수는 기능을 통해서 **어떠한 결과를 수행하는 것을 목적**으로 한다.
   - 프로시저 : 특정 작업을 수행하며 리턴 값이 없다. 리턴 값이 없기 때문에 **수행하는 절차 그 자체를 목적**으로 한다.
2. 클라이언트 스텁과 서버 스텁
   - 클라이언트 스텁은 메인 프로그램에 의해 호출되어 프로시저 역할과 파라미터를 전송하는 역할
   - 서버 스텁은 데이터를 받고 로컬에 지정된 프로시저를 호출하는 역할
3. Marshalling
   - 하나의 언어로 작성된 프로그램의 출력 파라미터를 다른 언어로 작성된 프로그램의 입력값으로 전달 할 때 필요하다.
   - 즉 표준화된 형태로 인코딩(XDR)

<br/>
<br/>

## 참고/ 이미지 출처

- [Geeks for Geeks - Socket in Computer Network](https://www.geeksforgeeks.org/socket-in-computer-network/)

- [Geeks for Geeks - Remote Procedure Call (RPC) in Operating System ](https://www.geeksforgeeks.org/remote-procedure-call-rpc-in-operating-system/)

- [프로시저와 함수의 차이](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=jyh0841&logNo=220332324511)

- [분산처리 시스템 part 3](https://myondal.tistory.com/33)
- [인프런 - 운영체제 공룡책 강의](https://www.inflearn.com/course/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EA%B3%B5%EB%A3%A1%EC%B1%85-%EC%A0%84%EA%B3%B5%EA%B0%95%EC%9D%98/dashboard)
