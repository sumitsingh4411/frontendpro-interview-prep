# Predict the event-loop order of setTimeout, promises, queueMicrotask and await

**Track:** JavaScript fundamentals  
**Level:** Easy  
**Time:** about 15 minutes  
**Reported at:** Microsoft, Meesho

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/predict-the-event-loop-order-of-settimeout-promises-queuemicrotask-and-await)**: free, no account needed.

## Problem

Interviewers love this one: read each snippet and write down the exact order of the logs, **without running it**. Fill in `answers.a`, `answers.b` and `answers.c` with the logged strings, in order.

```js
// Snippet A
function snippetA(log) {
  log("1");
  setTimeout(() => log("2"), 0);
  Promise.resolve().then(() => log("3"));
  queueMicrotask(() => log("4"));
  log("5");
}

// Snippet B
async function snippetB(log) {
  async function inner() {
    log("a");
    await null;
    log("b");
  }
  log("start");
  setTimeout(() => log("timeout"), 0);
  inner().then(() => log("inner done"));
  Promise.resolve()
    .then(() => log("then 1"))
    .then(() => log("then 2"));
  log("end");
}

// Snippet C
function snippetC(log) {
  Promise.resolve()
    .then(() => {
      log("A1");
      return Promise.resolve("x");
    })
    .then(() => log("A2"));
  Promise.resolve()
    .then(() => log("B1"))
    .then(() => log("B2"))
    .then(() => log("B3"))
    .then(() => log("B4"));
}
```

Then be ready to explain *why*, one rule per step.

## Starter code

```js
const answers = {
  a: [],
  b: [],
  c: [],
};
```

## Hints

<details><summary>Hint 1</summary>

Three queues decide the order: the synchronous call stack, the microtask queue and the timer queue. Place each callback in its queue as it is scheduled.

</details>

<details><summary>Hint 2</summary>

Run all synchronous code first, then drain every microtask (including ones added while draining), and only then take the next timer. Treat `await` as a continuation queued as a microtask.

</details>

<details><summary>Hint 3</summary>

Snippet C trips people up: returning a promise from a `then` handler makes the chain take extra microtask ticks, so the other chain's logs interleave with it. Count ticks carefully.

</details>

## Solution

The full answer is free on UIRound: [Predict the event-loop order of setTimeout, promises, queueMicrotask and await](https://frontend.nextjoblist.com/questions/predict-the-event-loop-order-of-settimeout-promises-queuemicrotask-and-await). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20151%5D%20).
