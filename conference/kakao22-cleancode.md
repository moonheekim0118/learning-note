# 섬세한 ISFP의 코드 가독성 개선 경험

https://www.youtube.com/embed/emGLxi0LvNI
​

- 정확한 단어 고르기
- 잘 보이는 형태로
  ​

## 정확한 단어 고르기

### 다른 뜻을 가진 단어와 비교하기

- load vs fetch - load 는 가져와서 싣다. (완결) - fetch 는 가져오다.
  ​

```js
const data = await loadData();
​
const data = await fetchData();
const success = await loadData();
```

​

### isLoading vs isFetching

- isLoading 은 데이터가 없을 때, 최초 한번만 바뀐다.
- isFetching 은 데이터를 다시 불러올 때에도 바뀐다.
  ​

### query ? Get ?

- get : 가져오다 ( 결과를 당연히 가져올 것으로 기대)
- query : 질문하다. (결과가 없을 수도 있음)
- get 은 결과가 없으면 Error, query 는 결과가 없으면 null
  ​

## UI 컴포넌트

- Card : 하나의 주제로 묶인 컨텐츠, 액션
- Box: 내용물을 감싸는 Wrapper
  ​

# 보다 구체적인 단어로 바꾸기

```js​
if(exprationTime < PROMOTION_END_TIME) {
    return remainTime / totalTime;
}
​
// 개선
if(exprationDate < PROMOTION_END_DATE) {
    return remainDuration / totalDuration;
}
```

- get (가져오다)
  - extract 추출하다
  - parse 분해하다
  - aggregate 합치다.
- number 숫자
  - limit 제한이 되는 수
  - count 총계
- change 변경하다.
  - convert 변환하다.
  - filter 거르다
  - override 덮어쓰다.
- changed 바뀐
  - dirty 더러운 = 수정이 이루어진
- 항상 정확할 필요는 없다. 문맥에 맞춰서 오히려 부정확한게 더 가독성에 좋을 수 있음
  ​

## 잘보이는 형태로 작성해보기

- 상수 사용은 책의 목차같은 느낌이다. 앱애서 사용되는 특정 값들을 한 곳에서 관리할 수 있기때문에!
- 로그 전송과 같은 것들을 모든 엘리먼트에 담는게 아니라 전체를 high order 컴포넌트로 감싸고, data-attribute 를 사용할수도 있다. (이벤트 전파 이용)
  ​

## 생각

- 좋은 네이밍은 그 자체로 좋은 추상화의 역할을 해준다고 생각한다.
- 결국 코딩은 글쓰기랑 매우매우 닮아있는 것 같다.
- 네이밍 어려워하는 사람들에게 정말 유용할듯
