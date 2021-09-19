## DAY 11 - 2021/09/19

### Function Type Expression

가끔씩 타입스크립트가 정의된 다른 라이브러리들을 보면 이런 생각을 한다. '도대체 요렇게 이상하게 생긴 문법은 무엇일까?' 그 중에 오늘 하나를 알게되었다. Function Type Expression이라고, 말 그대로 함수를 표현해주는 함수타입표현식이다. 웃긴게... 내가 이것을 이미 알고 있었다는 것이다. 이것이 코드에서 같이 쓰이니까 몰랐던 것일뿐. 코드를 한 번 보자

```typescript
function sayHi(fn: (msg: string) => void) {
  fn("Say hi");
}

function print(msg: string) {
  console.log(msg);
}
```

`sayHi` 매개변수 안의 이상한 `(msg: string) => void`는 도대체 어떻게 해석을 해야하는 것일까...?

이게 Function Type Expression이다. 그렇다면 아래의 코드를 한 번 보자

```typescript
type PrintFunc = (msg: string) => void;
function sayHi(fn: PrintFunc) {
  fn("SayHi");
}
```

응...? `sayHi`의 `fn`이라는 변수가 `PrintFunc`를 받는다는 것을 쉽게 알 수 있다.
뭐지? 아까랑 똑같은데?

```typescript
function sayHi(fn: (msg: string) => void) {
  fn("Say hi");
}

type PrintFunc = (msg: string) => void;
function sayHi(fn: PrintFunc) {
  fn("SayHi");
}
```

이 두개는 결국 똑같은 아이이다. 첫번째 예제는 그냥 Function Type Expression으로 바로 fn이 받을 타입의 정의를 해준 것이고, 밑의 예제는 `PrintFunc`라는 Type Alias를 사용하여 Function Type Expression에 이름을 붙여주고 사용해준 것이다.

### 새롭게 알게된 점

함수의 타입을 표현해 줄 수 있는 Function Type Expression 이라는 것에 대해서 알게 되었다.
