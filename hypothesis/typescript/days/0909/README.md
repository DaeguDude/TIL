## DAY 1 - 2021/09/09

Typescript는 **정적인 타입 체킹(Static Type Checking)** 시스템이다. 타입스크립트는 코드가 실행되기 전에 코드 내의 값들이나 모양을 통하여 그 특정 코드가 어떠한 행동을 해야하는지 체크하여 버그가 있으면 알려준다.

아래의 예시를 보면 정적인 타입 체킹이라는 말이 무슨 말인지 알 수 있다.

```javascript
function sayName(name: string) {
  console.log(`Hello ${name}!`);
}

sayName(5); // ERROR!
// Argument of type 'number' is not assignable to parameter of type 'string'.(2345)
```

이미 코드가 실행되기 전에 타입스크립트는 우리에게 `name` 은 분명 string을 받아야하는데 number type을 받았다고 알려준다. 코드가 실행되기 전에 체크를 이미해주는 이러한 것을 정적인 타입 체킹 시스템이라 부른다.

그리고 타입스크립트는 컴파일러를 가지고 있다. 그 컴파일러를 통하여서 코드를 변환시켜준다. 그럼 위의 코드를 실행시키면 어떤 코드가 생기는지 확인해보았다.

```shell
tsc hello.ts
```

```javascript
// hello.ts
function sayName(name) {
  console.log(`Hello ${name}`);
}
sayName("Daegudude");

// hello.js
function sayName(name) {
  console.log("Hello " + name);
}
sayName("Daegudude");
```

위와 같이 타입스크립트 컴파일러가 `hello.ts` 파일을 통하여 `hello.js` 파일을 생성하여 주었다! 그리고 코드를 보면 약간 다른 점이 눈에 보인다. 일단 `name: string` 이 사라지고 `name`만 남았다는 점. 이것이 정적인 타입 체킹 시스템이라는 또 하나의 증거다. 실제로 프로그램이 작동하는 자바스크립트 파일에는 웅리 타입스크립트에서 적용해주었던 타입들이 전혀 없는 것이다! 결국, **타입스크립트는 코드가 실행되기 전, 다양한 타입들을 정의를 해둠으로써 우리 코드에 어떤 문제가 있을지 미리 알려주는 정적인 타입 체킹 시스템이다**

### 새롭게 알게된 점

오늘은 타입스크립트가 하는 일이 기본적으로 무엇이고, 정적인 타입 체킹 시스템의 개념에 대해서 새롭게 알게되었다.
