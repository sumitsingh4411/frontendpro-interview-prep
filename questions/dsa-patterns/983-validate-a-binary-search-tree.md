# Validate a binary search tree

**Track:** Algorithms & data structures  
**Level:** Medium  
**Time:** about 25 minutes

**[Solve it in the browser with tests](https://uiround.com/questions/validate-a-binary-search-tree)**: free, no account needed.

## Problem

Write `isValidBST(root, options)` that returns `true` when a binary tree is a valid binary search tree, and `false` otherwise.

A node is a plain object `{ value, left, right }` with a number `value` and `left`/`right` set to a node or `null`. The tree passed in is `root`, which may be `null` (an empty tree is valid).

A tree is a valid binary search tree when, for **every** node:

- every value in its left subtree is smaller than the node's value, and
- every value in its right subtree is larger than the node's value.

The rule covers the whole subtree, not only the direct children. Values can be any numbers, including negative numbers, `-Infinity` and `Infinity`.

`options` is optional: `{ allowDuplicates: false }` by default. When `allowDuplicates` is `true`, a value **equal** to a node's value may appear in that node's right subtree, never in its left subtree. (This is how a tree that sends ties to the right is built.)

```js
const node = (value, left = null, right = null) => ({ value, left, right });

isValidBST(node(8, node(3, node(1), node(6)), node(10))); // true
isValidBST(node(8, node(3, null, node(9)), node(10))); // false: 9 is in 8's left subtree
isValidBST(node(5, node(3), node(5))); // false: duplicates are not allowed by default
isValidBST(node(5, node(3), node(5)), { allowDuplicates: true }); // true
```

## Starter code

```js
function isValidBST(root, options = {}) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

Comparing each node only with its two children is not enough. Think about what every node in a left subtree must be smaller than.

</details>

<details><summary>Hint 2</summary>

Pass a lower and an upper bound down the tree. Going left tightens the upper bound to the parent's value; going right tightens the lower bound.

</details>

<details><summary>Hint 3</summary>

Do not start the bounds at -Infinity and Infinity: a tree that holds Infinity is valid. Use null for no bound, and decide whether a value equal to a bound is allowed.

</details>

## Solution

The full answer is free on UIRound: [Validate a binary search tree](https://uiround.com/questions/validate-a-binary-search-tree). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20983%5D%20).
