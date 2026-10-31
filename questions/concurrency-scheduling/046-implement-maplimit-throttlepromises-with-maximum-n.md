# Implement mapLimit() / throttlePromises() with maximum N concurrent tasks

**Track:** Concurrency & scheduling  
**Level:** Medium  
**Time:** about 35 minutes  
**Reported at:** Rippling, Uber, Flipkart

**[Solve it in the browser with tests](https://uiround.com/questions/implement-maplimit-throttlepromises-with-maximum-n)**: free, no account needed.

## Problem

Implement `mapLimit(items, limit, mapper)`. It calls the async `mapper(item, index)` for every item, but **never runs more than `limit` calls at the same time**. It resolves with the results in input order.

```js
// Upload 200 photos, at most 4 at a time.
const urls = await mapLimit(photos, 4, (photo) => upload(photo));
```

**Requirements**

- At most `limit` mapper calls are in flight at any moment, and a new call starts as soon as one finishes.
- Results keep the input order.
- Reject as soon as one call fails, and **do not start any new calls** after that.
- A synchronous throw in `mapper` counts as a failure.
- `limit` must be at least 1; otherwise reject with a `RangeError`. An empty input resolves to `[]`.

## Starter code

```js
function mapLimit(items, limit, mapper) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

Picture a fixed number of workers. What should each one do the moment it finishes a job?

</details>

<details><summary>Hint 2</summary>

Run `limit` slots that each claim the next index from a shared cursor when their call finishes, with a completion counter to decide when to resolve.

</details>

<details><summary>Hint 3</summary>

After a failure, no new calls may start (use a flag), a synchronous throw in `mapper` counts as failure, `limit < 1` rejects with `RangeError`, and results stay in input order.

</details>

## Solution

The full answer is free on UIRound: [Implement mapLimit() / throttlePromises() with maximum N concurrent tasks](https://uiround.com/questions/implement-maplimit-throttlepromises-with-maximum-n). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2046%5D%20).
