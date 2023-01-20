# this 란 무엇인가요?

- This 는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수 (self-referencing variable) 입니다. 따라서 this 를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조 할 수 있게 됩니다.
- This 는 실제로 함수 호출 시점(런타임)에 결정되며, 무엇을 가리킬지는 전적으로 함수를 호출한 코드에 달려있습니다.

즉
This 는 함수 자체를 가리키거나, 함수의 렉시컬 스코프를 가리키지 않습니다.
This 는 함수 호출 방식에 따라서 동적으로 결정되기 때문에, 함수 선언 시점에는 this 가 무엇일지 알 수 없습니다.

# 자바스크립트에서 this 는 왜 필요할까요?

this 는 자바스크립트에서 '호출 주체'를 찾기 위해서 필요하다고 생각합니다.

```js
function identify() {
  return this.name;
}

function speak() {
  const greeting = `안녕 나는 ${identify.call(this)}`;
  console.log(greeting);
}

const coach1 = {
  name: "포비",
};

const coach2 = {
  name: "공원",
};

speak.call(coach1); // 안녕 나는 포비
speak.call(coach2); // 안녕 나는 공원
```

위와 같은 코드에서 this 가 없다면 일일이 context 를 파라미터로 넘겨줘야 합니다.

```js
function identify(context){
  return context.name;
}

function speak(context){
  const greeting = `안녕 나는 ${identify(context)}`;
  console.log(greeting);
}

const coach1 = {
  name: "포비";
}

const coach2 = {
  name: "공원";
}

speak(coach1); // 안녕 나는 포비
speak(coach2); // 안녕 나는 공원
```

즉 this 를 통해서 함수가 적절하게 현재 실행중인 객체를 자동으로 참조하게 됩니다.

## this 결정 방법

## 기본 바인딩

- 기본바인딩은 아무것도 하지 않았을 때 전역객체가 바인딩되는 것을 의미합니다.

## 암시적 바인딩

`.` 을 통해서 호출부 객체에 따라서 바인딩됩니다.

### 명시적 바인딩

`call, apply, bind` 를 통해서 명시적으로 자바스크립트에게 직접 this 바인딩을 명시해줄 수 있습니다.

## new 바인딩

자바스크립트에서 함수 앞에 new 를 붙여 생성자 호출을 하면 아래와 같은 일이 일어납니다.

1. 새 객체가 만들어 집니다.
2. 새로 생성된 객체의 [[Prototype]]이 연결 됩니다.
3. 새로 생성된 객체는 해당 함수 호출 시, this 로 바인딩 됩니다.
4. 이 함수가 자신의 또 다른 객체를 반환하지 않는 한, new 와 함께 호출된 함수는 자동으로 새로 생성된 객체를 반환합니다. (인스턴스 반환)
5. 즉,생성자 함수로서 호출 된 경우 내부에서의 this 는 곧 새로 만들 구체적인 인스턴스 자신이 됩니다

- 우선순위는 new > 명시적 > 암시적 이 됩니다.
