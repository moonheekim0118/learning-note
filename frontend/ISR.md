# Incremental Static Regeneration (증분 정적 페이지 생성)

- Next.js 에서 정적 페이지를 빌드 한 후, 업데이트 할 수 있게 해준다.
- 전체 사이트를 리빌드 할 필요 없이, 각 페이지별로 ISR 을 적용 할 수 있다.
- ISR 을 사용하기 위해서는 getStaticProps 함수의 revalidation 옵션을 사용하면 된다.
  - 따라서 해당 revalidation 옵션에 따라서 캐시(정적페이지)를 검증하고 stale 하다고 판단되면 next.js 가 현재 캐시된 페이지를 보여주는 동안, 백그라운드에서 정적 페이지를 재생성한다 (SWR)
  - 새로운 페이지가 생성되면, next.js 는 캐시를 무효화하고, 업데이트 된 페이지를 보여준다. 만약 새로운 페이지가 빌드되지 않을 경우 이전의 페이지(캐싱된 페이지)를 보여준다.

https://nextjs.org/docs/basic-features/data-fetching/incremental-static-regeneration
