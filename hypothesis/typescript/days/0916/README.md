## DAY 8 - 2021/09/16

### ReturnType, 넌 누구냐?

최근에 회사내에서 하고있는 프로젝트에서 redux를 사용하고 있다. 그런데 redux를 typescript와 함께사용하기 때문에 약간의 초기셋업이 필요하다.
[Define Root State and Dispatch Types](https://redux.js.org/tutorials/typescript-quick-start#define-root-state-and-dispatch-types)에서 보면 알 수 있듯이, 초기의 `RootState`와 `AppDispatch`의 타입을 지정하여 준다. 이렇게 지정을 하여줌으로써 우리가 나중에 `state`에 무엇이 들어갈지를 알 수 있는 것이다.

하지만 여기서 신기한 문법을 보았다.

```typescript
export type RootState = ReturnType<typeof store.getState>;
```

`ReturnType` 이라는 것인데... 이것은 도대체 무엇인가?

그래서 [Typescript 공식문서](https://www.typescriptlang.org/docs/handbook/utility-types.html#returntypetype)를 찾아보았다.

> Constructs a type consisting of the return type of function Type.

쉽게 얘기하여서, 함수가 돌려주는 값의 타입을 이용하여 타입을 생성하는 것이다.

그래서 예를 들어, 요렇게 해줄 수 있는 것이다.

```typescript
const student = {
  sayHi: (msg: string) => {
    console.log(msg);
  },
};

type myType = ReturnType<typeof student.sayHi>;
// myType: void
```

그래서 redux 예제로 다시 돌아가보면, 우리는 `store.getState`를 했을 때 return되는 타입을 이용하여
타입을 생성하는 것이다.

```typescript
export type RootState = ReturnType<typeof store.getState>;
```

### 새롭게 알게된 점

`ReturnType` 라는 녀석을 새롭게 알게되었다. 이 녀석은 함수의 `return` 타입을 통하여 새로운 타입을 생성한다.
