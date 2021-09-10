## DAY 2 - 2021/09/10

### Typescript Annotation

타입스크립트는 기본적으로 값을 보고 어떠한 타입인지를 알아서 정의를 해준다.

예를 들어서 아래의 코드를 보면 `myStudent` 가 자동으로 `string` 타입으로 정의가 되는 것을 볼 수 있다.

```typescript
const myStudent = "Daegudude";
// myStudnet: string
```

이것을 타입스크립트에서는 Type Annotation 이라고 얘기를 한다.
그렇기 때문에 타입스크립트 문서에서는 변수 이름에 타입을 붙여주지 않기를 권장한다. 왜냐하면 자동적으로 타입이 정의가 되기 때문이다.

또한, 타입스크립트에서는 보통 `return` 타입을 설정하여 줄 필요가 없다고 얘기를 한다. ???? 음... 내 생각에는 `return` 타입을 지정하여주고, 코드를 짜기 시작하면 `return` 타입이 다를 때 코드가 틀렸다고 얘기를 해줄 것 같았는데 그건 아닌가보다.

한 번 코드를 통해 확인하여볼까?

```typescript
type Student = {
  name: string;
  age: number;
};

function returnStudentAge(student: Student): number {
  return studnet.name; // number를 지정하여주었기 때문에 오류가 뜸
}
```

어, 신기하게도 나의 생각과 같이 `return` 타입을 지정하여 주면, 그 코드가 내가 지정한 타입의 `return` 값을 안 돌려주면 오류를 되돌려 주기는 한다. 하지만 자주 안 사용한다고 하니까 일단 그렇게 알고는 있어야겠다. 내가 위에서 설명한 상황을 잘 쓰지는 않는 거겠지.

### Contextual Typing

타입스크립트에는 Contextual Typing 이라는 것이있다. 특정한 문맥에 따라서 타입스크립트가 타입을 지정하여 주는 것이다. 예를 들어 아래의 코드를 보자.

```typescript
const cities = ["daegu", "seoul", "busan", "newyork"];

cities.forEach((city) => {
  city.tolowerCase();
  // Property 'tolowerCase' does not exist on type 'string'. Did you mean 'toLowerCase'?(2551)
});
```

여기서 `city`의 특정한 타입을 우리가 지정하여 주지 않았지만 자동적으로 `string` 이라는 것을 알고 `string`에는
`tolowerCase`가 존재하지 않는다고 타입스크립트가 똑똑하게 얘기해주었다. 이것을 contextual typing 이라고 한다.
왜냐하면 문맥에 맞게 타입을 정의하여 주기 때문이다.

### 새롭게 알게된 점

오늘은 타입스크립트에서 기본적으로 값을 읽고 정의해주는 것을 Type Annotation 이라고 부른다는 것을 알게 되었다. 또한 특정 문맥에 따라서 값을 지정해주는 것을 Contextual Typing 이라고 한다는 것을 배웠다.
