# Implement a single-flight token refresh mechanism: 10 failed requests trigger only one refresh, followed by safe retries

**Track:** Advanced async concurrency  
**Level:** Hard  
**Time:** about 60 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-a-single-flight-token-refresh-mechanism-10-failed)**: free, no account needed.

## Problem

A dashboard fires 10 requests at once just as the access token expires. All 10 get `401 Unauthorized`. A naive client refreshes the token **10 times**. Refresh tokens are often single-use, so the second refresh fails and the user is logged out.

Implement `createAuthClient({ request, refreshToken, initialToken, onAuthFailure = () => {} })` returning `{ fetch(url), token }`:

- `request(url, token)` performs the call and resolves to `{ status, data }`.
- `refreshToken()` resolves to a new access token (or rejects).

Rules for `client.fetch(url)`:

- Send the current token. If the status is not 401, return the response.
- On 401, refresh **at most once at a time** (single-flight): concurrent 401s all wait for the **same** refresh, then retry with the new token.
- If a request failed with an **old** token that has **already** been replaced (the refresh finished while it was in flight), retry with the current token **without** refreshing again.
- Retry each request **only once**. A second 401 rejects with an `Error` whose `status` is 401.
- If the refresh fails, every waiting request rejects with the refresh error, and `onAuthFailure(error)` is called **once** for that failed refresh.
- After a refresh settles, a later expiry can trigger a new refresh.

## Starter code

```js
function createAuthClient({ request, refreshToken, initialToken, onAuthFailure = () => {} }) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

Ten requests failing together should not mean ten refreshes. Think about what each failed request needs to know before deciding.

</details>

<details><summary>Hint 2</summary>

Cache the in-flight refresh promise so concurrent 401s await the same one. Remember which token each request used and compare it with the current token.

</details>

<details><summary>Hint 3</summary>

A request that failed with an already replaced token retries without refreshing. Retry once only, call `onAuthFailure` once per failed refresh, and clear the cached promise so a later expiry can refresh again.

</details>

## Solution

The full answer is free on FrontendPro: [Implement a single-flight token refresh mechanism: 10 failed requests trigger only one refresh, followed by safe retries](https://frontend.nextjoblist.com/questions/implement-a-single-flight-token-refresh-mechanism-10-failed). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20108%5D%20).
