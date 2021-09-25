## DAY 17 - 2021/09/25

### Type 'string' is not assignable to union type, but it exists in union type

- [Literal Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-types) 읽었는지? O
- [Literal Inference](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-inference) 읽었는지? O
- [Type assertion](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions) 읽었는지? X

오늘 코드를 짜다가 재밌는 에러를 만났다. 아마도 내가 한 번 만났던 경우가 있는 에러인 것 같은데, 이번 경우에 확실히 다시 짚고 넘어 가보자.

상황은 이러했다. 내가 union type을 가지는 변수에다가 union type 중 하나의 값을 부여를 해주는 상황이었다. 아래의 코드는 내가 가지고 있었던 상황을 약간 단순하게 가짜로 만든 상황이다.

```typescript
type AvailableFruits = "Banana" | "Apple" | "Pear";

let myFruit = "Banana";

const fruitList: AvailableFruits = myFruit;
```

분명히, `Banana` 라는 값을 가진 `myFruit`을 `fruitList`에 값을 넣어주려는 것인데, 왜 안되는 걸까? 분명히 `AvailableFruits`은 `Banana`라는 값을 가지는데?

그래서 stackoverflow를 찾아보았다.

> [Type string is not assignable to type](https://stackoverflow.com/questions/37978528/typescript-type-string-is-not-assignable-to-type)

흐음... 읽어보니 문제는 이러했다.

```typescript
let myFruit = "Banana";
```

여기에 보면, `Banana`라는 값이 `string`으로 타입이 정의되고 있다. 하지만 `AvailableFruits`은 `string` 타입을 가지는 것이 아니라, `Banana`, `Apple`, `Pear` 이 셋 중의 하나의 값을 가진다. 결국 `AvailableFruits`는 이 3개 중 하나의 타입 밖에 가질 수 없는데, 이 타입들 보다 더 일반적인 타입인 `string`이 들어오려고 하니까 안된다고 얘기를 하는 것이다.

그러면 어떻게 해야할까? type assertion이나 type literal로 변경을 해주어야 한다.

type assertion은 말 그대로 type을 강제시켜주는 것이다. `as`를 사용하면 된다.

```typescript
type AvailableFruits = "Banana" | "Apple" | "Pear";
let myFruit = "Banana" as "Banana";
const fruitList: AvailableFruits = myFruit;
```

우리는 `myFruit`의 타입이 `string`으로 유추되는 대신 type assertion을 통하여 `Banana` 라는 리터럴 타입으로 유추되게 하였다.

또 다른 것은 `as const`를 이용하여 리터럴 타입으로 변경하여 줄 수 있다.

```typescript
type AvailableFruits = "Banana" | "Apple" | "Pear";
let myFruit = "Banana" as const;
const fruitList: AvailableFruits = myFruit;
```

`as const`는 `const`와 똑같다. 그런데 그냥 타입스크립트를 위한 것이라고 보면 된다. `as const`를 쓰면 일반적인 `string`으로 타입이 유추되는 대신 리터럴 타입을 사용하게 해주는 것이다.

### 새롭게 알게된 점

typescript가 `string` 값이나 `number` 값을 `string`, `number` 타입으로 유추되기 전에, type assertion이나 type literal을 통하여
리터럴 타입으로 선언되게 해줄 수 있다.
