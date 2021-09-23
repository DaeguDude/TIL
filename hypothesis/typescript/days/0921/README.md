## DAY 13 - 2021/09/21

### useState 타입

오늘 `useState`를 쓰다가 오류를 만나게 되었다. 다름이 아니라, 대기 고객을 보여주는 컴포넌트에서, 대기 고객의 리스트를 상태로
관리를 해주려고 하였다. 그래서 먼저 대기 고객이라는 객체가 어떠한 프로퍼티를 가지는지 타입으로 정의를 해주었다.

```typescript
export type WaitingCustomer = {
  waitingNo: number;
  phone: string;
  numAdults: number;
  numKids: number;
  createdAt: string;
  updateStatus: "WAITING";
};
```

그 다음에는 대기고객을 보여주는 컴포넌트 `WaitingList` 에서 `useState`를 사용하여, 정의된 대기고객 타입 `WaitingCustomer`의 값을 가지는 배열의 타입을 `useState`에 넘겨줌으로써 대기고객의 리스트가 정의된 대기고객의 값만 가지도록 해주었다.

```typescript
const WaitingList = () => {
  const [customerList, setCustomerList] = useState<WaitingCustomer>([]);
  // Argument of type 'never[]' is not assignable to parameter of type 'WaitingCustomer | (() => WaitingCustomer)'.
  // Type 'never[]' is not assignable to type '() => WaitingCustomer'.
  // Type 'never[]' provides no match for the signature '(): WaitingCustomer'.ts(2345)
  return (
    // ...
  )
}
```

하지만 오류가 뜨는 것이었다. 왜 오류가 뜨는거지? `WaitingCustomer`를 값으로 가지는 배열은, 빈 배열일 수 없는 것인가? 여기서 말하는
`never[]`는 무슨 말이지?

그렇게 고민을 하고 있었는데... 생각해보니 `WaitingCustomer` 타입은 `WaitingCustomer` 값을 가지는 배열의 타입과는 다르다는 것이다!!

다시 말해서, 아래의 내가 대기고객 **리스트**를 담고자 했던 아래의 코드는

```typescript
const [customerList, setCustomerList] = useState<WaitingCustomer>([]);
```

사실 그냥 객체를 담게 정의된 것이었다.

```typescript
const WaitingList = () => {
  const [customerList, setCustomerList] = useState<{
    waitingNo: number;
    phone: string;
    numAdults: number;
    numKids: number;
    createdAt: string;
    updateStatus: "WAITING";
  };>([]);

  return (
    // ...
  )
}
```

그리고 `useState`의 정의를 보면 이렇게 되어있다.

```typescript
function useState<S>(
  initialState: S | (() => S)
): [S, Dispatch<SetStateAction<S>>];
```

`useState`는 `S`라는 변수를 가지고, 여기에 타입을 정의해 줄 수 있다. 우리는 여기에 `WaitingCustomer`를 넘겨준 것이다. 그리고 매개변수 `initialState`에는 `S`의 타입이 넘어와야 하는 것이다. 아니라면 `() => S` 를 반환하는 함수도 넣어줄 수 있다. 그리고 반환 값은 배열로 `S` 타입과, `Dispatch`를 반환하여 준다.

### 새롭게 알게된 점

하나의 객체 타입과, 객체를 값으로 가지는 배열의 타입은 다르다.
