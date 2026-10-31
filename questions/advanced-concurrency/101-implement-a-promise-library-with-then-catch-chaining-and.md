# Implement a Promise library with .then(), .catch(), chaining, and asynchronous handler scheduling

**Track:** Advanced async concurrency  
**Level:** Hard  
**Time:** about 60 minutes  
**Reported at:** Microsoft, Uber, Google

**[Solve it in the browser with tests](https://uiround.com/questions/implement-a-promise-library-with-then-catch-chaining-and)**: free, no account needed.

## Problem

Implement `class MyPromise` that follows the Promises/A+ rules, without using the built-in `Promise` anywhere in your implementation:

- `new MyPromise((resolve, reject) => …)`: the executor runs synchronously; if it throws, the promise rejects. A promise settles **once**; later calls are ignored.
- `then(onFulfilled, onRejected)` returns a **new** promise. Handlers run **asynchronously** (in a microtask, use `queueMicrotask`), in the order they were registered, even if the promise is already settled.
- A handler's return value resolves the next promise; a thrown error rejects it. Missing handlers pass values and errors through.
- **Resolution procedure**: resolving with a thenable (any object or function with a `then` method) adopts its state; resolving a promise with **itself** rejects with a `TypeError`; a thenable's callbacks are honoured only once.
- `catch(onRejected)`, `finally(onFinally)` (runs on both outcomes, passes the original value or error through unless it throws), and static `MyPromise.resolve` and `MyPromise.reject`.

```js
new MyPromise((resolve) => setTimeout(() => resolve(2), 10))
  .then((n) => n * 10)
  .then((n) => { throw new Error(`too big: ${n}`); })
  .catch((e) => e.message)
  .finally(() => console.log("done"))
  .then(console.log); // "too big: 20"
```

## Starter code

```js
class MyPromise {
  constructor(executor) {
    // Your code here
  }

  then(onFulfilled, onRejected) {}

  catch(onRejected) {}

  finally(onFinally) {}

  static resolve(value) {}

  static reject(reason) {}
}
```

## Hints

<details><summary>Hint 1</summary>

A promise is a small state machine plus a list of waiting continuations. Think about who is allowed to move it out of pending.

</details>

<details><summary>Hint 2</summary>

`then` creates a child promise and queues a continuation that runs in a microtask, then feeds the handler result through a resolution procedure that adopts thenables.

</details>

<details><summary>Hint 3</summary>

Settle only once, run handlers asynchronously even on settled promises, and reject on self-resolution with `TypeError`. `finally` passes the original outcome through unless the callback throws.

</details>

## Solution

The full answer is free on UIRound: [Implement a Promise library with .then(), .catch(), chaining, and asynchronous handler scheduling](https://uiround.com/questions/implement-a-promise-library-with-then-catch-chaining-and). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20101%5D%20).
