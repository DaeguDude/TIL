## DAY 19 - 2021/09/27

### Tuple Types

타입스크립트에는 Tuple Type이라는 것이 있다. 이것은 `Array` 타입의 일부인데, `Array`가 얼마만큼의 많은 원소를 담고있는지, 또한 어떤 위치에 어떤 타입의 원소를 가지고 있는지 알고 있을 때 쓸 수 있다.

```typescript
type Student = {
  name: string;
  age: number;
};

function sayTwoStudents(students: [Student, Student]) {
  students[0].name;
  students[0].age;

  students[2].name;
  // Tuple type '[Student, Student]' of length '2' has no element at index '2'.(2493)
}
```

우리가 `students`의 타입을 길이가 2개인 Tuple 타입으로 지정하여 주었기 때문에, 3번째 원소에 접근을 하려고 하니 길이가 2개인 Tuple 타입이라 3번째 원소는 없다고 얘기를 하여준다.

이러한 Tuple 타입은 우리가 자주 쓰는 react에서 심심찮게 찾아볼 수 있다. 우리가 아주 많이 사용하는 `useState`의 타입을 봐보자

```typescript
function useState<S>(
  initialState: S | (() => S)
): [S, Dispatch<SetStateAction<S>>];
```

여기서 `return` type에 한 번 주목을 해보자

```typescript
[S, Dispatch<SetStateAction<S>>];
```

`Return` Type은 2개의 길이를 가지는 Tuple로, 첫번째 타입으로는 `initialState`의 타입을 가지고, 두번째로는 `Dispatch`라는 타입을 가지는 것을 알 수 있다.

```typescript
Dispatch<SetStateAction<S>>
type Dispatch<A> = (value: A) => void;
type SetStateAction<S> = S | ((prevState: S) => S);
```

그 말은 즉슨 아래와 같다.

```typescript
const [isLoading, setIsLoading] = useState(false);
function useState<boolean>(
  initialState: boolean | (() => boolean)
): [boolean, Dispatch<SetStateAction<boolean>>];

type Dispatch = (value: boolean | ((prevState: boolean) => boolean)) => void;
type SetStateAction<boolean> = boolean | ((prevState: boolean) => boolean);
```

`useState(false)`를 사용시...

- 우리는 `initialState`를 `boolean`으로 지정해준다.
- 그리고 `Dispatch는 (value) => void` 요러한 형태의 함수 였는데... `(value: boolean | ((prevState: boolean) => boolean)) => void` 의 함수로 바꿔 준 것이다. 결론은 그냥 `boolean`을 인수로 받을 수도 있고, 함수를 인수로 받을 수도 있다는 것이다. 그 대신 다른 것은 받을 수가 없는 것이다!

### 새롭게 알게된 점

Array타입의 일부인 Tuple Type에 대해서 알게 되었고 그것이 어떻게 우리 주변에서 쓰이고 있는 지도 알게 되었다.
