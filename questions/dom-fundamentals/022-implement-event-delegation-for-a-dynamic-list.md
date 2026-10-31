# Implement event delegation for a dynamic list

**Track:** Browser & DOM fundamentals  
**Level:** Easy  
**Time:** about 15 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-event-delegation-for-a-dynamic-list)**: free, no account needed.

## Problem

A to-do list adds and removes `<li class="item">` elements all the time. Attaching a click listener to every item is slow and easy to get wrong, because new items need listeners too.

Implement `delegate(root, eventType, selector, handler)`. It adds **one** listener on `root`. When an event happens on an element inside `root` that matches `selector` (or on anything inside such an element), it calls `handler(event, matchedElement)` with `this` set to the matched element. It returns a function that removes the listener.

```js
const off = delegate(list, "click", ".item", (event, item) => {
  console.log("clicked", item.dataset.id);
});
list.insertAdjacentHTML("beforeend", '<li class="item" data-id="3">New</li>');
// Clicking the new item works without adding a listener.
off(); // stop listening
```

**Requirements**

- Items added after `delegate` was called must work.
- Clicking a child of an item, such as a `<span>` inside the `<li>`, counts as clicking the item.
- Ignore events that do not come from a matching element.
- Ignore matches outside `root`, even if an ancestor of `root` matches the selector.

## Starter code

```js
function delegate(root, eventType, selector, handler) {
  // Your code here
}

// Try it: press Run, then click the items in the preview.
const list = document.getElementById("root");
list.innerHTML = '<ul><li class="item" data-id="1"><b>Buy milk</b></li><li class="item" data-id="2">Call mum</li></ul>';
delegate(list, "click", ".item", (event, item) => {
  item.style.textDecoration = "line-through";
});
```

## Hints

<details><summary>Hint 1</summary>

Many items come and go, so where should the listener live and how will you work out which item an event was about?

</details>

<details><summary>Hint 2</summary>

Attach one listener on `root` and use `event.target.closest(selector)` to find the intended item, then call the handler with that element as `this`.

</details>

<details><summary>Hint 3</summary>

Clicking a nested `<span>` must count, and a match must be inside `root`, because `closest` can walk past it to an outer ancestor. Return a function that removes the listener.

</details>

## Solution

The full answer is free on UIRound: [Implement event delegation for a dynamic list](https://frontend.nextjoblist.com/questions/implement-event-delegation-for-a-dynamic-list). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2022%5D%20).
