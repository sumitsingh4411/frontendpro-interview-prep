# Implement a fetch wrapper with timeout and AbortController

**Track:** Browser, network & performance  
**Level:** Medium  
**Time:** about 35 minutes

**[Solve it in the browser with tests](https://uiround.com/questions/implement-a-fetch-wrapper-with-timeout-and-abortcontroller)**: free, no account needed.

## Problem

`fetch` has no timeout: on a bad network a request can hang for minutes. Implement `fetchWithTimeout(url, { timeout = 8000, signal, ...options } = {})`:

- It calls `fetch(url, options)` and resolves with the `Response`.
- If the request takes longer than `timeout` ms, it **aborts the request** and rejects with an error whose `name` is `"TimeoutError"`.
- If the caller passes their own `signal` and aborts it, the request is aborted and the promise rejects with that signal's reason (an `AbortError` by default), so callers can tell "cancelled" from "timed out".
- It cleans up: the timer is cleared and the listener on the caller's signal is removed when the request finishes, however it finishes.

```js
const controller = new AbortController();
cancelButton.onclick = () => controller.abort();

try {
  const res = await fetchWithTimeout("/api/report", { timeout: 5000, signal: controller.signal });
  render(await res.json());
} catch (error) {
  if (error.name === "TimeoutError") showToast("The server is slow, please retry");
  else if (error.name !== "AbortError") throw error;
}
```

## Starter code

```js
async function fetchWithTimeout(url, { timeout = 8000, signal, ...options } = {}) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

`fetch` can only be cancelled through a signal. How do you cancel it from two different sources, a timer and the caller?

</details>

<details><summary>Hint 2</summary>

Create one `AbortController`, abort it with a `TimeoutError` reason from a timer, and forward the caller's signal abort into it.

</details>

<details><summary>Hint 3</summary>

Clear the timer and remove the listener on the caller's signal in `finally`, and throw the abort reason so callers can tell `TimeoutError` from `AbortError`. Handle an already-aborted signal.

</details>

## Solution

The full answer is free on UIRound: [Implement a fetch wrapper with timeout and AbortController](https://uiround.com/questions/implement-a-fetch-wrapper-with-timeout-and-abortcontroller). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2086%5D%20).
