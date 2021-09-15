## DAY 7 - 2021/09/14

### 뭐야, e.target에 value property가 없다고!?

오늘 React에서 작업을 하다가 약간 당황스러운 상황을 만났다. 상황은 이러했다.
input element의 onChange에 콜백 함수를 전달하여 주어 상태를 관리를 하려 하였다.

당연히 나는 콜백 함수에 매개변수로 e를 받았고, e는 React.ChangeEvent 타입을 받는다고 정의했다.
그리고 원래 항상 해왔던 것처럼 e.target.value로 값을 컨트롤해주려 했다.

그런데 이게 웬일이람? e.target에 value property가 없다고 뜨는 것이 아닌가?
이게 뭔말인가...? React 공식문서에 떡하니 Input element를 관리하는 예제에 떡하니 e.target.value
를 찍어서 값을 바꿔주는게 나오는데...?

일단 기본적으로 정말 축약된 예시로써 살펴보자.

```typescript
import React, { useState } from "react";

export default function App() {
  const [count, setCount] = useState(0);

  const onChangeHandler = (e: React.ChangeEvent) => {
    console.log(e.target.value);
    // any: Property 'value' does not exist on type 'EventTarget & Element'.
  };

  return <input type="number" value={count} onChange={onChangeHandler} />;
}
```

흐음 왜 그런 것이지...? ChangeEvent 타입에 target이 정의되어 있지 않은 것인가? 그건 또 말이 안되는데?
그러면 target 자체에 접근을 못했을테니까. 그러면 ChangeEvent에 들어가서 뭐가 정의되어 있는지 확인해보자

React.ChangeEvent는 이런식으로 정의되어 있다.

```typescript
interface ChangeEvent<T = Element> extends SyntheticEvent<T> {
  target: EventTarget & T;
}
```

일단 target이 정의는 되어있다! 그러니까 우리가 접근이 가능했겠지(아니면 SyntheticEvent에 들어있었을 지도 모른다).
그런데 EventTarget & T 라고 되어있다. 내가 기억하기로 &는 Type extends 하는 것이다. 결국 target은 EventTarget과 T의 프로퍼티를 다 쓸 수 있는 것이다. 근데 생각하여보니 내가 Generic type을 넘겨주지 않았다. 그러니
Generic Default가 쓰여서 Element가 넘어갔을 것이다. 결국 아래와 같은 상황인 것이지

```typescript
interface ChangeEvent<T = Element> extends SyntheticEvent<T> {
  target: EventTarget & Element;
}
```

그러면 나의 추론은 EventTarget과 Element에 value라는 프로퍼티가 없다는 것이다!
한 번 확인해보자

```typescript
interface Element {}
interface EventTarget {}
```

음...두 개다 interface가 비어있다. 이러면 또 말이안되는데...? 왜냐하면 몇 개의 다른 프로퍼티들을 사용할 수 있었기 때문이다.

여튼 stackoverflow를 찾아봤다.

[property value does not exist on typescript](https://stackoverflow.com/questions/42066421/property-value-does-not-exist-on-type-eventtarget)

여기서 찾아보니 내 target이 어떠한 HTMLElement인지 얘기를 해주어야 된다는 것이다! 그러면 내 target은 input element니까 HTMLInputElement를 넘겨주면 되겠다. 그러면 `ChangeEvent<T = Element>` 여기에서, T 변수에 Element대신 HTMLInputElement를 쓰겠지. 그리고 HTMLInputElement에 value라는 프로퍼티가 있지싶다.

아 아니다... 지금 CodeSandbox이기 때문에 비어있는 것이다. 여튼 HTMLInputElement에는 있을 것이다!

### 새롭게 알게된 점

e.target에 value 프로퍼티가 없다는 황당한 경우를 겪었다. 하지만 그것이 내가 어떠한 HTMLElement를 쓰는지 정의를 안해줘서 였다는 것을 알았다.
