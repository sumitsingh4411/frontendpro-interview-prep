# Implement an HTTP cache with ETag validation, stale-while-revalidate, and request deduplication

**Track:** Advanced JS, browser & architecture  
**Level:** Hard  
**Time:** about 75 minutes

**[Solve it in the browser with tests](https://uiround.com/questions/implement-an-http-cache-with-etag-validation-stale-while)**: free, no account needed.

## Problem

Implement a client-side HTTP cache that follows the server's caching headers: `createHttpCache({ fetch, now = Date.now })` returns `{ get(url) }`, which resolves with `{ status, body, fromCache }`.

The server sends `ETag` and `Cache-Control` headers, for example `Cache-Control: max-age=60, stale-while-revalidate=300`.

Rules for `get(url)`:

- **No entry:** fetch, and store `{ body, etag, storedAt, maxAge, swr }` unless the response has `Cache-Control: no-store`. Only cache `200` responses.
- **Fresh** (age < `max-age` seconds): return the cached body without a request (`fromCache: true`).
- **Stale but within `stale-while-revalidate`**: return the cached body **immediately** and revalidate **in the background**.
- **Older than that:** revalidate and **wait** for the result.
- **Revalidating** sends `If-None-Match: <etag>` when there is an ETag. A `304 Not Modified` keeps the cached body and resets its age; a `200` replaces the entry.
- **Deduplication:** concurrent `get`s for the same URL that need the network share **one** request.
- A failed background revalidation keeps the stale entry; a failed blocking request rejects.

`fetch(url, { headers })` resolves with a standard `Response`. Body text can be read with `await response.text()`.

## Starter code

```js
function createHttpCache({ fetch, now = Date.now }) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

Think of each cached entry as being in one of three states depending on its age, and decide what the caller gets and what the network does in each.

</details>

<details><summary>Hint 2</summary>

Store the body with its ETag, storage time and `max-age`/`stale-while-revalidate`, then decide per request. Revalidate with `If-None-Match` and share in-flight requests through a per-URL map.

</details>

<details><summary>Hint 3</summary>

A 304 keeps the body and resets its age. Never cache `no-store` or non-200 responses. A failed background revalidation must keep the stale entry, but a failed blocking request rejects.

</details>

## Solution

The full answer is free on UIRound: [Implement an HTTP cache with ETag validation, stale-while-revalidate, and request deduplication](https://uiround.com/questions/implement-an-http-cache-with-etag-validation-stale-while). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20126%5D%20).
