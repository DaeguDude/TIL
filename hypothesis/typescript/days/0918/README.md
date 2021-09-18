## DAY 10 - 2021/09/18

### Discriminated Union

어제 non-null assertion이라는 것에 대해서 알아보았다. 다름이 아니라, typescript가 어떤 타입인지 정확히
알 수 없으니, 우리가 이것은 null이 아니야라고 !를 통해 지정해주는 것이었다.

```typescript
interface Shape {
  kind: "circle" | "square";
  radius?: number;
  sideLength?: number;
}

function getArea(shape: Shape) {
  return Math.PI * shape.radius! ** 2;
  // ! 를 통해 오류를 없앴다
}
```

하지만, 여기에는 구조적인 문제가 있다. **어떤 문제지?**

그렇기 때문에, 우리는 discriminated union이라는 것을 쓸 수 있다. discriminated union이라 함은
두 개의 타입이 똑같은 리터럴 프로퍼티를 공유하는 것이다. discriminated union이 되기 위한 조건은
그 타입들이 공통된 리터럴 멤버를 가지고 있어야 한다는 것이다.

```typescript
type RequestA = {
  action: "a";
  args: number[];
};

type RequestB = {
  action: "b";
  args: string;
};
```

위의 코드에서는 requestA와 requestB가 action이라는 리터럴 값을 가진 멤버를 공유하고 있다. 그렇기 때문에 최대한 자바스크립트와 비슷한
코드로 작성을 할 수 있다. !를 쓰지 않고 말이다.

```typescript
type Request = RequestA | RequestB;

function requestData(request: request) {
  switch (request.action) {
    case "a":
      return (doubledNumbers = request.args.map((num) => num * 2));
    case "b":
      return request.args;
  }
}
```

그리고 아래의 코드를 통해서 response타입도 잘 정의를 해 줄 수 있다.

```typescript
type RequestResponseMessage<Req, Resp> = [Req, Resp];
type ResponseA = { result: string };
type ResponseB = { status: number };
type AMessage = RequestResponseMessage<RequestA, ResponseA>;
type BMessage = RequestResponseMessage<RequestB, ResponseB>;
```

이 예제코드는 [fullstory](https://www.fullstory.com/blog/discriminated-unions-and-exhaustiveness-checking-in-typescript/)에서
들고왔다. 이것을 통해 회사에서 쓰는 API에 구현을 해두어야겠다. 아주 유용할 것 같다.

### 새롭게 알게된 점

discriminated union이라는 것에 대해서 알게 되었고 이것이 얼마나 타입이 보장된 코드를 작성함과 동시에 자바스크립트에
최대한 가깝게 작성을 할 수 있는 지를 알았다.
