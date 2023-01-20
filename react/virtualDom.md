리액트는 실제로 DOM 을 제어하는 방식이 아니라 중간의 가상 DOM, 즉 Virtual DOM 을 두어 개발의 편의성 (DOM 을 직접 제어하지 않는다)과 성능 (배치 처리로 DOM 변경) 을 개선했습니다.

# 📍 Virtual DOM 이란

- 특정 기술이라기 보다는 아래와 같은 패턴에 가깝습니다.
- UI 의 가상 표현을 메모리에 저장 한 후 → React DOM 과 같은 라이브러리로 실제 DOM 과 동기화 합니다. _( 이러한 과정을 **재조정(Reconciliation)** 이라고 합니다. )_
- 즉 DOM 에 실제 변경사항을 바로 반영하는 것이 아니라, **Virtual DOM 에 변경 사항을 먼저 저장한 후, 이전과 비교 하여 실제로 변경이 일어난 부분만 실제 DOM 에 적용하는 것** 입니다.

<br/>
<br/>

# 📍 Virtual DOM 을 사용하는 이유

## 개발의 편의성

- 재조정에 의해 리액트의 *선언적 방식*을 가능하게 합니다. 리액트에게 원하는 UI 상태를 알려주면 DOM 이 그와 일치하도록 만듭니다.
- 따라서 어트리뷰트 조작, 이벤트 처리, 수동 DOM 업데이트와 같은 작업들이 추상화 됩니다.
- 왜 재조정이 선언적 방식을 가능하게 하는걸까요?
  - 선언적 방식이란 ? 필요한 것을 달성하는 과정을 하나 하나 기술하는 것(명령)이 아니라, 필요한 것이 어떤 것인지 기술하는 것입니다.
  - 재조정 과정이 없다면, DOM 의 변경사항들을 일일이 직접 명령해주어야 합니다. 우리는 V-DOM 을 이용한 재조정 과정을 통해서 이러한 ‘명령’을 할 필요가 없어졌습니다.

<br/>

## 성능

브라우저 렌더링 과정을 살펴보면 아래와 같습니다.

1. DOM tree 생성 : 렌더 엔진이 HTML 을 파싱하여 DOM 노드로 이루어진 트리를 생성한다.
2. Render tree 생성 : CSS 파일과 inline 스타일을 파싱하여 DOM+CSSOM = 렌더트리 생성
3. Layout (reflow) : 각 노드들의 스크린에서의 좌표에 따라 위치를 결정한다.
4. Paint (repaint) : 실제 화면에 그린다.

_DOM 요소에 변화가 발생 할 때마다 우리는 렌더트리를 다시 그림으로써 Render Tree 생성 → Reflow → Repaint 과정을 반복합니다. VDom 은 이러한 성능의 문제를 해결해줍니다._

- 데이터 변경 시 전체 UI 는 일단 **Virtual DOM 에 먼저 반영** 됩니다. 이전 Virtual DOM 에 있던내용과 update 후의 내용을 **비교**하여 **바뀐 부분만 실제 DOM 에 적용**합니다. 아래 설명을 통해서 자세히 살펴봅시다.

- React 의 JSX 를 컴포넌트에서 Return 하면 바벨은 JSX 를 React.createElement() 호출로 컴파일 합니다. 실제 바벨에서 JSX 를 호출하면 JSX 가 객체 형태의 React Element 로 변환됩니다.
- React Element 는 DOM 요소의 가상 버전으로 , 가볍고(light), 상태를 가지지 않으며(stateless),불변성 (immutable) 을 유지합니다. 이러한 React Element 는 ReactDOM.render 에 의해서 실제 DOM 요소로 렌더됩니다.
- 하지만 React Element 는 불변성(immutable)을 가지기 때문에, 즉 변경이 불가능 하기 때문에 한번 요소를 만들었다면 데이터를 변경하기 위해서 그 자식이나 속성을 변경 할 수 없습니다.

```jsx
// before
function SomeComponent(){
	return(
		<div>
				<div>우테코</div>
				<Poco/>
		<div>
	)
}
```

```jsx
// after
function SomeComponent(){
	return(
		<div>
				<div>우테코</div>
				<Jun/>
		<div>
	)
}
```

- 위 예시에서 SomeComponent 의 바뀐 부분은 Poco → Jun 밖에 없는데, React Element 로 만들어진 SomeComponent 의 자식속성만 변경 할 수 없으니 다시 전체 컴포넌트의 React Element를 새로 생성하여 ReactDOM.render 로 전송하는 수밖에 없습니다.
- 이러한 문제점을 해결하기 위해 리액트는 Virtual DOM 을 이용하는 것입니다. 모든 React DOM object 는 그에 대응하는 Virtual DOM object 가 있습니다. 그리고 V-DOM object 는 각각의 React DOM object 에 맵핑됩니다.
- 데이터가 업데이트 되면, 바뀐 데이터를 기반으로 React.createElement 를 통해 JSX Element 를 렌더링 하고, 이 때 모든 Virtual DOM object 가 업데이트 됩니다. 이 때 Virtual DOM 이 업데이트 되면, 리액트는 업데이트 이전의 Virtual DOM 의 스냅샷과 비교하여 정확히 어떤 Virtual DOM 이 바뀌었는지 추적합니다. (Diffing 알고리즘)
  - _Element 의 속성만 변경 된 경우 ? 속성 값만 업데이트_
  - _Element 의 태그 혹은 컴포넌트가 변경된 경우 ? 해당 노드를 포함한 하위 모든 노드를 언마운트 후, 새로운 Virtual DOM 으로 대체_
- **이 후 변경된 부분만 실제 DOM 에 적용하게 됩니다.**

<br/>
<br/>

# 📍 Virtual DOM이 무조건 빠를까?

- 답은 NO
- 정보 제공만하는 어플리케이션 (ex 위키피디아) 이라면 아무런 인터렉션이 일어나지 않기 때문에, DOM 트리의 변화가 일어나지 않아 일반 DOM 의 성능이 더 좋을 수도 있습니다.

<br/>
<br/>
