## DAY 16 - 2021/09/24

### Property 'x' does not exist on union type

- [The in operator narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-in-operator-narrowing) 문서를 읽었는지? YES!

오늘 타입스크립트로 작업을 하다가 재밌는 오류가 떴다. 특정 고객의 타입을 받아 화면에 그에 알맞는 고객카드 UI를 렌더링해주는 컴포넌트
`CustomerCard` 라는 것이 있었는데, 이 녀석이 `props`로 `customer`를 가지는데, 이 `customer` 프로퍼티는 "대기고객(`WaitingCustomer`)"과 "입장안내 고객(`EnterNotifiedCustomer`)"을 받는다.

```typescript
export interface Customer {
  waitingId: number;
  phoneNumber: string;
  numAdults: number;
  numKids: number;
}
export interface WaitingCustomer extends Customer {
  updateStatus: "WAITING" | "CUSTOMER_CANCEL";
}

export interface EnterNotifiedCustomer extends Customer {
  enterNotifiedAt: string;
  updateStatus: "ENTER_NOTIFIED" | "CUSTOMER_CANCEL";
}

type CustomerCardProps = {
  customer: WaitingCustomer | EnterNotifiedCustomer;
};

const CustomerCard = ({ customer }: CustomerCardProps) => {
  const { waitingId, phoneNumber, numAdults, numKids, enterNotifiedAt } =
    customer;
  // Property 'enterNotifiedAt' does not exist on type 'WaitingCustomer | EnterNotifiedCustomer'.ts(2339
};
```

그리고 나서 나는 생각했다. 일단 object destructuring을 통해서 `enterNotifiedAt`이 `customer`에 존재한다면 그 값을 받아주고,
아니면 undefined로 선언이 되겠지라고 말이다.

그런데, 아래와 같은 오류가 떴다.

> Property 'enterNotifiedAt' does not exist on type 'WaitingCustomer | EnterNotifiedCustomer'.ts(2339)

이것은 무엇을 뜻하는 것일까? `enterNotifiedAt`은 분명히 `EnterNotifiedCustomer` 타입에 존재하는데??? `WaitingCustomer`에 존재하지 않아서 문제가 생긴건가??? 그래서 stackoverflow를 한 번 찾아보았다.

[property 'x' does not exist in union type](https://stackoverflow.com/questions/58974640/typescript-property-does-not-exist-on-union-type)

아... 여기의 글을 읽어보니 나의 상황과 같았다. 결국은 두 개의 타입이 있는데, 이 두 개의 타입은 겹치는 프로퍼티가 없어서 if 문을 사용한 구분을 못 해 주는 것이다.

```typescript
type obj1 = {
  fly: () => void;
};

type obj2 = {
  swim: () => void;
};

function move(obj: obj1 | obj2) {
  if (obj.fly) {
    obj.fly();
    // Property 'fly' does not exist on type 'obj1 | obj2'.
  }
}
```

그렇다면 이렇게 겹치는 프로퍼티가 없을 때는 어떻게 해야할까? 답변에서 `in` 연산자를 사용하여 쉽게 해줄 수 있다고 적어두었다. `in` 연산자는 객체에 프로퍼티가 존재하는지 안 존재하는지의 여부애 따라서 `true` 혹은 `false`를 돌려주는 녀석인데, typescript는 이 녀석을 사용해서 타입을 유추해낼 수 있다.

그래서 위의 것은 아래와 같이 바꿔줄 수 있다.

```typescript
type obj1 = {
  fly: () => void;
};

type obj2 = {
  swim: () => void;
};

function move(obj: obj1 | obj2) {
  if ("fly" in obj) {
    obj.fly();
  } else {
    obj.swim();
  }
}
```

위에서는, 이제 오류가 없이 깔끔하게 타입스크립트가 타입을 유추해낸 것을 볼 수 있다.

그렇다면 나의 예제로 돌아가, 나의 문제를 처리해보자. `enterNotifiedAt`이 `WaitingCustomer`에는 없기 때문에 일어난 일이다. 그렇다면 `in` 연산자를 이용해 프로퍼티가 있을 때만 값을 주게하면 된다.

```typescript
const CustomerCard = ({ customer }: CustomerCardProps) => {
  const { waitingId, phoneNumber, numAdults, numKids } = customer;
  let enterNotifiedAt;
  if ("entereNotifiedAt" in customer) {
    enterNotifiedAt = customer.enterNotifiedAt
  })
};
```

### 새롭게 알게된 점

어떠한 특정 프로퍼티가 union type에 존재하지 않는다는 에러는 narrowing(좁혀나가기) 기법을 통해서 타입스크립트가 타입을 유추할 수 있게
해주어야 된다는 것이다. 이러한 경우에는 `in` 연산자를 사용해서 손 쉽게 해결하여 줄 수 있다.
