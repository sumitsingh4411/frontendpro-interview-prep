# Implement throttle() with leading and trailing options

**Track:** JavaScript utilities & FP  
**Level:** Medium  
**Time:** about 35 minutes  
**Reported at:** Rippling, Razorpay, Adobe

**[Solve it in the browser with tests](https://uiround.com/questions/implement-throttle-with-leading-and-trailing-options)**: free, no account needed.

## Problem

Implement `throttle(fn, wait, { leading = true, trailing = true } = {})`. The throttled function calls `fn` **at most once per `wait` milliseconds**, however often it is called.

- `leading: true` calls `fn` immediately on the first call of a quiet period.
- `trailing: true` makes sure the **last** call made during a waiting period is not lost: `fn` runs with its arguments when the period ends.

Also add `cancel()`, which drops any pending trailing call.

```js
const onScroll = throttle(() => updateProgressBar(), 100);
window.addEventListener("scroll", onScroll);
```

**Requirements**

- Call `fn` with the arguments and `this` of the call that triggered it.
- A trailing call starts a new waiting period, so two calls are never closer than `wait` apart.
- With `leading: false`, the first call only schedules a trailing call.
- If nothing was called during a waiting period, no trailing call happens.

## Starter code

```js
function throttle(fn, wait, { leading = true, trailing = true } = {}) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

Think of the throttle as being in one of two states, idle or waiting, and ask what each call should do in each.

</details>

<details><summary>Hint 2</summary>

When idle, run immediately (if leading) and start a wait timer; while waiting, just remember the latest args. When the timer ends, run the trailing call if one is pending.

</details>

<details><summary>Hint 3</summary>

A trailing call begins a new waiting period so calls are never closer than `wait`. With `leading: false` the first call only schedules, and no trailing call happens if nothing was called.

</details>

## Solution

The full answer is free on UIRound: [Implement throttle() with leading and trailing options](https://uiround.com/questions/implement-throttle-with-leading-and-trailing-options). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2027%5D%20).
