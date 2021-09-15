## DAY 6 - 2021/09/14

### Generic 너 참 신기한 놈일세.

- [x] Generic 공식문서를 읽었는지?

보통 라이브러리를 사용하다 보면, 내가 어떠한 인수나 props를 넘겨줄 수 있는지를 모를 때가 많다. 보통 항상 공식문서를 찾아보곤 하지만 이미 내가 그 개념에 대해서 잘 알고 있다면 그냥 인수가 무엇인지만 알면 되는 경우가 참 많다.

나는 이때까지는 어떻게 그것을 알아내야 할지 잘 몰랐는데 최근에 들어서야 타입이 정의된 라이브러리들은 어떠한 인수를 받는지, 그 인수의 타입은 무엇인지 등이 정의가 되어있다는 걸 알았다.

그러면 지금 프로젝트에서 사용하는 redux-toolkit을 한 번 예로 들어보자.
redux-toolkit에 store를 만들어주는 `configureStore`라는 함수가 있다.
나는 여기에 어떠한 인수를 넘겨줘야 하는지 잘 모르니까, ctrl + click을 통하여 이놈이 어떠한 인수를 받아주는지 확인해보았다.

```typescript
export declare function configureStore<
  S = any,
  A extends Action = AnyAction,
  M extends Middlewares<S> = [ThunkMiddlewareFor<S>]
>(options: ConfigureStoreOptions<S, A, M>): EnhancedStore<S, A, M>;
```

띠용...! 너무 말도 안되는 복잡한 문법을 가지고 있다. 내가 모르는 문법 투성이기 때문에 하나씩 분해를 해나가야 할 것 같다.

저 위에서 내가 이해가 안되는 것은 크게 두가지 인 것 같다.

- `interface` 이름 뒤에 오는 `<>`(angle bracket)은 도대체 무엇을 뜻하는가?
- `<S = any>` 는 무엇인가...?

일단 첫번째 질문을 찾아보았다. 도대체 `<>`가 무엇을 뜻하는 것이지...?
stackoverflow를 찾아보았다. 조금 구글링을 하다보니 나와 똑같은 질문을 한 사람이 있었다.

[Angle brackets in Typescript after interface declaration](https://stackoverflow.com/questions/40342758/angle-brackets-in-typescript-after-interface-declaration)

답변에 의하면 `<>`은 Generic의 클래스 이름을 준다고 되어있다. 아, 이게 generic의 일부이구나. 나는 Generic을 들어만 보았지 Generic이 어떤 것인지에 대해서 잘 알지는 못한다. 그래서 나는 [Typescript 공식문서 Generic](https://www.typescriptlang.org/docs/handbook/2/generics.html#working-with-generic-type-variables)을 읽어보았다.

Generic의 모든 문법이 다 이해가 가는 것은 아니지만, 대충의 Generic을 쓰는 이유는 알 것 같다. 예시와 한 번 함께 보면 이해가 더 쉬울 것 같다.

```typescript
function logArgument(arg: any): any {
  return arg;
}
```

위의 코드는 `arg`로 `any` 타입을 가지고 있고, return 타입도 `any`를 가지고 있다. 이렇게 쓴 이유는 아마 어떤 타입이 인수로 들어올지 모르기 때문이다. 인수가 무엇이 들어올지 모를 때 이렇게 사용하는 것은 아무 문제가 없다. 하지만 여기서 약간의 문제아닌 문제는 return 타입을 지정하여 줄 수 없다는 것이다. `any`가 인수로 들어왔으니 결과값도 무엇이 될지 모르는 `any`인 것이다.

이러한 문제를 Generic이 해결을 하여준다. Generic은 변수를 사용하여, 변수에 들어오는 값의 타입을 캐치해낼 수 있다. 그릐고 이것을 통하여 여러곳에서 사용할 수 있다.

```typescript
function logArgument<Type>(arg: Type): Type {
  return arg;
}
```

위의 코드를 보면 `<Type>` 이라는 것이 보일 것이다. 이것이 뭐냐하면은, `Type`이 특별한 변수인데, 여기에 들어오는 타입이 `Type`이라는 변수에 저장되어서 다른 인수나 return 타입에 사용을 할 수 있는 것이다. 예를 들어, `number`가 들어오면 인수도 `number`, return 타입도 `number`가 될 것이다.

이렇게 generic으로 정의된 함수는 호출하는 방법이 두 가지가 있다.

```typescript
// <> 안에 type 인수를 넣어주고, 함수의 인수도 넘겨주기
const returnedArg = logArgument<number>(3);
// const returnedArg: number

// type inference 함수의 인수만 넘겨주기
const returnedArg2 = logArgument(3);
// const returnedArg: 3
```

하지만 위의 예제를 보듯이, 두번째는 넘겨준 인수의 타입을 제대로 유추하지 못하고 인수 그대로 타입으로 사용된 것을 알 수 있다. 이것은 아마 우리가 원하는 것이 아닐 수도 있다. 그러므로 `type` 인수와 함수의 인수를 동시에 넘겨주는게 복잡한 상황에서는 안전하다.

이제 두번째 질문에 답해보자. `<S = any>` 는 도대체 무엇이지?
일단 이제 우리는 첫번째 질문을 통하여 `S`가 Type variable 이라는 것을 알게되었다(Type variable의 이름은 꼭 Type이 아니어도 된다. 여기선 `S`가 사용된 것이다).

일단 대충 보아하니... default parameter의 개념인 것 같다. 그래서 default parameter in generic type로 검색을 해보았다. 역시 갓구글...!
조금 찾아보니 똑같은 질문이 있었다.

[Typescript: Force default generic type to be 'any' instead of '{}'](https://stackoverflow.com/questions/34938617/typescript-force-default-generic-type-to-be-any-instead-of)

그리고 여기 답변에 의하면 default parameter가 맞았다. 정식명칭은 Generic Default이다 Type variable `S`가 일단 어떠한 타입이 들어오기 전까지는 `any`로 작동을 하는 것이다.

Generic Default가 어떻게 만들어졌는지는 [typescript github issue](https://github.com/Microsoft/TypeScript/pull/13487)를 보면 알 수 있다.

### 새롭게 알게된 점

Typescript로 정의된 라이브러리에서는 타입을 이미 지정을 해주기 때문에 내가 어떤 것은 인수로 넘겨줄 수 있는지 손쉽게 확인할 수 있다는 것을 알았다. 또한 Generic에 대해서 알게 되었고, Generic에 기본값을 설정해주는 Generic Default에 대해서도 알게되었다.
