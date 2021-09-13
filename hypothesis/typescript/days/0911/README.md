## DAY 3 - 2021/09/11

### Typescript Alias

[Typescript Type Alias](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-aliases)

오늘 Test Driven Development를 연습하기 위해 시작한 [Battleship project](<https://en.wikipedia.org/wiki/Battleship_(game)>) 자바스크립트 프로젝트를 TS 프로젝트로 바꾸는 도중이었다. 코드 안에서 특정한 좌표가 맞았는지 안 맞았는지를 기록하여주는 `hits` 라는 배열이 있었다. 그리고 이 배열은 `false` 아니면 `true` 인 값을 가지는 `boolean` 타입이였다. 그래서 나는 이 `hits`를, `boolean` 값들을 가진 배열이라고 정의를 해주려고 하니, 배열의 타입을 정의하는 법이 생각이 나지 않았다. 왜냐하면, `type` 이나 `interface` 를 통하여 객체의 타입만 정의를 했던 기억밖에 없었기 때문이다.

예를 들어, 나는 아래의 코드와 같이 객체 타입만 정의를 해본 것 같다.

```typescript
type Student {
  name: string;
  age: number;
  grade: "A" | "B" | "C" | "D"
}
```

도대체 배열은 어떻게 정의를 하지...? 나는 정말 이것을 진짜 고민을 했다...! ㅋㅋㅋ 그러던 도중, 기억이 잘 나진 않는데 그냥 배열을 값으로 넣어주면 안되나 라는 생각이 들었다.

```typescript
type hit = boolean; // 응 이게 된다고...?
type hits = hit[]; // 그럼 이게 되잖아...!
```

위의 코드처럼 왜이리 간단한 것을 생각못하였을까? 항상 객체모양으로 된 `type`만 봐서 배열을 가진 타입을 만드는 것은 생각조차 못했던 것이다.

그리고 오늘 Documentation을 읽다가 내가 오늘 한 고민을 문서적으로 정확하게 정리해주는 것을 발견했다. 그 이름하여... **type alias**!!! alias의 사전적 정의는 가명, 별명이다. 결국은 `type` 라는 키워드를 쓰면 특정 타입에 별명을 붙여주는 것이다.

type alias가 어떠한 타입이든 이름을 붙여줄 수 있기 때문에 그 이름을 통하여 우리는 정의된 타입을 손 쉽게 쓸 수 있는 것이다.

예를 들어보자. 우리는 `string` 타입에 `myString` 이라는 이름을 붙여주었다.

```typescript
type myString = string;
```

이제 그리고 이 이름표를 가지고 항상 `string` 타입을 받아주게 사용할 수 있는 것이다.

```typescript
function sayName(name: myString) {
  console.log(name);
}

sayName("DaeguDude!");
```

type Alias.... 항상 사용을 해왔지만 타입에 이름표를 붙여준다는 개념으로는 전혀 생각을 하지 못하였다. 아주 흥미로웠다!

### 새롭게 알게된 점

오늘은 type Alias 라는 녀석에 대해 알게되었다. 이 녀석이 하는 일은 어떤 타입이 되었든 그 타입에 이름을 붙여주는 녀석이다. type Alias는 타입에 이름을 붙여주는 것이기 때문에 객체 타입, 배열 타입, 숫자 타입 등등 어떤 타입이 되든 전혀 상관없다.
