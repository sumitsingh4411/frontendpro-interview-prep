# Build a binary search tree class with insert, search, delete and in-order traversal

**Track:** Algorithms & data structures  
**Level:** Medium  
**Time:** about 35 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/build-a-binary-search-tree-class-with-insert-search-delete-and-in-order-traversal)**: free, no account needed.

## Problem

Implement a binary search tree of numbers as a class called `BST`. Every node is a plain object `{ value, left, right }`, where `left` and `right` are child nodes or `null`. Smaller values go in the left subtree, larger values in the right subtree, and the tree never holds the same value twice.

The class has two public fields and four methods:

- `root`: the root node, or `null` for an empty tree.
- `size`: the number of values in the tree.
- `insert(value)`: adds the value as a new leaf and returns `true`. If the value is already in the tree, changes nothing and returns `false`.
- `search(value)`: returns the node that holds the value (the same object that sits in the tree), or `null`.
- `delete(value)`: removes the value and returns `true`, or returns `false` if it is not in the tree. Follow these rules, because the tests check the shape of the tree afterwards:
  1. A leaf is removed from its parent.
  2. A node with one child is replaced by that child.
  3. A node with two children keeps its place in the tree but takes the value of its **in-order successor** (the smallest value in its right subtree). The successor's node is then removed with rule 1 or 2.
- `inOrder()`: returns a new array of all values in ascending order.

Sorted input turns the tree into a long chain, so prefer loops to recursion for `insert`, `search` and `delete`.

```js
const tree = new BST();
[50, 30, 70, 20, 40, 60, 80].forEach((v) => tree.insert(v));
tree.inOrder(); // [20, 30, 40, 50, 60, 70, 80]
tree.search(40) === tree.root.left.right; // true
tree.delete(50); // true; the root node now holds 60
tree.insert(30); // false, already there
```

## Starter code

```js
class BST {
  constructor() {
    this.root = null;
    this.size = 0;
  }

  insert(value) {
    // Your code here
  }

  search(value) {
    // Your code here
  }

  delete(value) {
    // Your code here
  }

  inOrder() {
    // Your code here
  }
}
```

## Hints

<details><summary>Hint 1</summary>

Every operation starts the same way: compare the value with the current node and walk left when it is smaller, right when it is larger.

</details>

<details><summary>Hint 2</summary>

Deleting is three cases. A leaf just goes away, a node with one child is replaced by that child, and a node with two children takes its in-order successor's value.

</details>

<details><summary>Hint 3</summary>

Delete needs the parent of the node you remove, including the case where the node is the root. Keep a parent pointer as you walk, and update `size` only when something really changed.

</details>

## Solution

The full answer is free on UIRound: [Build a binary search tree class with insert, search, delete and in-order traversal](https://frontend.nextjoblist.com/questions/build-a-binary-search-tree-class-with-insert-search-delete-and-in-order-traversal). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20982%5D%20).
