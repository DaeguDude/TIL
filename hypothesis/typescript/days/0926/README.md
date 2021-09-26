## DAY 18 - 2021/09/26

### ReadonlyArray type

- [The ReadonlyArray type](https://www.typescriptlang.org/docs/handbook/2/objects.html#the-readonlyarray-type)을 읽었는지? O

오늘은 `ReadonlyArray` 타입에 대해서 알게되었다. 말 그대로, 이 값을 건드릴 수 없다는 뜻이다. 이것은 함수형 프로그래밍에서 아주 유용하게 쓰일 것 같다. 왜냐하면, 함수형 프로그래밍의 기본은 [순수 함수](https://en.wikipedia.org/wiki/Pure_function)이고, 순수 함수는 입력값을 변화시키지 않는 것을 기본 원칙으로 하는데, 타입스크립트를 통해서 내가 코드를 짤 때 이 값을 변화시키지 못하도록 강제시켜 줄 수 있는 것이다.

그렇다면 예시를 보면서 한 번 이해를 해보자.
학교에 새로운 학생이 전학을 왔다고 하여보자. 우리는 이미 존재하는 학생들에, 새로운 학생을 추가하려고 하는 것이다.

```typescript
type Student = {
  name: string;
  age: number;
};

function addNewStudent(students: Student[], student: Student) {
  students.push(student);

  return students;
}

const students = [
  { name: "Kim ji seong", age: 10 },
  { name: "park ji seong", age: 11 },
  { name: "lee ji seong", age: 19 },
];

const newStudent = { name: "Park joo ho", age: 15 };

const newStudents = addNewStudent(students, newStudent);
console.log(newStudents === students); // true
```

위의 코드를 보면, 새로운 학생을 추가하고 우리는 새로운 학생을 추가한 결과값을 받았다. 그리고 나서 원래의 학생들이랑 비교를 해봤는데,
왠 걸 둘 다 똑같다고 나온다. **우리는 원래의 배열을 변화시킨 것이고, 이것은 프로그램을 예측하기 힘들게 한다.**

그래서 Typescript에서 `ReadonlyArray`를 사용하여, 원래의 값을 못 건드리게 할 수 있다.

```typescript
type Student = {
  name: string;
  age: number;
};

function addNewStudent(students: ReadonlyArray<Student>, student: Student) {
  students.push(student);
  // Property 'push' does not exist on type 'readonly Student[]'.(2339)

  return students;
}
```

### 새롭게 알게된 점

`ReadonlyArray` 타입을 이용하여서, 배열을 못 건드리게 할 수 있다. 이것을 사용하여
순수함수를 조금 더 많이 사용함으로써 프로그램을 조금 더 예측 가능하게 할 수 있을 듯 싶다!
