# Implement a concurrency-safe async cache with TTL

**Track:** Concurrency & scheduling  
**Level:** Medium  
**Time:** about 35 minutes  
**Reported at:** Microsoft

**[Solve it in the browser with tests](https://uiround.com/questions/implement-a-concurrency-safe-async-cache-with-ttl)**: free, no account needed.

## Problem

Implement `createAsyncCache({ load, ttl, now = Date.now })`. `load(key)` is an async function that fetches a value. The cache:

- `get(key)`: returns a promise for the value. A value younger than `ttl` ms is served from the cache. Otherwise `load(key)` is called, **once**, even if many `get(key)` calls arrive while it is loading.
- `set(key, value)`: store a value directly (for example after a mutation).
- `delete(key)` and `clear()`: remove entries.

```js
const users = createAsyncCache({ ttl: 30_000, load: (id) => api.getUser(id) });
await users.get(7); // network
await users.get(7); // cache
users.set(7, updatedUser); // after a successful edit
```

**Requirements**

- Concurrent `get` calls for the same key share one `load`.
- Failed loads are not cached: the next `get` tries again.
- **Race safety:** if `set`, `delete` or `clear` happens while a load is in flight, the result of that older load must not overwrite the newer state.
- `now` is injectable so tests can control time.

## Starter code

```js
function createAsyncCache({ load, ttl, now = Date.now }) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

Two different things can be shared: finished values and loads still in progress. How would you track each?

</details>

<details><summary>Hint 2</summary>

Keep a value map with expiry timestamps plus an in-flight map, and a per-key version counter that a load checks before committing.

</details>

<details><summary>Hint 3</summary>

Failed loads must not be cached. If `set`, `delete` or `clear` happens during a load, the older load must not overwrite the newer state, so bump the version on every write.

</details>

## Solution

The full answer is free on UIRound: [Implement a concurrency-safe async cache with TTL](https://uiround.com/questions/implement-a-concurrency-safe-async-cache-with-ttl). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2054%5D%20).
