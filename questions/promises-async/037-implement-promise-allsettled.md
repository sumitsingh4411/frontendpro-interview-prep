# Implement Promise.allSettled()

**Track:** Promises & async  
**Level:** Medium  
**Time:** about 35 minutes  
**Reported at:** Google, Adobe

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-promise-allsettled)**: free, no account needed.

## Problem

Implement `promiseAllSettled(iterable)` without using `Promise.allSettled`. It returns a promise that **always fulfils**, once every item has settled, with an array of outcome objects in input order:

- `{ status: "fulfilled", value }` for items that fulfilled;
- `{ status: "rejected", reason }` for items that rejected.

```js
const results = await promiseAllSettled([fetchProfile(), fetchFeed(), fetchAds()]);
for (const result of results) {
  if (result.status === "fulfilled") render(result.value);
  else logError(result.reason);
}
```

**Requirements**

- Never reject, even if every item rejects.
- Keep the input order.
- Items may be promises, thenables or plain values; accept any iterable.
- An empty input fulfils with `[]`.

## Starter code

```js
function promiseAllSettled(iterable) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

What would have to change about each item so that it can never reject?

</details>

<details><summary>Hint 2</summary>

Convert each item into a promise that always fulfils with a status object, then collect by index like `Promise.all`.

</details>

<details><summary>Hint 3</summary>

You never call `reject`. Both outcomes map to `{status, value}` or `{status, reason}`, input order is preserved, and an empty input resolves to `[]`.

</details>

## Solution

The full answer is free on UIRound: [Implement Promise.allSettled()](https://frontend.nextjoblist.com/questions/implement-promise-allsettled). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2037%5D%20).
