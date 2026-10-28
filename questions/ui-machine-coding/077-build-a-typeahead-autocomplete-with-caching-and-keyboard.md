# Build a typeahead/autocomplete with caching and keyboard support

**Track:** UI machine coding  
**Level:** Medium  
**Time:** about 45 minutes  
**Reported at:** Swiggy, Airbnb, Intuit, Microsoft

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/build-a-typeahead-autocomplete-with-caching-and-keyboard)**: free, no account needed.

## Problem

Build an **Autocomplete** component with these props:

- `fetchSuggestions(query)`: returns a promise of an array of strings. It defaults to a small search over Indian city names, so the preview works on its own.
- `debounceMs = 200`: how long typing must pause before a search.
- `onSelect(value)`: called when the user picks a suggestion.

Solve it in React, Vue, Angular or Svelte with the switcher above the editor. Export the component as the default export; in Angular, props are inputs and `onX` callbacks are outputs named `x` (here, an output named `select`).

Follow the ARIA **combobox** pattern:

- `<input role="combobox" aria-autocomplete="list" aria-expanded aria-controls="{listboxId}" aria-activedescendant="{activeOptionId}">`
- `<ul role="listbox" id="{listboxId}">` with `<li role="option" id="…" aria-selected="true|false">` for each suggestion, shown only while open.

**Requirements**

- Debounce: fetch only after the user stops typing for `debounceMs`. Do not fetch for an empty (trimmed) query.
- **Cache** results by query: typing a query you already searched shows the cached results without a request.
- Ignore responses for queries that are no longer current.
- `ArrowDown` and `ArrowUp` move the active option (wrapping); the active option has `aria-selected="true"` and its id is the input's `aria-activedescendant`.
- `Enter` selects the active option: put it in the input, close the list and call `onSelect(value)`. Pressing the mouse on an option (`mousedown`) does the same.
- `Escape` closes the list.
- Selecting a suggestion must not start a new search for the selected text.

## Starter code

```jsx
import { useEffect, useId, useRef, useState } from "react";

const CITIES = ["Ahmedabad", "Bengaluru", "Bhopal", "Chennai", "Delhi", "Hyderabad", "Jaipur", "Kolkata", "Lucknow", "Mumbai", "Pune", "Surat"];
const searchCities = (query) =>
  new Promise((resolve) => setTimeout(() => resolve(CITIES.filter((c) => c.toLowerCase().startsWith(query.toLowerCase()))), 300));

export default function Autocomplete({ fetchSuggestions = searchCities, onSelect = () => {}, debounceMs = 200 }) {
  // Your code here
  return <input role="combobox" />;
}
```

## Starter code (Vue)

```vue
<script setup>
import { computed, onBeforeUnmount, ref, useId } from "vue";

const props = defineProps({
  fetchSuggestions: {
    type: Function,
    default: (query) => {
      const cities = ["Ahmedabad", "Bengaluru", "Bhopal", "Chennai", "Delhi", "Hyderabad", "Jaipur", "Kolkata", "Lucknow", "Mumbai", "Pune", "Surat"];
      return new Promise((resolve) => setTimeout(() => resolve(cities.filter((c) => c.toLowerCase().startsWith(query.toLowerCase()))), 300));
    },
  },
  debounceMs: { type: Number, default: 200 },
});
const emit = defineEmits(["select"]);

// Your code here
</script>

<template>
  <input role="combobox" />
</template>
```

## Starter code (Angular)

```ts
import { Component, OnDestroy, computed, input, output, signal } from "@angular/core";

const CITIES = ["Ahmedabad", "Bengaluru", "Bhopal", "Chennai", "Delhi", "Hyderabad", "Jaipur", "Kolkata", "Lucknow", "Mumbai", "Pune", "Surat"];
function searchCities(query: string): Promise<string[]> {
  return new Promise((resolve) => setTimeout(() => resolve(CITIES.filter((c) => c.toLowerCase().startsWith(query.toLowerCase()))), 300));
}

@Component({
  selector: "app-autocomplete",
  template: `<input role="combobox" />`,
})
export default class Autocomplete implements OnDestroy {
  fetchSuggestions = input<(query: string) => Promise<string[]>>(searchCities);
  debounceMs = input(200);
  select = output<string>();

  // Your code here

  ngOnDestroy() {}
}
```

## Starter code (Svelte)

```svelte
<script>
  import { onDestroy } from "svelte";

  const CITIES = ["Ahmedabad", "Bengaluru", "Bhopal", "Chennai", "Delhi", "Hyderabad", "Jaipur", "Kolkata", "Lucknow", "Mumbai", "Pune", "Surat"];
  const searchCities = (query) =>
    new Promise((resolve) => setTimeout(() => resolve(CITIES.filter((c) => c.toLowerCase().startsWith(query.toLowerCase()))), 300));

  let { fetchSuggestions = searchCities, onSelect = () => {}, debounceMs = 200 } = $props();

  // Your code here
</script>

<input role="combobox" />
```

This question can also be solved in Vue, Angular and Svelte on the site.

## Hints

<details><summary>Hint 1</summary>

Typing, fetching, caching and keyboard navigation all interact. Which of them should depend on the query being current?

</details>

<details><summary>Hint 2</summary>

Debounce the query with a timer that restarts on every keystroke, check a cache keyed by query before fetching, and use `aria-activedescendant` for the highlighted option so focus stays on the input.

</details>

<details><summary>Hint 3</summary>

Don't fetch for an empty trimmed query, ignore responses for stale queries, wrap the arrow keys, and have `Enter`, a click and `Escape` each close the list correctly.

</details>

## Solution

The full answer is free on FrontendPro: [Build a typeahead/autocomplete with caching and keyboard support](https://frontend.nextjoblist.com/questions/build-a-typeahead-autocomplete-with-caching-and-keyboard). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2077%5D%20).
