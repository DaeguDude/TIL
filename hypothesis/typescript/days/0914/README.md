## DAY 6 - 2021/09/14

### Figuring out what I can pass by seeing declared Type of component

오늘 Redux를 사용하면서 Typescript의 유용한 점을 알게 되었다. 그 점은, Typescript로 작성된 라이브러리일 경우, 함수가 어떤 매개변수를 가지는지 그래서 어떠한 인수를 넘겨줘야 하는지 등등을 알 수 있다는 것이었다.

예를 들어서 redux-toolkit 에서 제공하는 configureStore를 ctrl+click을 하여서 type이 어떻게 정의되었는지 한 번 봐보자.

```typescript
export declare function configureStore<
  S = any,
  A extends Action = AnyAction,
  M extends Middlewares<S> = [ThunkMiddlewareFor<S>]
>(options: ConfigureStoreOptions<S, A, M>): EnhancedStore<S, A, M>;
```

위처럼 정의가 된다. 일단 지금 내가 이해를 하기에는 약간 너무 복잡한 Typescript 문법을 가지고 있는 것 같다. 그러면 일단 간단하게 하나씩 이해해보자.

- interface 이름 뒤에 오는 <>(angle bracket)은 도대체 무엇을 뜻하는가?
- 그 안에 있는 것들은 무엇이지?

일단 첫번째 질문을 답해보자..
우리의 친구 stackoverflow를 찾아보았다! 그러니 나와 똑같은 질문을 한 사람이 있었다. 역시...나만 그런게 아니었어..!

[Angle brackets in Typescript after interface declaration](https://stackoverflow.com/questions/40342758/angle-brackets-in-typescript-after-interface-declaration)

답변에 의하면 <>은 Generic의 클래스 이름을 준다고 되어있다. 아, 이게 generic의 일부이구나. 그래서 나는 [Typescript 공식문서 Generic](https://www.typescriptlang.org/docs/handbook/2/generics.html#working-with-generic-type-variables)을 찾아갔다.

그래서 Generic을 읽어봤다. Generic을 쓰는 이유는 다음과 같다. 코드와 설명을 하면 더 좋을 것 같다.

```typescript
function logArgument(arg: any): any {
  return arg;
}
```

위으 코드는 arg로 any 타입을 가지고 있고, return type도 any를 가지고 있다. 이렇게 쓴 이유는 아마 어떤 타입이 인수로 들어올지 모르기 때문이다. 이렇게 해도 어떤 타입을 받을 수는 있지만 이렇게 하면 한 가지 큰 문제가 생긴다. return type을 지정하여 줄 수 없다는 것이다. 결국, logArgument를 썼을 때 어떤 타입이 돌아올지 에상을 할 수 없다는 것이다.

이러한 문제를 Generic이 해결을 하여준다. Generic은 변수를 사용하여, 변수에 들어오는 값의 타입을 캐치해낼 수 있다. 그릐고 이것을 통하여 여러곳에서 사용할 수 있다.

```typescript
function logArgument<Type>(arg: Type): Type {
  return arg;
}

const returnedArg = logArgument<number>(3);
// const returnedArg: number
```

이렇게 generic으로 정의된 함수는 호출하는 방법이 두 가지가 있다.

```typescript
// <> 안에 type 인수를 넣어주고, 함수의 인수도 넘겨주기
const returnedArg = logArgument<number>(3);
// const returnedArg: number

// type inference 함수의 인수만 넘겨주기
const returnedArg2 = logArgument(3);
// const returnedArg: 3
```

하지만 위의 예제를 보듯이, 두번째는 넘겨준 인수의 타입을 제대로 유추하지 못하고 인수를
그대로 타입으로 사용된 것을 알 수 있다. 이것은 아마 우리가 원하는 것이 아닐 수도 있다. 그러므로 type 인수와 함수의 인수를 동시에 넘겨주는게 복잡한 상황에서는 안전하다.

### 새롭게 알게된 점

```typescript
export interface Action<T = any> {
  type: T;
}
```

위와 같이, interface의 이름 뒤에 붙는 `<>`은 generic을 사용할 때 사용된다는 것을 알았다. 그리고 `T = any` 는 Generic Default라고Generic에 default로 사용할 Type을 지정해 줄 수 있다.

- [Generic Defaults](https://github.com/Microsoft/TypeScript/pull/13487)
