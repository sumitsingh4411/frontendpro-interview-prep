# Implement useDebounce() for values

**Track:** React hooks & state  
**Level:** Medium  
**Time:** about 35 minutes

**[Solve it in the browser with tests](https://uiround.com/questions/implement-usedebounce-for-values)**: free, no account needed.

## Problem

Implement the hook `useDebounce(value, delay)`. It returns a copy of `value` that only updates after `value` has stopped changing for `delay` milliseconds.

```jsx
function Search() {
  const [query, setQuery] = useState("");
  const debouncedQuery = useDebounce(query, 300);
  useEffect(() => {
    if (debouncedQuery) searchApi(debouncedQuery); // runs once the user pauses typing
  }, [debouncedQuery]);
  return <input value={query} onChange={(e) => setQuery(e.target.value)} />;
}
```

**Requirements**

- Return the initial value immediately on the first render.
- Every change restarts the wait, so a burst of changes produces a single update with the last value.
- Clear any pending timer when the component unmounts.
- If `delay` changes, use the new delay.

## Starter code

```jsx
import { useState, useEffect } from "react";

function useDebounce(value, delay) {
  // Your code here
  return value;
}

// Preview: type quickly and watch the debounced value catch up.
function App() {
  const [text, setText] = useState("");
  const debounced = useDebounce(text, 500);
  return (
    <div>
      <input value={text} onChange={(e) => setText(e.target.value)} placeholder="Type here" />
      <p>Debounced: {debounced}</p>
    </div>
  );
}
```

## Hints

<details><summary>Hint 1</summary>

Which part of React's lifecycle already gives you a place to schedule something and to cancel it when things change?

</details>

<details><summary>Hint 2</summary>

Keep the debounced value in state, and in an effect on `value` and `delay` set a timer that updates it, returning a cleanup that clears the timer.

</details>

<details><summary>Hint 3</summary>

The first render must return the initial value immediately, the cleanup also covers unmount, and `delay` belongs in the dependency array so a new delay applies.

</details>

## Solution

The full answer is free on UIRound: [Implement useDebounce() for values](https://uiround.com/questions/implement-usedebounce-for-values). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2056%5D%20).
