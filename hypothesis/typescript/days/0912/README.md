## DAY 4 - 2021/09/11

### Typescript

[Literal Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-types)

리터럴 타입. 오늘은 리터럴 타입이라는 것에 대해서 알게 되었다. 아마도 내가 사용했던 것들이였겠지만(사실 사용을 잘 안했을 수도...?) 이러한 용어가 있다는 것은 몰랐다. 그리고 조금 유용한 것들을 배울 수 있었다.

일단 리터럴 타입 대해서 기본적으로 설명을 하자면, 보통 우리는 특정한 값의 타입을 지정하여 준다.

```typescript
function sayHi(msg: string) {
  console.log(msg);
}
```

위에서는 `msg`라는 `string`이라는 값의 타입을 받는다. 그런데 `string`은 `string`으로 된 모든 값을 다 받을 수 있다. 예를 들어, `hello world', 'hey' 등등 어떤 값이 들어가도 상관없다. 하지만 리터럴 타입은 약간 다르다. 조금 더 구체적으로, 나는 특정한 값을 받겠다! 라고 지정을 해 줄 수 있는 것이다.

```typescript
type LoginStatus = "LOGIN" | "LOGOUT";
```

하지만, 이렇게 특정한 값을 받는다고만 하면 크게 유용하지는 않을 것이다 라고 문서에서 설명을 한다. 맞는 말인 것 같다. 그래서 union type이라고, 다른 값과 섞어서 쓰면 훨씬 유용할 것 같다.

```typescript
type StudentStatus = "재학" | "휴학" | "졸업";

type Student = {
  name: string;
  status: StudentStatus;
};

function sayStudentStatus(student: Student) {
  console.log(student.status);
}

sayStudentStatus({
  name: "Daegudude",
  status: "중퇴", //Type '"중퇴"' is not assignable to type 'StudentStatus'.(2322)
});
```

위의 코드를 보면, 우리가 `student`의 `status`에 `재학`, `휴학`, `졸업`이라는 특정한 값만을 받아주기로 하였기 때문에, `sayStudentStatus`에서 오류가 나는 것을 알 수 있다. 이렇게 조금 더 특정한 값을 세부적으로 지정해줌으로써 조금 더 안전하게 코딩을 해 나갈 수 있다.

`string`만 되는 것이 아니라 모든 값을 다 리터럴 타입으로 지정하여 줄 수 있다.

```typescript
function compareValue(num1: number, num2: number): -1 | 0 | 1 {
  // ...
}

compareValue(3, 4);
```

그리고 조금 더 흥미롭게 literal inference라는 것도 있었다. 요것은 type assertion과 섞어서 이미 존재하는 `string`, `number` 등등의 타입을 추론하여 적어주는 대신 리터럴 타입을 쓰게 해주는 것이다.

아래의 예시를 보면, `myStudnet`의 `status`의 타입을 `string`으로 추론을 하였기 때문에, `string`이면 값을 바꿀 수 있는 게 보인다.

```typescript
const myStudent = { name: "Daegu", status: "재학" };
myStudent.status = "중퇴";
```

하지만 type assertion을 통하여, 특정한 값을 타입으로 추론하게 할 수 있다.

```typescript
const myStudent = { name: "Daegu", status: "재학" as "재학" };
myStudent.status = "중퇴";
// Type '"중퇴"' is not assignable to type '"재학"'.
```

타입스크립트가 우리에게 `중퇴` 라는 타입은 `string` 타입에 대입이 불가능한 것이 아니라 `재학` 이라는 타입에 대입이 불가능하다고 얘기해 주는 것이 보일 것이다. 우리는 `string` 대신 재학이라는 값을 타입으로 정의를 해준 것이다.

또 유용한 것은 `as const` 를 써서 전체 객체를 리터럴 타입으로 만들 수도 있다.

```typescript
const myStudent = { name: "Daegu", status: "재학" } as const;

myStudent.name = "SeoulBoy";
myStudent.status = "중퇴";
```

### 새롭게 알게된 점

보통 타입스크립트가 `string`, `number`, `boolean` 등 존재하는 타입을 유추해서 타입을 대입해주는 대신 특정한 타입을 사용하게 해주는 literal type 이라는 것에 대해서 배웠다. 또한 literal type을 이용하여 조금 더 세분화된 값을 타입으로 지정해주는 법도 알았다.
