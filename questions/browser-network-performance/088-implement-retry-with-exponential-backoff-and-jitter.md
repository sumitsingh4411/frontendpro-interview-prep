# Implement retry with exponential backoff and jitter

**Track:** Browser, network & performance  
**Level:** Medium  
**Time:** about 40 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-retry-with-exponential-backoff-and-jitter)**: free, no account needed.

## Problem

Implement two functions:

`computeDelay(attempt, { baseDelay = 100, factor = 2, maxDelay = 10000, jitter = "full", random = Math.random })` returns the wait in ms before retry number `attempt` (0 for the first retry):

- the exponential part is `min(maxDelay, baseDelay * factor ** attempt)`;
- `jitter: "none"` returns it unchanged; `"full"` returns `random() * exp`; `"equal"` returns `exp / 2 + random() * exp / 2`.

`retryWithBackoff(fn, options)` calls the async `fn(attempt)` and retries failures:

- options: `retries = 3` (retries after the first try), the `computeDelay` options, `shouldRetry`, `onRetry(error, attempt, delay)`, `signal`, and `sleep = (ms) => new Promise(…)` (injectable for tests);
- by default, retry network errors (`TypeError`) and errors with `status` 408, 429 or 5xx; never retry other 4xx;
- if an error has `retryAfter` (milliseconds, for example parsed from a `Retry-After` header), wait at least that long;
- stop and reject with `signal.reason` when `signal` is aborted;
- reject with the last error when retries run out.

```js
const data = await retryWithBackoff(() => api.get("/report"), { retries: 5, baseDelay: 200, maxDelay: 5000 });
```

## Starter code

```js
function computeDelay(attempt, { baseDelay = 100, factor = 2, maxDelay = 10000, jitter = "full", random = Math.random } = {}) {
  // Your code here
}

async function retryWithBackoff(fn, options = {}) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

Separate three questions: how long to wait, whether to retry at all, and how to stop early.

</details>

<details><summary>Hint 2</summary>

Compute `min(maxDelay, baseDelay * factor ** attempt)`, apply the jitter mode, take at least `retryAfter` if present, then sleep and loop until the retries run out.

</details>

<details><summary>Hint 3</summary>

Only retry `TypeError`, 408, 429 and 5xx by default, never other 4xx. Inject `random` and `sleep` for tests, reject with `signal.reason` on abort, and reject with the last error at the end.

</details>

## Solution

The full answer is free on UIRound: [Implement retry with exponential backoff and jitter](https://frontend.nextjoblist.com/questions/implement-retry-with-exponential-backoff-and-jitter). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2088%5D%20).
