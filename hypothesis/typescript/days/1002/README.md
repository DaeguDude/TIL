## DAY 23 - 2021/10/02

### Generic Constraints 재밌는 녀석이구만!

Generic은 재사용 할 수 있는 interface를 만드는 데 아주 효율적인 녀석이다. 왜냐하면, 특정 타입을 정의해두고 쓰는 것이 아니라, 여러 가지 타입에 사용될 수 있기 때문이다.

이것이 무슨 말인지는 코드를 보자.

```typescript
function logArgument(arg: number): number {
  return arg;
}
```

위의 코드는, `number`를 인수로 받고 또한 `number` 를 `return` 타입으로 가지고 있다. 이 일반적이지 않고 `number`에 아주 특정된 함수이다.

그러면 아래의 코드는 어떤가?

```typescript
function logArgument(arg: any): any {
  return arg;
}
```

위의 함수는 인수를 `any`로 받고, `return` 타입도 `any`로 가진다. 이것은 조금 더 일반적이라고 말 할 수는 있겠지만, 여기서 우리는 어떠한 특정인수가 들어왔을 때, `return` 타입을 어떤 것으로 가지는 지 전혀 알 수 없다.

그래서 우리는 Generic이라는 녀석을 써서, 유저가 주는 타입을 '캡쳐' 하여 `return` 타입에도 써 줄 수 있다.

```typescript
function logArgument<Type>(arg: Type): Type {
  return arg;
}

const loggedMsg = logArgument<string>("yo");
// loggedMsg: string

const loggedNum = logArgument<number>(3);
// loggedNum: number;
```

Generic을 통해서 우리는 이제 재사용이 가능한 타입과 interface를 정의해줄 수 있다.

이제 조금 더 나아가 새로운 경우를 생각하여보자. 특정 타입을 인수로 가지고, 그 인수의 타입을 반환해주는 함수를 정의해준다고 해보자. 그런데, 우리는 그 인수의 타입으로 어떤 것이 들어올지 알고 있다. 어떠한 행동을 할 지 아는 것이다.

아래는 `Circle`, `Square`등 인수로 도형의 타입을 가지는 함수이고 그것을 반환하여준다.

```typescript
interface Circle {
  type: "circle";
  radius: number;
}

interface Square {
  type: "square";
  length: number;
}

function logShape<Type>(shape: Type): Type {
  if (shape.type === "circle") {
    // Property 'type' does not exist on type 'Type'
    console.log("it is circle");
  }

  if (shape.type === "square") {
    // Property 'type' does not exist on type 'Type'
    console.log("it is sqaure");
  }

  return shape;
}
```

우리는 들어오는 인수의 타입에 따라서 `return` 의 타입을 정의해주기 위해 Generic을 썼다. 하지만, typescript가 오류를 주고있다.

> Property 'type' does not exist on type 'Type'

이것은 무슨 뜻일까? 타입스크립트가 `Type`에 들어올 타입에 `type`이라는 프로퍼티가 존재하는지 알 수가 없으니 오류를 주고 있는 것이다! 하지만 우리는 `type`이라는 프로퍼티를 가진 도형의 타입들이 인수로 들어올 것을 알고있다. 이럴 때 우리는 `extends` 키워드를 사용하여, `type`에 제한을 주어야 한다. 그리고 이것을 Generic Constraint 라고 한다.

```typescript
interface Circle {
  type: "circle";
  radius: number;
}

interface Square {
  type: "square";
  length: number;
}

function logShape<Type extends Circle | Square>(shape: Type): Type {
  if (shape.type === "circle") {
    console.log("it is circle");
  }

  if (shape.type === "square") {
    console.log("it is sqaure");
  }

  return shape;
}

const myCircle = logShape({
  type: "circle",
  radius: 10,
});
// const myCircle: {
//     type: "square";
//     radius: number;
// }

const mySquare = logShape({
  type: "square",
  length: 5,
});
// const mySquare: {
//     type: "square";
//     length: number;
// }
```

위는 `Type`이라는 아이가 `Circle` 아니면 `Square`라는 타입을 가질 것이야~! 라고 말을 해주는 것이다. 그렇기 때문에 `shape`에는 `Circle` 아니면 `Square`가 들어오게 되는 것이고, 반환값도 그렇게 정의되는 것이다.

### 새롭게 알게된 점

Generic을 사용하여 특정 타입 하나만에 사용되는 것이 아닌 여러 가지 타입에 유연하게 대응할 수 있는 법을 알았다.
그리고 여러가지 타입에 유연하게 대응을 함과 동시에, 내가 어떠한 타입이 들어올지 대충의 예상이 있다면, Generic Constraint를 사용하여 특정한 타입들을 받아주게 하는 방법도 있다는 것을 알았다.
