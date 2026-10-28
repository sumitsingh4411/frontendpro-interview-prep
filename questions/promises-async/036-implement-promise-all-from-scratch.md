# Implement Promise.all() from scratch

**Track:** Promises & async  
**Level:** Medium  
**Time:** about 35 minutes  
**Reported at:** Flipkart, Tata 1mg, Zepto, Amazon, Adobe

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-promise-all-from-scratch)**: free, no account needed.

## Problem

Implement `promiseAll(iterable)` without using `Promise.all`. It returns a promise that:

- **fulfils** with an array of every result, in the **same order as the input**, once all of them have fulfilled;
- **rejects** as soon as any of them rejects, with that reason.

```js
const user = fetchUser(); // resolves after 300 ms
const posts = fetchPosts(); // resolves after 100 ms
const [u, p] = await promiseAll([user, posts]); // order follows the input, not the timing
```

**Requirements**

- Items may be promises, thenables or plain values (`promiseAll([1, Promise.resolve(2)])` gives `[1, 2]`).
- Accept any iterable, such as a `Set` or a generator.
- An empty input fulfils with `[]`.
- Do not wait for the slow items once one has rejected.

## Starter code

```js
function promiseAll(iterable) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

The result must follow input order even though promises finish in any order. How will each result find its slot?

</details>

<details><summary>Hint 2</summary>

Normalise each item with `Promise.resolve`, store the value at its own index, and resolve when a counter of pending items hits zero; the first rejection rejects.

</details>

<details><summary>Hint 3</summary>

Count completions instead of checking array length, since holes mislead. An empty input must resolve with `[]` and the iterable must be copied to an array first.

</details>

## Solution

The full answer is free on FrontendPro: [Implement Promise.all() from scratch](https://frontend.nextjoblist.com/questions/implement-promise-all-from-scratch). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2036%5D%20).
