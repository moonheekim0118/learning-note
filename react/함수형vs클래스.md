# 📍 클래스 컴포넌트의 문제점

- 반복되는 로직
- 거대해지는 컴포넌트
- this binding 등, 고려해야 할 것들이 많아진다.
- 고정되지 않는 값 (This)

<br/>

## 함수형 컴포넌트는 렌더링 된 값을 고정시킨다.

[Untitled](https://codesandbox.io/s/pjqnl16lm7)

위의 예제에서 아래와 같은 동작을 해봅시다.

1. follow 버튼을 클릭한다.
2. 3초가 지나기 전에 Profile 이름을 수정한다.

- 함수형의 경우, 프로필의 이름이 변경되었더라도 이전의 이름을 alert 로 띄웁니다.
- 클래스의 경우, 변경된 프로필 이름을 alert 로 띄웁니다.

위 예제에서는 함수형이 올바르게 작동하고 있습니다. 사용자가 어떤 사람을 팔로우 한 후, 다른 사람의 프로필로 이동했다고 해도, 컴포넌트는 이를 헷갈려서는 안됩니다.즉, 클래스컴포넌트의 동작은 명백한 버그가 됩니다.

**그렇다면 클래스는 왜 이렇게 동작하는걸까요 ?**

```jsx
class ProfilePage extends React.Component {
  showMessage = () => {
    alert('Followed ' + this.props.user);
  };
```

- props 는 불변하지만 this 는 가변합니다.
- 따라서 요청이 진행되고 있는 상황에서 클래스 컴포넌트가 리렌더링 된다면, this.props 또한 변경됩니다. 따라서 showMessage의 this.props 가 새로운 props 를 읽어들이는 것입니다.

**그렇다면 함수형 컴포넌트에서는 왜 잘 동작할까요?**

- 바로 props 를 인자로 받아오기 때문입니다.
- 클래스의 this 와 다르게, 함수가 받는 인자는 리액트가 변경할 수 없습니다.
- 즉, 함수형 컴포넌트는 렌더링 된 값을 고정시킵니다.

**그렇다면, 만약 함수형에서 렌더시의 값이 아니라 최근의 값을 가져오고 싶다면 어떻게 할까요?**

- ref 를 사용 할 수 있습니다.

<br/>
<br/>

# 참고자료

https://overreacted.io/ko/how-are-function-components-different-from-classes/
