# Implement a reactive dependency system with automatic dependency tracking

**Track:** Advanced JS, browser & architecture  
**Level:** Hard  
**Time:** about 75 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-a-reactive-dependency-system-with-automatic)**: free, no account needed.

## Problem

Signals (Solid, Vue, Preact Signals, Angular) update exactly what depends on changed data, with no dependency arrays. Build the core:

- `createSignal(initial)` returns `[read, write]`. `write(value | updater)` changes the value; writing an equal value (`Object.is`) does nothing.
- `createMemo(fn)` returns a `read` function for a **derived** value. It is computed lazily, cached, and recomputed only when one of the signals or memos it read has changed.
- `createEffect(fn)` runs `fn` immediately and again whenever anything it **read during its last run** changes. If `fn` returns a function, call it before the next run and on dispose. `createEffect` returns a `dispose` function.
- `batch(fn)`: run `fn`; effects affected by writes inside it run **once**, after it.

Dependencies are tracked **automatically**: whatever a memo or effect reads while it runs becomes its dependency set, rebuilt on every run (so `if/else` branches work).

**Glitch-free:** in a diamond (`a → b`, `a → c`, effect reads `b` and `c`), changing `a` runs the effect **once**, and it never sees `b` updated but `c` stale. If a memo recomputes to the same value, effects that depend only on it do **not** re-run.

```js
const [price, setPrice] = createSignal(100);
const [qty, setQty] = createSignal(2);
const total = createMemo(() => price() * qty());
createEffect(() => console.log(`Total: ${total()}`)); // "Total: 200"
batch(() => {
  setPrice(120);
  setQty(3);
}); // logs "Total: 360" once
```

## Starter code

```js
function createSignal(initial) {
  // Your code here
}

function createMemo(fn) {}

function createEffect(fn) {}

function batch(fn) {}
```

## Hints

<details><summary>Hint 1</summary>

Dependencies are not declared. Ask how the system can learn what a function reads while it is running.

</details>

<details><summary>Hint 2</summary>

Keep a global 'currently running' subscriber; reads register an edge to it and writes mark dependents dirty. Rebuild the dependency set on every run.

</details>

<details><summary>Hint 3</summary>

In a diamond the effect must run once and never see a stale value. A memo that recomputes to an equal value must not trigger its dependents, and `batch` runs affected effects once after it ends.

</details>

## Solution

The full answer is free on FrontendPro: [Implement a reactive dependency system with automatic dependency tracking](https://frontend.nextjoblist.com/questions/implement-a-reactive-dependency-system-with-automatic). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20123%5D%20).
