# Build infinite scrolling using IntersectionObserver

**Track:** React application patterns  
**Level:** Medium  
**Time:** about 35 minutes  
**Reported at:** Rippling, LinkedIn, Google

**[Solve it in the browser with tests](https://uiround.com/questions/build-infinite-scrolling-using-intersectionobserver)**: free, no account needed.

## Problem

Build `<InfiniteList fetchPage={fetchPage} />`. `fetchPage(page)` (pages start at 1) resolves to `{ items: string[], hasMore: boolean }`.

- Load page 1 on mount.
- Render the items as `<li>` elements, followed by an empty sentinel `<div data-testid="sentinel" />` while there are more pages.
- When the sentinel scrolls into view (use `IntersectionObserver` with `rootMargin: "200px"`), load the next page and append its items.
- Show `<p role="status">Loading…</p>` while a page loads, and `<p>You have seen everything</p>` when `hasMore` is false.
- On failure, show `<p role="alert">` with a **Retry** button that loads the same page again.

**Requirements**

- Never load the same page twice, even if the observer fires several times while a page is loading.
- Stop observing once there are no more pages.
- Disconnect the observer on unmount.

## Starter code

```jsx
import { useCallback, useEffect, useRef, useState } from "react";

function InfiniteList({ fetchPage }) {
  // Your code here
  return <ul />;
}

// Preview: a fake API with 5 pages.
const fakePage = (page) =>
  new Promise((resolve) =>
    setTimeout(() => resolve({ items: Array.from({ length: 10 }, (_, i) => `Item ${(page - 1) * 10 + i + 1}`), hasMore: page < 5 }), 400),
  );

function App() {
  return (
    <div style={{ height: 250, overflow: "auto" }}>
      <InfiniteList fetchPage={fakePage} />
    </div>
  );
}
```

## Hints

<details><summary>Hint 1</summary>

Think about how the page knows the user has reached the end of the list without listening to scroll events.

</details>

<details><summary>Hint 2</summary>

Render a sentinel after the list, observe it with `IntersectionObserver` using `rootMargin: '200px'`, and call `loadNext` when it intersects.

</details>

<details><summary>Hint 3</summary>

The observer can fire many times, so guard against double loads with a ref, not state. Append pages with functional updates, retry the same page on failure, and stop when `hasMore` is false.

</details>

## Solution

The full answer is free on UIRound: [Build infinite scrolling using IntersectionObserver](https://uiround.com/questions/build-infinite-scrolling-using-intersectionobserver). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2068%5D%20).
