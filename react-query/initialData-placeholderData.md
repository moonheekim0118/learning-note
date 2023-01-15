# placeholder data vs initialData

출처 - [https://tkdodo.eu/blog/placeholder-and-initial-data-in-react-query](https://tkdodo.eu/blog/placeholder-and-initial-data-in-react-query)
​

- 둘 다 동기적으로 사용할 수 있는 데이터로 캐시를 미리 채우는 방법을 제공
- 즉, 이 중 하나가 제공되면 쿼리가 로드 상태가 아니라 성공 상태로 직접 이동한다는 의미
- 캐시에 이미 데이터가 있는 경우 둘 다 효과가 없음
  ​

### Observer level

- 리액트 쿼리의 관찰자는 일반적으로 하나의 캐시 항목에 대해 생성된 구독이다.
- 관찰자는 캐시 항목의 변경사항을 관찰하고, 변경 사항이 있을 때마다 알림을 받는다.
- 관찰자를 만드는 기본 방법은 useQuery 를 호출하는 것.
- 관찰자 수준에서 작동하는 일부 옵션은 select 또는 keepPreviousData
- select가 data transformation에 매우 유용한 이유는, 동일한 캐시 항목을 관찰하면서, 다른 컴포넌트에서 데이터의 다른 조각을 구독하는 기능
  ​
  **InitialData는 캐시 수준에서 작동하는 반면 placeholderData는 관찰자 수준에서 작동한다.**
  ​
- initialData는 캐시에 유지
- 캐시 수준에서 작동하기 때문에 하나의 initialData만 있을 수 있으며,해당 데이터는 캐시 항목이 생성되는 즉시(즉, 첫 번째 관찰자가 마운트될 때) 캐시에 저장
- placeholderData 는 캐시에 유지되지 않는다. 해당 데이터는 서버 데이터와 관련없는 보여주기용 가짜 데이터임이 명백하다.
- React Query는 실제 데이터를 가져오는 동안 해당 데이터를 표시할 수 있도록 해준다.
- 관찰자 수준에서 작동하기 때문에 이론적으로 다른 컴포넌트에 대해 다른 placeholderData를 가질 수 있다.
