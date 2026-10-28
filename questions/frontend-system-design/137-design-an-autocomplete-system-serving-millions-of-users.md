# Design an autocomplete system serving millions of users with caching and request cancellation

**Track:** Frontend system design  
**Level:** Hard  
**Time:** about 60 minutes  
**Reported at:** LinkedIn, Flipkart, Swiggy, Zepto

**[Design it on the whiteboard](https://frontend.nextjoblist.com/questions/design-an-autocomplete-system-serving-millions-of-users)** and check yourself against the rubric: free, no account needed.

## Problem

Design the search box of a large site (an e-commerce store or a search engine) that shows suggestions as the user types, for millions of users.

- Suggestions appear within about 100 ms of typing.
- Results are always for **what is currently typed**, never for an older query that came back late.
- The client minimises requests and the backend copes with peak traffic.
- It works well with keyboard, screen readers and on slow mobile networks.
- Suggestions can mix types: recent searches, popular queries, products, categories.

Cover the component API, the request strategy (debounce, cancellation, caching), the client cache, rendering, accessibility, and how the frontend cooperates with the backend and CDN.

## Hints

<details><summary>Hint 1</summary>

Clarify what a 'good' suggestion is and how fast it must appear. Also decide what happens when responses return out of order.

</details>

<details><summary>Hint 2</summary>

Build a controller that normalises the query, debounces, aborts the previous request, and caches results in an LRU, backed by CDN-cached popular prefixes and a prefix index on the server.

</details>

<details><summary>Hint 3</summary>

Be ready for stale responses (accept only the latest query), cache keys and invalidation, load at peak, combobox accessibility, and degrading gracefully when the network is slow or fails.

</details>

## Solution

The full answer is free on FrontendPro: [Design an autocomplete system serving millions of users with caching and request cancellation](https://frontend.nextjoblist.com/questions/design-an-autocomplete-system-serving-millions-of-users). It has a complete design walkthrough, the rubric interviewers score against, and follow-up questions with model answers.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20137%5D%20).
