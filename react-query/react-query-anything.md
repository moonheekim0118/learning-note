- tkdodo 블로그 공부기록

## 커스텀 훅 장점

- UI에서 실제 데이터를 가져오지만 useQuery 호출과 같은 위치에 배치할 수 있습니다.
- 하나의 Query key(그리고 잠재적으로 타입을 정의한)를 하나의 파일에 유지할 수 있습니다.
- 일부 설정을 변경하거나 데이터 변환을 추가해야 하는 경우 한 곳에서 수행할 수 있습니다.

## 구조분해할당 하지 않기

우선, data 나 error와 같은 이름은 이름을 바꿀 가능성이 높다. 어떤 데이터인지, 어디에서 오류가 발생했는지 해당 객체에 컨텍스트가 유지된다. 또한 상태 필드 또는 상태 플래그(boolean) 중 하나를 사용할 때 TypeScript가 타입을 좁히는 데 도움이 된다. 이러한 작업은 구조분해할당 할 시 사용 할 수 없다.

```
const { data, isSuccess } = useGroups()
if (isSuccess) {
  // 🚨 data will still be `Group[] | undefined` here
}

const groupsQuery = useGroups()
if (groupsQuery.isSuccess) {
  // ✅ groupsQuery.data will now be `Group[]`
}
```

## 쿼리키 팩토리 만들기

## Use Query Key factories

- 일반적으로 쿼리키를 선언하면 이는 오류가 발생하기 쉬울 뿐만 아니라 키에 다른 수준의 세분화를 추가하려는 경우처럼 향후 변경 작업을 더욱 어렵게 만듦
- 함수당 하나의 Query Key factory를 추천한다.
- etries and functions이 있는 간단한 객체일 뿐이며 쿼리 키를 생성하고, 이를 Custom Hook에서 사용할 수 있기 때문.

```jsx
const todoKeys = {
  all: ['todos'] as const,
  lists: () => [...todoKeys.all, 'list'] as const,
  list: (filters: string) => [...todoKeys.lists(), { filters }] as const,
  details: () => [...todoKeys.all, 'detail'] as const,
  detail: (id: number) => [...todoKeys.details(), id] as const,
}
```

- 따라서 각 레벨은 다른 레벨 위에 구축되지만 독립적으로 액세스할 수 있으므로 유연성이 높다.

```jsx
// 🕺 remove everything related to the todos feature
queryClient.removeQueries(todoKeys.all);

// 🚀 invalidate all the lists
queryClient.invalidateQueries(todoKeys.lists());

// 🙌 prefetch a single todo
queryClient.prefetchQueries(todoKeys.detail(id), () => fetchTodo(id));
```

## queryKey 와 상태의 종속성 비동기화 문제

```jsx
export const useTodos = () => {
  const { state, sorting } = useTodoParams();

  // 🚨 can you spot the mistake ⬇️
  return useQuery(["todos", state], () => fetchTodos(state, sorting));
};
```

- queryKey는 실제 의존성과 동기화되지 않았으며, 이에 대해 오류를 나타내는 빨간 줄은 없다.

### 해결 - QueryFunctionContext 사용하기

- QueryFunctionContext는 queryFn에 인수로 전달되는 객체

```
// this is the QueryFunctionContext ⬇️
const fetchProjects = ({ pageParam = 0 }) =>
  fetch('/api/projects?cursor=' + pageParam)

useInfiniteQuery('projects', fetchProjects, {
  getNextPageParam: (lastPage) => lastPage.nextCursor,
})
```

- 그러나 컨텍스트에는 이 쿼리에 사용되는 queryKey도 포함되어 있다. 즉, React Query에 의해 제공된다.

```jsx
const fetchTodos = async ({ queryKey }) => {
  // 🚀 we can get all params from the queryKey
  const [, state, sorting] = queryKey;
  const response = await axios.get(`todos/${state}?sorting=${sorting}`);
  return response.data;
};

export const useTodos = () => {
  const { state, sorting } = useTodoParams();

  // ✅ no need to pass parameters manually
  return useQuery(["todos", state, sorting], fetchTodos);
};
```
