## DAY 12 - 2021/09/20

### 'never' 를 사용을 해~!

typescript 공식문서를 읽다가 `never`라는 녀석을 발견하였다. `never`는 어떨 때 쓰이냐 하면은 아무것도 반환을 하지 않는 함수에 쓰인다고 한다.

잠깐만? 우리는 그런 상황을 대비해서 항상 `void`를 쓰지 않는가?

```typescript
function logMsg(msg: string): void {
  console.log(msg);
}
```

위에선 아무것도 반환을 안하고 있지 않은가?

아니다. [MDN의 Function 문서](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function#description)를 보면 어떤 값을 반환을 하지 않을시 `undefined`를 돌려주는 것을 알 수 있다.

```typescript
function logMsg(msg: string): void {
  console.log(msg);
}

const a = logMsg("hey~!");
console.log(a); // undefined
```

하지만 `never는` 다르다. `never`는 함수가 끝까지 실행되지 않거나 에러를 던지는 경우를 얘기한다. 쉽게 말해 함수가 끝까지 실행되지 못하고 중간에 중단됨으로써 정말로 아무 값도 되돌려주지 않는 것을 얘기하는 것이다.

그래서 만약 위의 예제에서 `never`를 쓴다면 어떻게 될까?

```typescript
function logMsg(msg: string): never {
  // A function returning 'never' cannot have a reachable end point.(2534)
  console.log(msg);
}
```

`never`를 반환값으로 가지는 함수는 끝까지 실행될 수 없다고 얘기를 하여준다.

그래서 `never`는 에러를 던지는 상황에 가장 유용할 것이다.

```typescript
function throwCustomError(errMsg: string): never {
  throw new Error(errMsg);
}
```

### 새롭게 알게된 점

`never`라는 타입은 관찰이 될 수 없는 값을 나타낸다. 여기서 관찰이 될 수 없는 값이란, 프로그램 상으로, 로직적으로 말이 되지 않거나 함수의 반환 타입에서는 아무 것도 되돌려주지 않는 것을 뜻한다.

예를 들어, typescript 공식문서에 나오는 예제를 보자.

```typescript
function fn(x: string | number) {
  if (typeof x === "string") {
    // do something
  } else if (typeof x === "number") {
    // do something else
  } else {
    // x는 string이나 number를 타입으로 가지기 때문에
    // 절대 else 문이 실행될수가 없다. 그렇기 때문에 여기서
    // x는 never라는 값을 가진다. '관찰될 수 없는 값'이다.
    x;
  }
}
```
