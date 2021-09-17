## DAY 9 - 2021/09/17

### non-null assertion

우리는 `radius` 를 optional property로 지정을 해주었다 그래서 있어도 되고 없어도 된다.

```typescript
interface Shape {
  kind: "circle" | "square";
  radius?: number;
  sideLength?: number;
}

function getArea(shape: Shape) {
  return Math.PI * shape.radius ** 2;
  // shape.radius is possibly undefined
}
```

그래서 shape가 undefined일수도 있다고 얘기한다. 지금 우리는 타입스크립트보다 이제 더 많이 정보를 알고있다.
이럴 때는 undefined가 아니라고 non-null assertion을 통하여 해줄 수 있다.

```typescript
interface Shape {
  kind: "circle" | "square";
  radius?: number;
  sideLength?: number;
}

function getArea(shape: Shape) {
  return Math.PI * shape.radius! ** 2;
}
```

그러면 오류가 없어진다.

### 새롭게 알게된 점

[공식문서](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#discriminated-unions)

non-null assertion이라는 것에 대해 알게되었음.
