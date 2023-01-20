## 왜 협력 프로세스를 사용하는가

1. 데이터를 공유하기 위해서
2. 속도 향상
3. 모듈화
4. 멀티태스킹

<br/>
<br/>

## IPC(Interprocess Communication)

- 프로세스 간 통신을 가능하게 하는 기술
- 여러 프로세스가 통신하여 서로 영향을 주고 받을 때 동시에 운영되는 프로세스들 간 데이터를 주고받는 과정을 어떻게 해결 할 것인가에 초점을 맞춘다.
- `공유 메모리 사용 (Shared Memory) ` 방법과 `메시지 패싱(Message Passing)` 방법으로 이 있다.

## 생산자와 소비자 문제

- IPC에서 해결해야하는 문제
- 생산자 : 정보를 생산하는 모델 ex) 웹서버
- 소비자 : 정보를 소비하는 모델 ex) 브라우저
  - ex) 브라우저가 웹서버에 정적 파일을 요청함
- 여러개의 생산자와 소비자가 있을 경우 어떻게 처리할 것인가?에 초점을 맞춘다.

<br/>
<br/>

## 1. 공유 메모리 방법 (Shared Memory)

![](https://www.softprayog.in/images/shared-memory.png)

- 서로 **공유되는 메모리**를 사용하여 데이터를 주고 받는다.
- 공유 메모리 사용 방식은 공유 메모리에 정보 저장,사용과 같은 역할을 어플리케이션 프로그래머에게 위임한다.
- 중간에 공유되는 메모리 공간 (Buffer) 을 사용하여 생산자는 Buffer에 전송하고자 하는 정보를 채우고, 소비자는 Buffer에 채워진 정보를 사용한 후 비운다.
- Buffer 사이즈가 가득 찬 상태에서, 생산자가 또 다른 정보를 전송하고자 할 때에는 `wait`상태가 된다.
- 마찬가지로 Buffer 사이즈가 0 인 상태에서, 소비자가 특정 정보를 사용하고자 할 때에는 `wait` 상태가 된다.

<br/>
<br/>

## 2. 메시지 패싱 방법 (Message Passing)

- 메시지 패싱 방법을 이용하면 공유 메모리 영역은 OS가 알아서 처리해주고, 프로그래머는 생산자와 소비자를 연결해주는 직접적인 커뮤니케이션 (링크)만 만들어서 전송해준다.
- 메시지 패싱 방법은 커널이 직접 메시지를 전달하는가에 따라 크게 두가지 커뮤니케이션 방법으로 나뉜다.

#### 1. 직접 커뮤니케이션 (Direct Communication)

- 각 프로세스가 수신자와 발신자를 정확히 안다.
- 예를 들어 A 프로세스가 B 프로세스에게 메시지를 전달하고 싶을 때, 커널에게 직접적으로 수신자 A 프로세스가 메시지를 전달한 후, 커널이 B 프로세스에게 해당 메시지를 전달하는 방식
- 프로세스 간 링크는 유일하다.

#### 2. 간접 커뮤니케이션 (Indirect Communication)

- 중간 매개체 (Port)를 이용한 커뮤니케이션 방식
- 예를 들어 A 프로세스가 B 프로세스에게 메시지를 전달 하고 싶을 때, 커널 내부 특정 포트에 메시지를 저장해놓고, B 프로세스가 해당 포트에 접근하여 메시지를 전달받는 방식
- OS 레이어는 새로운 포트 생성, 삭제, 수신, 발신의 역할을 해준다.

<br/>
<br/>

## 참고/ 이미지 출처

- [softprayog](https://www.softprayog.in/programming/interprocess-communication-using-system-v-shared-memory-in-linux)
- [prepinsta](https://prepinsta.com/wp-content/uploads/2019/01/Message-Passing-in-OS-Operating-System.png)
- [인프런 - 운영체제 공룡책 강의](https://www.inflearn.com/course/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EA%B3%B5%EB%A3%A1%EC%B1%85-%EC%A0%84%EA%B3%B5%EA%B0%95%EC%9D%98/dashboard)
- [운영체제 IPC 메시지 교환 vs 데이터 공유 프로세스간 통신](https://jhnyang.tistory.com/24)
