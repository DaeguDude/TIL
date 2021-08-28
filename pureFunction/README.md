## Pure Function

What is a pure function? How can I use them?
What is the benefit of them and why we need to use them.

Pure function is a function that doesn't create a side effect. Which means, if same arguments are passed in, it will always return the same result.

Take a look at this following example.

```javascript
function add(num1, num2) {
  return num1 + num2;
}

add(2, 2); // 4
for (let i = 0; i < 10000; i++) {
  console.log(add(2, 2));
}

// 4
// 4
// 4... 10000 times
```

Take a moment to look at the code above. We are calling `add` function 10000 times, and it will always produce the same result because it doesn't depend on any external source such as variables.

Why is it good? Because the result is always expectable so it is more maintainable.

Let's take a look at 'impure' function. And why it might be not a good idea to use them.

```javascript
const people = [
  { name: "John", age: 51 },
  { name: "Matthew", age: 32 },
  { name: "Michael", age: 30 },
  { name: "Kim", age: 66 },
  { name: "Park", age: 70 },
];

function getPeopleOverFifty() {
  return people.filter((person) => person.age > 50);
}
```

If you see the code above, the function `getPeopleOverFifty` is not pure. Why? Because it is dependant on the variable that is outside the function. Which will make the result not expectable. You will run the code, and you don't know what it will return. If somehow the value in people changes, it will return different result.

We can make this 'impure' function to 'pure' function.

```javascript
function getPeopleOverFifty(people) {
  return people.filter((person) => person.age > 50)
}

const groupOne = { name: "John", age: 51 }, { name: "Matthew", age: 32 },

const groupTwo = { name: "Michael", age: 30 },
  { name: "Kim", age: 66 },

getPeopleOverFifty(groupOne) // { name: "John", age: 51 }
getPeopleOverFifty(groupTwo) // { name: "Kim", age: 66 }
```

See how this pure function takes an array of people and uses it to filter people that are over 50? In this way, whatever input is passed in, it will always produce the same result. Pure function can't depend on outside variables.

## So Why is it important?

Pure function is important because it reduces the possibility of unexpected error in your code.

And there are other reasons. Testability. If your function is pure you can immediately test them.

Let's try to test pure function and impure function and what differences there are.

```javascript
// getVAT.js
function getValueAddedTax(tax, price) {
  return price + price * tax;
}

// getVAT.test.js
import { getValueAddedTax } from "./getVAT";

describe("getValueAddedTax", () => {
  test("Calculates price after VAT correctly", () => {
    expect(getValueAddedTax(0.1, 100)).toBe(110);
    expect(getValueAddedTax(0.05, 100)).toBe(105);
    expect(getValueAddedTax(0.2, 100)).toBe(120);
  });
});

/** 
PASS  src/practice/getVAT.test.js
  getValueAddedTax
    ✓ Calculates price after VAT correctly (1 ms)
*/
```

```javascript
// getVAT.js
const tax = 0.1;

function getValueAddedTax(price) {
  return price + price * tax;
}

// getVAT.test.js
describe("getValueAddedTax", () => {
  test("Calculates price after VAT correctly", () => {
    expect(getValueAddedTax(100)).toBe(110);
    expect(getValueAddedTax(100)).toBe(105); // fail
    expect(getValueAddedTax(100)).toBe(120); // fail
  });
});
```

Here, the test code of impure function, you see how the function is confined to just calculate what fixed value of text, whether makes it less flexible? And also, you are not too sure what it will return since it depends on the `tax` variable. What if it changes to `0.2`? We will have to rewrite our test code...That's very redundant work.

So it seems like it's good to write pure function when it's 'possible'. Not all code can be written in pure function.
