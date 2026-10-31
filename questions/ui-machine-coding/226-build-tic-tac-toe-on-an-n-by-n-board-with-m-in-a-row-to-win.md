# Build tic-tac-toe on an N×N board with M in a row to win

**Track:** UI machine coding  
**Level:** Medium  
**Time:** about 40 minutes  
**Reported at:** Atlassian, Swiggy, Databricks

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/build-tic-tac-toe-on-an-n-by-n-board-with-m-in-a-row-to-win)**: free, no account needed.

## Problem

Build a **TicTacToe** component that works on any board size, with two props: `size = 3` (the board is `size × size`) and `winLength` (how many marks in a row win; defaults to `size`). Solve it in React, Vue, Angular or Svelte with the switcher above the editor. Export the component as the default export; in Angular, props are inputs.

- Render `size × size` cells as `<button>`s, row by row, each with `aria-label="Row r, column c"` (1-based) and the mark as its text.
- X moves first, then players alternate. Clicking an empty cell places the current player's mark.
- A player wins with `winLength` of their marks in a row horizontally, vertically or on either diagonal. Lines do not wrap from the end of one row to the start of the next. `winLength` can be smaller than `size` (4 in a row on a 5×5 board).
- A status line (`role="status"`) shows `Next player: X`, `Player O wins!` or `Draw!` (every cell filled and nobody won).
- When the game is over, every cell is disabled; filled cells are always disabled.
- A **Reset** button starts a new game.

Writing the win check as a pure `findWinner(cells, size, winLength)` function over a flat array is a good way to structure it.

## Starter code

```jsx
import { useState } from "react";

function findWinner(cells, size, winLength) {
  // Your code here
  return null;
}

export default function TicTacToe({ size = 3, winLength = size }) {
  // Your code here
  return null;
}
```

## Starter code (Vue)

```vue
<script setup>
import { computed, ref } from "vue";

const props = defineProps({
  size: { type: Number, default: 3 },
  winLength: { type: Number, default: undefined },
});

function findWinner(cells, size, winLength) {
  // Your code here
  return null;
}

// Your code here
</script>

<template>
  <div></div>
</template>
```

## Starter code (Angular)

```ts
import { Component, computed, input, signal } from "@angular/core";

type Mark = "X" | "O" | null;

function findWinner(cells: Mark[], size: number, winLength: number): Mark {
  // Your code here
  return null;
}

@Component({
  selector: "tic-tac-toe",
  template: `<div></div>`,
})
export default class TicTacToe {
  size = input(3);
  winLength = input<number | undefined>(undefined);

  // Your code here
}
```

## Starter code (Svelte)

```svelte
<script>
  let { size = 3, winLength } = $props();

  function findWinner(cells, size, winLength) {
    // Your code here
    return null;
  }

  // Your code here
</script>

<div></div>
```

This question can also be solved in Vue, Angular and Svelte on the site.

## Hints

<details><summary>Hint 1</summary>

Decide what the single source of truth is. If you store only the cells, almost everything else (turn, winner, draw) can be derived.

</details>

<details><summary>Hint 2</summary>

Detect wins by scanning from each filled cell in four directions (right, down, two diagonals) counting consecutive equal marks up to `winLength`.

</details>

<details><summary>Hint 3</summary>

Convert between flat index and row/column carefully, and don't let a line wrap around the row edge. Disable all cells once the game ends, and `winLength` need not equal board size.

</details>

## Solution

The full answer is free on UIRound: [Build tic-tac-toe on an N×N board with M in a row to win](https://frontend.nextjoblist.com/questions/build-tic-tac-toe-on-an-n-by-n-board-with-m-in-a-row-to-win). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20226%5D%20).
