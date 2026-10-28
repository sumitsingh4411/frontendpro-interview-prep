# Implement debounce() with cancel() and flush()

**Track:** JavaScript utilities & FP  
**Level:** Medium  
**Time:** about 35 minutes  
**Reported at:** Tata 1mg, Rippling, Flipkart, Swiggy, Adobe, Oracle

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-debounce-with-cancel-and-flush)**: free, no account needed.

## Problem

Implement `debounce(fn, wait)`. It returns a debounced function that delays calling `fn` until `wait` milliseconds have passed **since the last call**. Every new call restarts the timer, so a burst of calls produces a single call to `fn` with the latest arguments.

The debounced function also has two methods:

- `cancel()`: drop the pending call, if there is one.
- `flush()`: run the pending call **now** and return its result. If nothing is pending, return the result of the last call.

```js
const save = debounce((text) => api.save(text), 500);
input.addEventListener("input", (e) => save(e.target.value));

window.addEventListener("beforeunload", () => save.flush()); // do not lose the last edit
cancelButton.onclick = () => save.cancel();
```

**Requirements**

- Call `fn` with the arguments and `this` of the **latest** call.
- The debounced function returns the result of the last completed call (`undefined` before the first).
- After `fn` has run, the debounced function can be used again.

## Starter code

```js
function debounce(fn, wait = 0) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

Consider what state a debounced function needs to remember between calls, and what each new call should do to it.

</details>

<details><summary>Hint 2</summary>

Keep one timer and the latest args and `this` in a closure; every call clears and restarts the timer, and the timer firing runs `fn`.

</details>

<details><summary>Hint 3</summary>

Use a regular function for the wrapper so `this` works, funnel the real call through one place so `flush` and the timer share it, and return the last result (`undefined` at first).

</details>

## Solution

The full answer is free on FrontendPro: [Implement debounce() with cancel() and flush()](https://frontend.nextjoblist.com/questions/implement-debounce-with-cancel-and-flush). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2026%5D%20).
