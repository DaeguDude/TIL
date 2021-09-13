## DAY 5 - 2021/09/11

### Extending Union Type

오늘 Test Drvien Development 를 연습하기 위해서 시작한 프로젝트인 Battleship game 프로젝트를 진행 중, 타입을 extend 해서 써야할 경우가 생겼다. 하지만 나는 그렇게 한 번도 해본적이 없기 때문에 어떻게 해야할 지 전혀 감이 오지 않았다.

나의 상황은 아래와 같았다. 아래와 같이 `ShipNames`와 `CellStatus`란 타입이 있는데, `CellStatus`에서,
`ShipNames`의 값 중 하나를 가질 수도 있다고 정의를 해주어야 했다. 그러니, 말 그대로 `CellStatus` 란 Union Type이 `ShipNames`란 Union Type을 자기 자신의 값으로 가져야 하는 것이었다.

```typescript
export type ShipNames =
  | "Carrier"
  | "Battleship"
  | "Destroyer"
  | "Submarine"
  | "PatrolBoat";

export type CellStatus = "noHit" | "missed";
```

그래서 [stackoverflow](https://stackoverflow.com/questions/45745441/extending-union-types-alias-in-typescript)에 한 번 union type을 extend 하는 법을 찾아보았다. 답이 잘 나오지는 않았다. 음... 너무 뻔한 거라 답이 안 나오는 건가? 그래서, documentation 에서 extend 하는 법을 보았던 것 같아 [공식문서](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)로 다시 한 번 들어가보았다.

공식문서에서는 이런 식으로 type을 extend 하라고 나와있었다.

```typescript
type Animal = {
  name: string
}

type Bear = Animal & {
  honey: boolean
}



const bear: Bear = {
  name: "BlackBear"
  honey: false
}
```

그런데 이것은 보면 두 개의 객체의 타입을 동시에 가지는 것이지, 나처럼 Union Type에 또 다른 Union Type을 추가해주는 것은 아니다.

음...고민을 하다 이런 생각이 났다.

"둘다 Union이니까, 그냥 `|` 을 이용해 `ShipNames` 라는 Union Type을 `CellStatus`의 값으로써 추가해주면 되지 않을까?" 그래서 한 번 해보았다.

```typescript
export type ShipNames =
  | "Carrier"
  | "Battleship"
  | "Destroyer"
  | "Submarine"
  | "PatrolBoat";

export type CellStatus = "noHit" | "missed" | ShipNames;

const myCell: CellStatus = "Battleship";
```

오오.. 된다! 그냥 Type을 더 추가하기만 해주면 되는 것이었다. 이제 `CellStatus` 는, `noHit`, `missed`, 그리고 `ShipNames` 의 값 중 하나를 값으로 가질 수 있다. 그냥 Union Type을 값으로써 추가해주면 되는 이렇게 간단한 것을 왜 생각하지 못했을까? ㅋㅋㅋ 웃기긴 하다

조금 더 자세한 설명을 보기 위해 [공식문서의 Union Type 부분](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types)을 다시 읽어보았다.

가장 첫번째 머리에, 내가 바라던 정답이 적혀 있었다...

> TypeScript’s type system allows you to build new types out of existing ones using a large variety of operators. Now that we know how to write a few types, it’s time to start combining them in interesting ways. **A union type is a type formed from two or more other types, representing values that may be any one of those types.**

위에서 보듯이, 두 개나 그 이상의 타입들을 합쳐서 그 타입들 중 하나를 값으로 가지는 타입을 만들 수 있다는 것이다. 예제에서는 이미 존재하는 `string` 이나 `number` 등을 합쳐서 사용하였기 때문에, 나는 내가 만든 `ShipNames` 라는 타입을 사용할 수 있다는 걸 생각하지 못했다. 참...인간은 단순해!(아니 나란 인간이 단순한건가...!?)

그리고, 또 팁은 Union Type에 사용되는 Type들을 Union의 멤버(Union's member)라고 부른다는 것이었다.

그러니 아래의 코드를 보면, 내 `CellStatus` 라는 Union Type의 멤버들은, `noHit`, `missed`, 그리고 `ShipNames` 인 것이다!

```typescript
export type CellStatus = "noHit" | "missed" | ShipNames;
```

#### 꿀팁 약간 더 추가

공식문서에서 본 꿀팁을 약간 더 추가하자면, union type은 두 개 아니 그 이상의 타입들을 값으로 가질 수 있기 때문에, 만약에 그 값을 가지고 무엇을 하고 싶다면 그 하려는 행위가 모든 멤버들의 타입에 충족되는 것이여야 한다.

예를 들어 아래의 코드를 보면, `toUpperCase` 메쏘드는 `string` 에서만 존재하고 `number` 에서는 존재하지 않기 때문에 typescript가 사용을 할 수 없다고 주의를 준다.

```typescript
function sayName(name: number | string) {
  consolelog(name.toUpperCase())
})

// Property 'toUpperCase' does not exist on type 'string | number'.
// Property 'toUpperCase' does not exist on type 'number'.
```

그래서 이럴 경우에, 공식문서에서는 narrowing 이라는 기법을 사용하여서, 특정 타입일 때 특정 행위를 할 수 있게 지정을 해 주라고 되어있다.

```typescript
function sayName(name: number | string) {
  if (typeof name === 'string') {
    console.log(name.toUpperCase())
  } else {
    console.log('hey ' + name)
  }
})
```

`name` 이 `string` 일시에만 `toUpperCase` 를 사용하게 조건문을 주니 이제 typescript에서 오류를 주지 않는다!

### 새롭게 알게된 점

이미 존재하는 타입들을 이용하여서 Union Type을 만드는 법을 배웠다. 내가 생각하는 Union Type은 `string`, `number` 등등 자바스크립트의 원시 데이터 타입만 이용할 수 있는 줄 알았는데 그게 아니고, 어떤 타입이든 그 타입들을 합쳐서 사용할 수 있는 것이었다.
