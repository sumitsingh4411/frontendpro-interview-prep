# Build search-as-you-type with debounce and AbortController

**Track:** React application patterns  
**Level:** Medium  
**Time:** about 35 minutes  
**Reported at:** CRED, Adobe

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/build-search-as-you-type-with-debounce-and-abortcontroller)**: free, no account needed.

## Problem

Build a `<Search searchApi={searchApi} delay={300} />` component. `searchApi(query, { signal })` returns a promise of an array of strings.

It renders:

- an `<input aria-label="Search">`;
- `<p role="status">Searching…</p>` while a request is in flight;
- the results as `<ul><li>…</li></ul>`, or `<p>No results</p>` when a finished search found nothing;
- `<p role="alert">Something went wrong</p>` when the request fails.

```jsx
<Search searchApi={(q, { signal }) => fetch(`/api/search?q=${encodeURIComponent(q)}`, { signal }).then((r) => r.json())} />
```

**Requirements**

- Debounce: only search after the user has stopped typing for `delay` ms. Typing "react" quickly sends **one** request.
- Trim the query; an empty query clears the results and sends nothing.
- When a new search starts, **abort** the previous in-flight request, and never show results for an older query.
- Keep the input responsive at all times.

## Starter code

```jsx
import { useEffect, useState } from "react";

function Search({ searchApi, delay = 300 }) {
  // Your code here
  return <input aria-label="Search" />;
}

// Preview: a fake API with a random delay.
const FRUITS = ["apple", "apricot", "banana", "blackberry", "blueberry", "cherry", "grape", "mango", "melon", "orange", "peach", "pear"];
function fakeSearch(query, { signal }) {
  return new Promise((resolve, reject) => {
    const timer = setTimeout(() => resolve(FRUITS.filter((f) => f.includes(query.toLowerCase()))), 200 + Math.random() * 400);
    signal.addEventListener("abort", () => { clearTimeout(timer); reject(new DOMException("Aborted", "AbortError")); });
  });
}

function App() {
  return <Search searchApi={fakeSearch} />;
}
```

## Hints

<details><summary>Hint 1</summary>

The text the user types and the text you search for are not the same thing. How would you keep them separate?

</details>

<details><summary>Hint 2</summary>

One effect debounces the typed text into a `debouncedQuery`; a second runs a search for it with its own `AbortController`, aborted by the cleanup.

</details>

<details><summary>Hint 3</summary>

Trim the query and clear results for an empty one without a request. Ignore `AbortError` rather than show an error, and never show results for an older query.

</details>

## Solution

The full answer is free on UIRound: [Build search-as-you-type with debounce and AbortController](https://frontend.nextjoblist.com/questions/build-search-as-you-type-with-debounce-and-abortcontroller). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2066%5D%20).
