## 1. SOP (Same Origin Policy)

다른 출처의 리소스를 사용하는 것을 제한하는 보안 방식이다.

> 출처란 ?
> URL의 Protocol, Host, Port이 같다면 같은 출처라고 판단 할 수 있다.
> 다만 IE 브라우저의 경우 Port는 출처 판단에 포함하지 않는다.

### 왜 SOP가 필요한가?

**보안상 위협이 되는 악의적인 요청을 막기 위해서**이다. 이에 따라 아무나 서버에 요청을 보낼 수 없도록 한다.

<br/><br/>

## 2. CORS (Cross-Origin Resource Sharing)

위와 같은 SOP 보안 방식에서 다른 출처의 자원을 공유해야는 체제이다.
즉, 추가 HTTP 헤더를 사용하여 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 자원에 접근 할 수 있는 권한을 부여하도록 **브라우저에 알려주는 체제**이다.

<br/>
<br/>

## 3. CORS 접근제어 시나리오

### 단순 요청 (Simple Request)

**바로 본 요청을 보내며**, 아래와 같은 조건을 만족해야만 단순 요청을 할 수 있다.

1. GET, POST, HEAD 메서드 중 하나여야 한다.
2. 헤더는 Accept, Accept-Language, Content-Language, Content-Type만 허용한다.
3. Content-Type이 아래 중 하나여야 한다.

- application/x-www-form-urlencoded
- multipart/form-data
- text/plain

#### 문제점

![](https://images.velog.io/images/moonheekim0118/post/f2fe0b35-b11d-430b-9725-ca100c4d3a6a/%E1%84%8F%E1%85%B3%E1%84%85%E1%85%A9%E1%84%89%E1%85%B3%E1%84%8B%E1%85%A9%E1%84%85%E1%85%B5%E1%84%8C%E1%85%B5%E1%86%AB.jpeg)
CORS 에러는 결국 브라우저가 판단하므로, **서버는 CORS에 대해 모를 수 있다**. 따라서 만약 CORS 처리가 되지 않은 서버에 허용되지 않은 클라이언트가 DB를 수정을 요청을 바로 할 경우 서버는 이미 요청을 수행하게 되고, 해당 응답을 클라이언트에 전달하는 과정에서 브라우저가 CORS 에러를 띄우게 된다.

이러한 문제점을 방지하기 위한 것이 **프리플라이트 요청**이다.

<br/> <br/>

### 프리플라이트 요청 (Preflight Request)

본 요청을 보내기 전, 서버에 먼저 OPTIONS 메서드를 통해 다른 도메인의 리소스에 요청이 가능한지 확인한다.
이 후 요청이 가능하다면 본 요청을 보낸다.

#### 프리플라이트 요청 헤더

1. Origin : 요청 출처
2. Access-Control-Request-Method: 실제 요청 메소드
3. Access-Control-Request-Headers: 실제 요청의 추가 헤더

#### 프리플라이트 응답

1. Access-Control-Allow-Origin: 서버 측 허가 출처
2. Access-Control-Allow-Methods: 서버 측 허가 메서드
3. Access-Control-Allow-Headers: 서버 측 허가 헤더
4. Access-Control-Max-Age: 프리플라이트 응답 캐시 기간
   - 모든 요청마다 프리플라이트 응답을 요청하는 것은 비효율적이므로, 응답을 일정 기간동안 캐싱해놓는다.

<br/> <br/>

### 인증정보 포함 요청 (Credentialed Request)

인증 관련 헤더를 포함할 때 사용하는 요청이다.
클라이언트 측에서 쿠키나 JWT를 포함하여 서버에 요청을 보내고 싶을 때 사용하게 된다.

#### 클라이언트 측

- credentials : include

#### 서버 측

- Access-Control-Allow-Credentials: true

<br/><br/>

## 3. CORS 해결 방법

### 프론트 프록시 서버 설정

만약 프론트 서버의 출처가 localhost:8000이고, 백엔드 서버의 출처가 localhost:9000일 때 프론트 측에서 api로 보내는 요청은 출처를 localhost:9000(서버 측 출처)으로 바꾸어서 보내는 방법이다.

- 웹팩에서 DevServer 설정을 통해 프록시서버를 설정할 수 있다.

```javascript
// webpack.config.js
module.exports = {
  devServer: {
    proxy: {
      '/api': 서버측 출처
    }
  }
};
```

### 헤더 설정

> 서버 측 헤더를 직접 설정해주는 방법이 있다.

```javascript
Access-Control-Allow-Origin: 프론트 출처
```

<br/>
<br/>
