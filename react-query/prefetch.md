# prefetching 사용하기

말그대로 ‘미리’ fetch 해놓은다는건데..어디에 사용 할 수 있을까?

- pagination 에서 page 가 바뀔 때

```tsx
useEffect(() => {
  if (currentPage < maxPostPage) {
    let nextPage = currentPage + 1;
    queryClient.prefetchQuery(["posts", nextPage], () => {
      fetchPosts(nextPage);
    });
  }
}, [currentPage, useQueryClient]);
```

이런식으로 하면..다음 페이지에 가는동안 로딩상태가 없어짐! 사용자 경험이 좋아질 것 같다.

- 그러니까 어떤 컨텐츠를 다시 Fetch 해옴이 명확 할 때 prefetch 를 사용하면 loading 상태를 없앨 수 있어서 좋은 사용자 경험을 구현 할 수 있다!
- 그러나 언제 써야할지는 잘 고민해야할듯. 무분별하게 사용하면 불필요한 서버요청이 증가할것같다.
  - 만약 해당 컨텐츠를 불러와야하는 상황이 아님에도 prefetch 를 남발하면?
- SSR 시에도 사용하는 것 같다… 더 알아봐야할듯?!
