# Implement useInterval() without stale closures

**Track:** React hooks & state  
**Level:** Medium  
**Time:** about 35 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-useinterval-without-stale-closures)**: free, no account needed.

## Problem

This counter looks right but gets stuck at 1:

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    const id = setInterval(() => setCount(count + 1), 1000);
    return () => clearInterval(id);
  }, []); // the callback only ever sees count = 0
  return <h1>{count}</h1>;
}
```

Implement `useInterval(callback, delay)` so that:

- `callback` runs every `delay` ms and always sees the **latest** props and state (no stale closure);
- passing a new callback on every render does **not** restart the interval;
- `delay === null` pauses the interval, and changing `delay` restarts it with the new delay;
- the interval is cleared when the component unmounts.

```jsx
function Clock() {
  const [count, setCount] = useState(0);
  const [running, setRunning] = useState(true);
  useInterval(() => setCount(count + 1), running ? 1000 : null);
  return <button onClick={() => setRunning(!running)}>{count}</button>;
}
```

## Starter code

```jsx
import { useEffect, useRef, useState } from "react";

function useInterval(callback, delay) {
  // Your code here
}

// Preview: a counter you can pause.
function App() {
  const [count, setCount] = useState(0);
  const [running, setRunning] = useState(true);
  useInterval(() => setCount(count + 1), running ? 500 : null);
  return (
    <div>
      <h1 style={{ margin: 0 }}>{count}</h1>
      <button onClick={() => setRunning(!running)}>{running ? "Pause" : "Resume"}</button>
    </div>
  );
}
```

## Hints

<details><summary>Hint 1</summary>

Why does the callback inside the effect always see `count = 0`, and which value should be allowed to change without restarting the timer?

</details>

<details><summary>Hint 2</summary>

Store the latest callback in a ref updated each render, have the interval call `ref.current()`, and make the timer effect depend only on `delay`.

</details>

<details><summary>Hint 3</summary>

`delay === null` should skip creating the interval (pause), changing `delay` restarts it, and the cleanup must clear the interval on unmount.

</details>

## Solution

The full answer is free on FrontendPro: [Implement useInterval() without stale closures](https://frontend.nextjoblist.com/questions/implement-useinterval-without-stale-closures). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2059%5D%20).
