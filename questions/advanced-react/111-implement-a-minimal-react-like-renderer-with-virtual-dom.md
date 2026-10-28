# Implement a minimal React-like renderer with virtual DOM diffing and keyed reconciliation

**Track:** Advanced React & rendering  
**Level:** Hard  
**Time:** about 75 minutes  
**Reported at:** Intuit

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-a-minimal-react-like-renderer-with-virtual-dom)**: free, no account needed.

## Problem

Build the core of a React-like library, without React:

- `h(type, props, ...children)` creates a virtual node `{ type, props, children, key }`. `type` is a tag name or a **function component** (`(props) => vnode`). Strings and numbers become text nodes; `null`, `undefined` and booleans render nothing; nested arrays are flattened. `key` comes from `props.key`.
- `render(vnode, container)` mounts on the first call and **patches** on later calls, reusing existing DOM nodes wherever possible.

Patching rules:

- Same `type`: update the existing DOM node's props and diff its children. Different `type`: replace the node.
- Props: attributes (removed when absent), `className`, `style` objects (removing old keys), and `on*` event handlers (`onClick` → `click`), replaced without stacking listeners.
- Children: keyed children are matched **by key** and **moved** (the same DOM node), so state like an input's value survives reordering. Unkeyed children are matched by position.

```js
render(h("ul", null, items.map((item) => h("li", { key: item.id }, item.text))), root);
```

## Starter code

```js
function h(type, props, ...children) {
  // Your code here
}

function render(vnode, container) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

Separate describing the UI (plain objects) from touching the DOM. The interesting part is what you do on the second render.

</details>

<details><summary>Hint 2</summary>

Mount builds DOM from vnodes. Patch compares old and new vnodes of the same type, updates changed props, and reconciles children by key or position, moving existing nodes.

</details>

<details><summary>Hint 3</summary>

Keyed children must move the same DOM node so input state survives. Remove props and style keys that vanished, and replace `on*` handlers without stacking listeners. Normalise children in `h`.

</details>

## Solution

The full answer is free on FrontendPro: [Implement a minimal React-like renderer with virtual DOM diffing and keyed reconciliation](https://frontend.nextjoblist.com/questions/implement-a-minimal-react-like-renderer-with-virtual-dom). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20111%5D%20).
