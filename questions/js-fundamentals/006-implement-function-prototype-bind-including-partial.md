# Implement Function.prototype.bind(), including partial arguments

**Track:** JavaScript fundamentals  
**Level:** Easy  
**Time:** about 15 minutes  
**Reported at:** Rippling, Salesforce, Walmart Global Tech, Flipkart

**[Solve it in the browser with tests](https://uiround.com/questions/implement-function-prototype-bind-including-partial)**: free, no account needed.

## Problem

Implement `Function.prototype.myBind(thisArg, ...boundArgs)` without using the built-in `bind`. It returns a **new function** that, when called, runs the original with `this` set to `thisArg` and with `boundArgs` placed before any arguments passed later.

```js
function volume(l, w, h) {
  return l * w * h * this.scale;
}
const scaled = volume.myBind({ scale: 2 }, 3); // l is fixed to 3
scaled(4, 5); // 3 * 4 * 5 * 2 = 120
```

**Requirements**

- Support partial application: arguments given to `myBind` come first, call-time arguments after them.
- The bound `this` cannot be changed later, for example by calling the bound function as a method of another object.
- When the bound function is used with `new`, ignore the bound `this` and construct a normal instance of the original function.
- Throw a `TypeError` when `myBind` is called on something that is not a function.

## Starter code

```js
Function.prototype.myBind = function (thisArg, ...boundArgs) {
  // Your code here
};
```

## Hints

<details><summary>Hint 1</summary>

Think about what a bound function must remember, and what it must do differently when called with `new`.

</details>

<details><summary>Hint 2</summary>

Return a closure that captures the function, `thisArg` and bound args, and calls the original with bound args followed by call-time args.

</details>

<details><summary>Hint 3</summary>

When the wrapper is called with `new`, the bound `this` must be ignored and the instance should still pass `instanceof` for the original, so mind `new.target` and the prototype.

</details>

## Solution

The full answer is free on UIRound: [Implement Function.prototype.bind(), including partial arguments](https://uiround.com/questions/implement-function-prototype-bind-including-partial). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%206%5D%20).
