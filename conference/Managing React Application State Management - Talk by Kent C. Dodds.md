# [참고영상](https://www.youtube.com/watch?v=zpUMRsAO6-Y)

# [참고슬라이드](https://github.com/kentcdodds/managing-state-management-slides)

### 두 가지 상태

1. 서버 캐시

- 서버에 저장되어 있는 정보이며, 이를 빠르게 사용자에게 보여주기 위해서 클라이언트 사이드에 상태로서 캐싱해놓는다.
- 매번 백엔드로 요청을 보내는 대신, 백엔드와 프론트엔드 사이에 캐시라는 레이어를 두어서 성능상 문제를 해결하는 것.

2. UI 상태

- 프론트엔드에만 저장되어있는 상태.
- 페이지 새로고침시 모두 사라지는 상태.

이 두가지 상태는 다르게 처리되어야 한다.
서버 캐시는 리액트 쿼리, 리코일 같은 상태관리 라이브러리에서 핸들링하고, 리액트에서는 UI 상태만 다루도록 하자.

## UI 상태

- 모든걸 전역으로 둔다면 결국 App (최상위컴포넌트)에서 관리하는게 기하급수적으로 늘 수 밖에 없다. (Prop Drilling)
- 그러면 어떻게 해결해야할까?

### 합성 이용하기

```jsx
function App() {
  const [someState, setSomeState] = React.useState("some state");
  return (
    <>
      <Header
        logo={<Logo someState={someState} />}
        settings={<Settings onStateChange={setSomeState} />}
      />
      <LeftNav>
        <SomeLink someState={someState} />
        <SomeOtherLink someState={someState} />
        <Etc someState={someState} />
      </LeftNav>
      {/* ... */}
    </>
  );
}
```

만약…합성이 충분하지 않다면 Context 를 사용하세용

합성 관련 영상
[YouTube](https://www.youtube.com/watch?v=3XaXKiXtNjw)

Context api 관련 글
[How to use React Context effectively](https://kentcdodds.com/blog/how-to-use-react-context-effectively)

### Context

```jsx
const CountContext = React.createContext()

function Counter() {
  const {count, increment} = React.useContext(CountContext)
  return <button onClick={onIncrementClick}>{count}</button>
}

function CountDisplay() {
  const {count} = React.useContext(CountContext)
  return <div>The current counter count is {count}</div>
}

function App() {
  const [count, setCount] = React.useState(0)
  const increment = () => setCount(c => c + 1)
  return (
    <CountContext.Provider value={{count, increment}}>
      <div>
        <CountDisplay />
        <Counter />
      </div>
    </CountContext.Provider>
  )

```

## Colocate States

- 글로벌에 모든 상태를 놓는다면…

```jsx
function App() {
  return (
    <UserProvider username={username}>
      <NotificationsProvider>
        <ThemeProvider>
          <AuthenticationProvider>
            <Router>
              <HomeScreen path="/" />
              <AboutScreen path="/about" />
              <UserScreen path="/:userId" />
              <UserSettingsScreen path="/settings" />
              <NotificationsScreen path="/notifications" />
            </Router>
          </AuthenticationProvider>
        </ThemeProvider>
      </NotificationsProvider>
    </UserProvider>
  );
}
```

- 위와 같은 컴포넌트 구조라면 아래와 같은 파일 구조를 갖게된다.

```jsx
my-cool-app
└── src
    ├── index.js
    ├── providers
    │   ├── auth.js
    │   ├── notifications.js
    │   ├── theme.js
    │   ├── user.js
    │   └── ...etc
    ├── screens
    │   ├── about.js
    │   ├── home.js
    │   ├── notifications
    │   │   ├── index.js
    │   │   ├── list.js
    │   │   ├── tab.js
    │   │   └── type-list.js
    │   ├── settings.js
    │   └── user
    │       ├── activity.js
    │       ├── index.js
    │       ├── info.js
    │       └── nav.js
    └── utils
        └── ...etc
```

- 문제점 : Notification Provider 는 notification 컴포넌트에서만 쓰는데 해당 로직을 수정하기 위해서는 각 폴더를 널뛰기 해야함…

- 문제점 2: 자바스크립트 파일을 로드 할 때.. 사용자에게 Notification 컴포넌트가 보이기 전이나 Setting 컴포넌트가 보이기도 전에 provider 관련 코드가 로드되면서 불필요한 로딩이 생겨버린다. -> 코드 스플릿팅 불가능

그래서 아래와 같이 colocate 하자!

```jsx
function App() {
  return (
    <ThemeProvider>
      <AuthenticationProvider>
        <Router>
          <HomeScreen path="/" />
          <AboutScreen path="/about" />
          <UserScreen path="/:userId" />
          <UserSettingsScreen path="/settings" />
          <NotificationsScreen path="/notifications" />
        </Router>
      </AuthenticationProvider>
    </ThemeProvider>
  );
}

function NotificationsScreen() {
  return (
    <NotificationsProvider>
      <NotificationsTab />
      <NotificationsTypeList />
      <NotificationsList />
    </NotificationsProvider>
  );
}

function UserScreen({ username }) {
  return (
    <UserProvider username={username}>
      <UserInfo />
      <UserNav />
      <UserActivity />
    </UserProvider>
  );
}
```

```jsx
my-cooler-app
└── src
    ├── index.js
    ├── providers
    │   ├── auth.js
    │   ├── theme.js
    │   └── ...etc
    ├── screens
    │   ├── about.js
    │   ├── home.js
    │   ├── notifications
    │   │   ├── index.js
    │   │   ├── list.js
    │   │   ├── provider.js
    │   │   ├── tab.js
    │   │   └── type-list.js
    │   ├── settings.js
    │   └── user
    │       ├── activity.js
    │       ├── index.js
    │       ├── info.js
    │       ├── nav.js
    │       └── provider.js
    └── utils
        └── ...etc
```
