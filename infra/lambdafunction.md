## CloudFront 의 Lambda Function이란?

- Lambda@Edge 라고 불린다.
  - 버지니아 리전에 생성하는 Lambda 함수가 하나 있음
  - cloudfront 의 지역 단위인 edge location 들이 있고, 요것들은 버지니아 lambda 함수를 복제하여 각 edge location에 배포한다.
  - 클라이언트들은 cloudfront edge location에 요청한다.
- 즉 Lmbda@Edge라고 불리는 이유는, 버지니아 lambda 함수를 복제하여 cloudfront의 각 ege location에 전역으로 배포하기 때문이다.
  - 클라이언트는 어떤 리전에서 요청하던지 간에, edge location에 배포된 Lambda@edge 함수를 거쳐 응답받음

### 람다 펑션으로 할 수 있는 것

(이런식으로도 사용할 수 있다니!)

- 이미지 리사이징
  - 썸네일용 이미지, 큰 이미지 등등을 이미지 서버에 다 가지고 있기에 무리가 있음 (용량부족)
  - 따라서 이미지를 크기별로 저장하는게 아니라, 하나의 사이즈만 가지고 있고 (아마 젤 큰 사이즈) 요 람다 펑션으로 이미지 리사이징을 해준다.
- [[트러블슈팅기 CSR에서 동적 OG 메타태그 적용하기]] 요 포스팅에서도 보았듯이, CSR 앱의 동적 메타태그 삽입에도 사용이 가능하당

https://devhaks.github.io/2019/08/25/aws-lambda-image-resizing/
