# Implement a mini useState and useEffect hooks engine

**Track:** Advanced React & rendering  
**Level:** Hard  
**Time:** about 60 minutes  
**Reported at:** Zomato

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-a-mini-usestate-and-useeffect-hooks-engine)**: free, no account needed.

## Problem

Hooks look like magic: how does `useState` "remember" a value in a plain function? Build a tiny hooks engine to find out.

Implement `mount(Component, props)`, `useState`, `useEffect` and `useRef`. A component is a plain function that returns any value (for example a string); `mount` returns an instance:

```js
function Counter({ step }) {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]);
  return `count=${count}`;
}

const counter = mount(Counter, { step: 1 });
counter.output; // "count=0"
```

Instance API: `output` (the last returned value), `renders` (how many times it rendered), `setProps(props)` (re-render now with new props), and `unmount()`.

**Rules**

- `useState(initial)` returns `[state, setState]`. `initial` may be a function (called only on the first render). `setState(value | updater)` schedules a re-render. Several calls in the same tick are **batched** into one render (use a microtask), and updaters apply in order. Setting the same value (`Object.is`) does not re-render. `setState` is stable across renders and does nothing after unmount.
- `useEffect(effect, deps)` runs **after** the render. With `deps` omitted it runs after every render; with `[]` only once; otherwise when any dep changed (`Object.is`). Before re-running, and on unmount, call the cleanup the effect returned.
- `useRef(initial)` returns the same `{ current }` object on every render, and changing it never re-renders.
- Instances are independent.

## Starter code

```js
function mount(Component, props = {}) {
  // Your code here
}

function useState(initial) {}

function useEffect(effect, deps) {}

function useRef(initial) {}
```

## Hints

<details><summary>Hint 1</summary>

A plain function has no memory between calls. Think about where state could live, and how a call knows which slot is its own.

</details>

<details><summary>Hint 2</summary>

Store each instance's hooks in an array indexed by call order, with a global current instance. Batch `setState` through a microtask and run effects after the render.

</details>

<details><summary>Hint 3</summary>

Skip re-render when `Object.is` says the value is unchanged, apply updaters in order, and run an effect's cleanup before it re-runs and on unmount. `setState` must be stable and ignored after unmount.

</details>

## Solution

The full answer is free on FrontendPro: [Implement a mini useState and useEffect hooks engine](https://frontend.nextjoblist.com/questions/implement-a-mini-usestate-and-useeffect-hooks-engine). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20112%5D%20).
