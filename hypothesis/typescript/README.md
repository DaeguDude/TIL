# Typescript 실험

Developer Tea 팟캐스트를 듣다가 엄청나게 [흥미로운 Episode(Use your Expectation as a tool)](https://developertea.com/episodes/ced78f5e-317d-4411-be97-f760cadbccf4)가 있었다. 무엇이였냐하면은 보통 우리는 항상 목표(Goal)를 세운다. 목표를 세우는 것은 아주 좋다. 하지만 대부분은 목표를 세우고 그 목표를 달성하지 못한다. 팀으로 진행하는 것이 아니라면.... 그 이유는 아마도 혼자서 하면 동기부여가 잘 되지않기도 하고 꼭 지켜야할 약속이 아니기 때문에 우선순위에서 밀려나는 것이다.

이렇게 하면 안 좋은 점이 어떤 것이냐 하면은, 보통 우리는 목표를 달성하지 못하였을 때 목표를 달성한 원인(증거)을 찾으려 하지않고 그냥 흘려 보내거나 자기 자신을 탓하기 마련이다. 예를 들어, "아 나는 항상 이런식이야" 아니면 "아 난 왜이러지?" 등등의 말이다. 이것은 어떻게 보면 당연하다. 원인을 찾으려 노력을 하는 것보다 내가 끈기가 없어서라고 결론을 내리는 것이 뇌의 관점에서 훨씬 쉽기 때문이다.

그래서 이 에피소드에서는 새로운 것을 제안을 한다. 목표를 세우기 보다는 가설을 세우는 것이다. 가설은 무엇인가?

> 과학적 자료들에 근거하여 논리적으로 유추하여 설정한 것이므로 개연성을 떠나 아무런 과학적 근거도 없이 자의적으로 꾸며내는 억측과는 구별된다. 그 예측이 옳다는 것이 논리적으로 그리고 실험적으로 증명될 때에는 확고한 정설로, 과학적 학설로 된다.

즉, 가설은 실험이다. 실험은 **자료**에 기반하여서 어떠한 예측을 증명해내는 과정이다. 즉슨, 목표를 세우고 그 목표를 달성했는지 안 달성했는지에 대한 '결과'에만 중점을 두는 것이 아니라 그 특정한 **과학적 근거** 를 통해 **기대값**을 유추하는 것이다. 이것은 조금 더 근거와 자료에 중점이 맞추어져 있다. 실험과정에 중점을 두는 것이다.

이것은 왜 유용할까? 이렇게 하면 당신이 어떠한 기대값을 두고, 그 기대값이 옳거나 옳지 않았을 때 결론을 그냥 지어버리기 보다는 왜 그 기대값이 옳지 못 했는지 아니면 왜 옳았는지에 대한 근거와 자료들을 볼 것이기 때문이다. 예를 들어서 당신이 살을 빼고 싶다고 하자. '나는 100일만에 5kg를 뺄 것이야' 라고 목표를 설졍하면, 그것을 달성하기 위한 행위에 초점을 덜 두게 된다. 하지만 '1주일에 5번 30분씩 운동을 하고 매일 저녁 7시 이후에는 아무것도 먹지 않는다면(근거) 5kg가 빠질 것이다(기대값)' 이라는 가설을 세운다면, 100일 이후에 그것을 달성하였다면, 그 근거가 사실이 되는 것이고 또한 당신은 원했던 바까지 달성을 한 것이 된다. 만약에 그 기대값이 옳지 않았다고 나오더라도, 당신은 운동을 했던 기록(자료)들을 살펴보며 '왜' 기대값이 옳지 않았는지 원인을 찾을 수 있게 되고 다음 번에는 조금 더 나은 계획과 실험을 할 수 있을 것이다.

이러한 논리에 기반하여, 나는 새로운 실험을 해보고 싶다. 요즈음에 나는 Testing에 관심이 있다. 그리고 Testing을 잘 사용하고 싶다. 그래서 테스팅을 살펴보던 중 Kent C Dodd의 [블로그 글 - How to add testing to an existing project](https://kentcdodds.com/blog/how-to-add-testing-to-an-existing-project)이 생각이 났다. Testing에 가장 기본이 될 수 있는 것이 정적인 testing(Prettier, ESLint, Typescript)이라고 한다. 뭐든지 시작할 때 기본을 세우는 것이 중요하다고 생각한다. 그래서 나는 Testing의 기본이 되는 Typescript, 여기에 대해서 실험을 1달동안 해보려고 한다.

### Typescript 실험

- 1달 동안 매일 Typescript에 대해 새롭게 알게된 점을 정리를 하고 TIL에 올린다. (단, 이 새롭게 알게된 개념이 Typescript의 Documentation에 있다면 읽었던 말았던 한 번 더 읽는다)
- Typescript 공식문서를 2번 정독한다.

귀무가설: 위의 2 조건을 충족하였을 시 Typescript를 조금 더 잘 할 수 있다.
대립가설: 위의 2 조건을 충족하여도 Typescript를 조금 잘 할 수 없다.

**'조금 더 잘한다' 라는 것을 어떻게 정량화할까?**

- Typescript Documentation에 나오는 개념들을 보며 이해하고 예제(코드)로 설명할 수 있다.
- TypeScript에 나오는 개념들을 사용하여 실제 프로젝트를 진행할 수 있다 혹은 진행했다.(지금 내가 사용할 수 있는 기본적인 개념들을 정리해보자, 그리고 마지막에 비교를 하면 될 것. 내가 어떤 개념들을 사용하며 프로젝트에 실제 적용을 하고 있는지)

## 자료

### Typescript 공식문서 2회 독파

#### 정리

- 실험목표: 2회독파
- 실제 읽은 양: 1회 75%
- 달성률: 37.5%

---

Typescript 기본적인 공식문서는 [Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)이다. Handbook은 아래와 같이 이루어져 있고, 내가 읽은 자료는 다음과 같다.

- [The Typescript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html) 09/09
- [The Basics](https://www.typescriptlang.org/docs/handbook/2/basic-types.html) 09/09
- [Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html) 09/10~09/12
- [Narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html) 09/14~09/18
- [More on Functions](https://www.typescriptlang.org/docs/handbook/2/functions.html) 09/19~09/21
- [Object Types](https://www.typescriptlang.org/docs/handbook/2/objects.html) 09/22~09/27

- **Type Manipulation**

  - [Creating Types from Types](https://www.typescriptlang.org/docs/handbook/2/types-from-types.html) 10/02
  - [Generics](https://www.typescriptlang.org/docs/handbook/2/generics.html) 10/02
  - [Keyof Type Operator](https://www.typescriptlang.org/docs/handbook/2/keyof-types.html) 10/02
  - [Typeof Type Operator](https://www.typescriptlang.org/docs/handbook/2/typeof-types.html) 10/02
  - [Indexed Access Types](https://www.typescriptlang.org/docs/handbook/2/indexed-access-types.html) 10/02
  - [Conditional Types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html) 10/05
  - [Mapped Types](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html) 10/06
  - [Template Literal Types](https://www.typescriptlang.org/docs/handbook/2/template-literal-types.html) 10/06

- [Classes](https://www.typescriptlang.org/docs/handbook/2/classes.html)
- [Modules](https://www.typescriptlang.org/docs/handbook/2/modules.html)

일단 실험을 할 당시 충족을 해야 했던 공식문서 2회를 독파하지 못했다.
위의 카테고리가 9개 있다고 가정을 했을 때, 7 가지의 카테고리는 다 읽었다. 공식 문서 1회 독파의 75% 정도는 했다고 볼 수 있다.

## 1일 1 몰랐던 Typescript 정리

이번 실험을 하면서 또 하나의 요건인 타입스크립트의 몰랐던 개념을 하루에 한 개씩 정리하는 것이었다.

#### 정리

- 실험목표 총 일수: 31일
- 정리를 한 일수: 22일
- 달성률: 70%

---

- **Day1** 09/09 [타입스크립트는 정적인 타입체킹 시스템이다](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0909)
- **Day2** 09/10[Type Annotation과 Contextual Typing](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0910) 09/10
- **Day3** 09/11 [Type Alias](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0911)
- **Day4** 09/12 [Literal Types](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0912)
- **Day5** 09/13 [Extending Union Type](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0913)
- **Day6** 09/14 [Generic이란](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0914)
- **Day7** 09/15 [e.target에 value property가 없다고?](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0915)
- **Day8** 09/16 [ReturnType, 넌 누구냐](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0916)
- **Day9** 09/17 [non-null assertion](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0917)
- **Day10** 09/18 [Discriminated Union](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0917)
- **Day11** 09/19 [Function Type Expression](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0919)
- **Day12** 09/20 [never를 사용해](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0920)
- **Day13** 09/21 [useState의 타입](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0921)
- **Day14** 09/22 [readonly 프로퍼티](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0922)
- **Day15** 09/23 [Type 상속(extend)받기](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0923)
- **Day16** 09/24 [property 'x' does not exist on union type](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0924)
- **Day17** 09/25 [Type 'string' is not assignable to union type, but it exists in union type](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0925)
- **Day18** 09/26 [ReadonlyArray Type](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0926)
- **Day19** 09/27 [Tuple Types](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/0926)
- **Day20** 09/28 x
- **Day21** 09/29 x
- **Day22** 09/30 x
- **Day23** 10/01 x
- **Day24** 10/02 [Generic Constraints, 재밌는 녀석이군!](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/1002)
- **Day25** 10/03 x
- **Day26** 10/04 x
- **Day27** 10/05 [keyof type operator, 너 아주 유용할 것 같아](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/1005)
- **Day28** 10/06 [Conditional Type, 넌 누구냐?](https://github.com/DaeguDude/TIL/tree/main/hypothesis/typescript/days/1006)
- **Day29** 10/07 x
- **Day30** 10/08 x
- **Day31** 10/09 x

## 실험결과

### Typescript Documentation에 나오는 개념들을 보며 이해하고 예제코드로 설명할 수 있다.

아주 정확하게 하는 것은 불가능 할 것 같고, 기본적으로 크게 3가지로 나누어 보았다.
**A** - 개념을 보고 이해하고 예제코드로 설명가능
**B** - 개념을 대충 이해하고 있고 **공식문서를 참조**하면 예제코드로 설명가능
**C** - 이해를 못하고 있고 설명도 할 수 없음

### 정리

총 40개의 개념

- A - 15
- B - 13
- C - 12

기본적으로 정리를 하자면, Typescript에 대한 개념이 전반적으로 아주 상승했다고 볼 수 있다.

**The Basics**

- **A** - Static Type checking에 대해서 설명할 수 있는지?

Everyday Types

- **A** - primitive types
- **A** - Object Types
- **A** - Union Types
- **A** - Type alias
- **A** - Interface
- **B** - Type Assertion
- **A** - Literal Types
- **C** - Enum

Narrowing

- **A** - typeof type guards
- **A** - Truthiness narrowing
- **A** - Equality narrowing
- **A** - The in operator narrowing
- **B** - Control flow analysis
- **C** - Type predicates
- **C** - Discriminated Unions
- **C** - never type

More on functions

- **B** - Function type expressions
- **C** - Call Signatures
- **C** - Construct Signatures
- **B** - Generic Functions
- **A** - Optional Parameters
- **C** - Function Overloads
- **B** - Rest parameters and arguments
- **A** - Parameter destructuring

Object Types

- **B** - Property Modifiers
- **B** - Index signature
- **B** - Extending Types
- **C** - Intersection Types
- **A** - Generic Object Types

Creating Types from Types
Generics

- **A** - Generic Types
- **C** - Generic Classes
- **B** - Generic Constraints

Keyof Type Operator

- **B** - the keyof type operator

Typeof Type operator

- **B** - the typeof type operator

Indexed Access Types

- **B** - indexed Access Types

Conditional Types

- **B** - Conditional Type constraints
- **C** - Distributive Conditional Types

Mapped Types

- **C** - mapped types

Template literal Types

- **C** - template literal types

### Typescript에 나오는 개념들을 사용하여 실제 프로젝트를 진행할 수 있다.

실제로 Typescript에 나오는 개념들을 사용하여 실제 프로젝트를 진행하고 있는지?

실제로 위의 개념 40개 중에, 나는 11개 정도를 프로젝트에서 사용을 하고 있다. 여기서 재밌는 점은 아주 기본적인 개념의 비중이 크고, 조금 더 고급된 개념은 실제로 사용을 하고 있지 못하다.

- primitive types
- Union Types
- Type Alias
- Interface
- Literal Types
- typeof type guards
- Truthiness narrowing
- Equality narrowing
- The in operator narrowing
- Optional Parameters
- Extending Types

**Typescript Documentation에 나오는 개념들을 보며 이해하고 예제로 설명을 할 수 있다**

이 능력은 이번의 실험을 통해서 많이 올라간 것 같다. 새로운 개념을 배울 수 있게 되었고 이것을 설명을 할 수 있는 능력도 올라갔다.

**Typescript에 나오는 개념들을 실제 프로젝트에 사용할 수 있다**

이 부분에 대해서는 약간의 의문이 생긴다. 위의 사용하는 11가지 중, Union Type, Extending Type 말고는 실제로 내가 이미 알고있었던 개념이라 볼 수 있기 때문이다. 그렇기 때문에, 여기에 대한 능력은 상승이 거의 없었다고 볼 수 있다.

총 정리를 하자면... Typescript에 대한 이해도는 많이 올라갔다고 할 수 있지만 이것을 실제로 사용하는 능력을 크게 올라갈 수 있다고 할 수 없다. 그렇기 때문에 아래의 가설 중 하나를 택해야 된다면...

- 귀무가설: 1달 동안 매일 Typescript에 대해 새롭게 알게된 점을 정리를 하고, Typescript 문서를 2회 독파하면 Typescript를 더 잘 할 수 **있다**.
- 대립가설: 1달 동안 매일 Typescript에 대해 새롭게 알게된 점을 정리를 하고, Typescript 문서를 2회 독파하면 Typescript를 더 잘 할 수 **없다**.

귀무가설을 기각하고 대립가설을 채택을 하고 싶다. 타입스크립트에 대한 이해도는 높아졌지만, 이것을 더 잘 한다 라기보다는 잘 알게 되었다라는 개념이 맞는 것 같다.
여기서 또 하나 참고해야 될 점은, 내가 실험의 요건을 충족하지 못했다는 것도 알고 있어야 할 것 같다. 잘 알게 되었으므로, 이것이 잘 할 수 있음의 초석이 될지 말지는 나도 잘 모르겠지만 될 것은 같다.

## 느낀 점 && 참조할 점

이번 실험을 진행하면서 느낀 점을 정리해보자면, 일단 매일매일 정리를 한다는 것은 거의 불가능에 가까웠다. 정리를 하는데 기본적으로 30분~1시간이 걸렸고 1시간은 거의 내가 하루에 공부를 할 수 있는 맥시멈 시간이였으므로 이것은 아주 힘들었다. 또한, 공식문서를 읽을 때 새로운 것을 배우는 것은 아주 좋았다. 내가 모르는 개념들을 알게되는 것이 아주 좋았는데, 이 개념을 실제로 적용을 해보지 않으니 실제로 사용을 할 수는 없었던 것 같다. 실제로 사용을 한다는 것이 얼마나 중요한 지 알 수 있었던 것 같다.

다음 실험을 할 때는 조금 더 이 부분에 초점을 맞추어야 할 것 같다.

- 1달 동안 매일 휴식없이 어떤 것을 한다는 것은 지속가능성이 크지 않다. 결국 더욱 더 쫓기는 상황이 발생한다. 내가 31일에 22일을 했는 것을 봤을 때, 1주일에 5회가 제일 적당할 듯 싶다. 왜 이것이 지속가능성이 없다는 것을 보여주냐면 실제로 Day19까지는 한 번도 빼먹지 않고 다 하였다. 하지만, Day 20에서 Day 31일에서, 총 11회 중에 3회밖에 하지않았다. 결국 꾸준해지지 못하는 것이다.
- 문서를 읽는 것은 실제로 이해를 높이는 데 아주 도움이 된다. 하지만, 사용을 하지 않는다면 내것으로 만들지 못한다. 결국 사용을 하는 방법을 찾아야 한다. 다음 실험에는 조금 더 내가 실제로 **사용할 수 있음**에 초점을 맞추는 것이 어떨 까 싶다.
