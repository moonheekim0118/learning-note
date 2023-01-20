# RESTful API

- REST (Representational State Transfer) 는 자원을 이름으로 구분하여, 해당 자원의 상태를 주고받는 것을 의미한다. 따라서 HTTP URI 를 통해 자원을 명시하고, HTTP Method 를 통해 해당 자원에 대한 CRUD 작업을 적용하는 것을 의미한다.
- REST 를 통해서 서버와 클라이언트가 분리 될 수 있다.
  - 자원을 보유한 쪽(서버)와 자원을 이용하는 쪽(클라이언트)

### REST 의 구성

1. 자원 : URI
   - 클라이언트는 URI 를 이용하여 자원을 지정하고, 해당 자원에 대한 CRUD 조작을 서버에 요청한다.
2. 행위 : HTTP Method
   - HTTP 프로토콜의 메서드를 사용한다.
   - GET PUT POST DELETE
3. 표현
   - 클라이언트가 자원의 상태에 대한 CRUD 를 요청하면 서버는 이에 적절한 응답을 보낸다.
   - REST 에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 표현으로 나타내어 진다.
