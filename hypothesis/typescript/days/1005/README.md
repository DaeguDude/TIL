## DAY 26 - 2021/10/05

### keyof type operator, 아주 유용할 것 같아~

오늘은 새롭게 `keyof` 타입 연산자 라는 녀석을 배웠다. 이것이 하는 것은 객체 타입을 받아, 그 객체타입의 키를 이용하여 union 타입을 생성해 주는 것이다.

```typescript
interface Student {
  name: string;
  height: number;
  age: number;
}

type OneOfStudentKeys = keyof Student;

function sayStudentProperty(student: Student, property: OneOfStudentKeys) {
  console.log(student.property);
}

const myStudent = {
  name: "sung ki hoon",
  height: 180,
  age: 47,
};
sayStudentProperty(myStudent, "classRoom");
// Argument of type '"classRoom"' is not assignable to parameter of type 'keyof Student'.(2345)

sayStudentProperty(myStudent, "height"); // okay
```

위에서, `sayStudentProperty` 함수는 `Student` 타입을 받아주고, 프로퍼티로는 `Stduent` 타입의 키를 받아준다. 그래서 `classRoom`이라는 `Stduent` 타입에 존재하지 않는 프로퍼티를 넘겨주면 에러를 일으키는 것이다.

이것은 아주 유용하게 쓰일 것 같다. 예를 들어 정렬을 하는 함수를 만들었다고 해보자.

```typescript
interface Student {
  name: string;
  height: number;
  age: number;
  classRoomNumber: number;
}

// NOTE: 실제 예시문이 추가된 코드를 올리자
function sortStudentsByProperty(students: Student[], property: keyof Student) {
  if (typeof property === "string") {
    // 알맞는 정렬을 해줌
  } else if (typeof property === "number") {
    // 알맞는 정렬을 해줌
  }
}
```

위와 같이 해주면, 우리는 `sortStudentsByProperty` 함수를 쓸 때, 실제로 `Student에` 존재하는 프로퍼티만 넘기게 할 수 있고, 정렬도 그에 맞게 올바르게 해 줄 수 있다!

### 새롭게 알게된 점

객체 타입을 받아 객체 타입의 키를 이용해 유니언 타입을 만들어주는 `keyof` 타입 연산자에 대해서 알게되었다.
