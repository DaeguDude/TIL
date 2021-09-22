## DAY 13 - 2021/09/22

### readonly 프로퍼티

`readonly` 프로퍼티라는 것이 있다는 걸 알게 되었다. `readonly` 프로퍼티는 말그대로 값을 바꿀 수 없는 프로퍼티를 얘기한다. 당연히 자바스크립트가 실행될 때에는 아무 영향을 미치지는 않지만, 타입 체킹을 할 때는 값이 바뀔 수 없게 정의를 해주는 것이다.

```typescript
interface Administrator {
  readonly name: string;
}

function changeName(obj: Administrator) {
  console.log(`his name is ${obj.name}`);

  obj.name = "Admin Lee";
}
//Cannot assign to 'name' because it is a read-only property.(2540)
```

### 새롭게 알게된 점

`readonly` 프로퍼티라는 것이 있다는 것을 알게되었다. 그런데 어디에 쓰일지는 잘 모르겠다...! ㅎㅎ
