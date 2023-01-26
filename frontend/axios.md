## interceptor 란

- Axios는 HTTP 요청과 응답을 가로채는 Interceptor를 지원한다.
- Axios 인스턴스는 요청과 응답에 대해 각각 Interceptor 관리자를 가지고 있고, 이 관리자들은 요청이나 응답을 가로챌 때 실행할 핸들러를 관리한다.
- 따라서, 실행하고자 하는 핸들러를 Interceptor 관리자에 등록해두면, `Axios 인스턴스가 요청을 보내기 직전`과 `응답을 받은 직후`에 미리 등록한 핸들러들을 차례로 실행한다.

### 언제 쓰일 수 있을까?

- 요청 시, 어떠한 핸들링을 해줘야 할 때.
- 실패 시 재요청하기.
- 인증인가 처리 할 때, `인증에 실패->리프레시 토큰이 있을 경우 해당 리프레시 토큰으로 재요청` 로직을 구현 할 때
- 그러니까, 리액트 쿼리를 사용한 `Error Boundary` 나 `전역적인 onError 처리`는 `API 요청에 따른 에러 상황을 보여주기 위한 UI 핸들링`으로만 사용하고, Axios Interceptor 는 그 외의, API 요청별 전/후 로직 처리를 할 때 용이 할 것 같다.

## Axios Cancel Token

- Axios 인스턴스는 요청을 취소 할 수 있는 cancel token 을 갖는다.

### 언제 쓰일 수 있을까?

- 하나의 페이지에 여러 api 요청이 있고, 만약 첫 api 요청이 실패했을경우 나머지 api 요청을 취소시켜야 할 때 , cancel token 을 저장해두고, interceptor에서 api cancel 을 진행 할 수 있을 것 같다.
