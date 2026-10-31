# Two Sum using a hash map

**Track:** Strings, objects & algorithms  
**Level:** Easy  
**Time:** about 15 minutes

**[Solve it in the browser with tests](https://uiround.com/questions/two-sum-using-a-hash-map)**: free, no account needed.

## Problem

Implement `twoSum(nums, target)`. Return the indexes `[i, j]` of two different elements whose sum is `target`, with `i < j`. If no pair exists, return `[]`.

```js
twoSum([2, 7, 11, 15], 9); // [0, 1]
twoSum([3, 2, 4], 6); // [1, 2]
twoSum([3, 3], 6); // [0, 1]
```

**Requirements**

- Do not use the same element twice.
- Solve it in O(n) time with a hash map.
- When several pairs exist, return the first pair completed while scanning from left to right.

## Starter code

```js
function twoSum(nums, target) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

The brute force checks every pair. What information about earlier elements would let you answer each new element in one lookup?

</details>

<details><summary>Hint 2</summary>

Store value to index in a map as you scan, and for each element look up `target - value` among the ones already seen.

</details>

<details><summary>Hint 3</summary>

Look up the complement before inserting the current element, otherwise `[3, 3]` with target 6 or a lone `3` would reuse the same index.

</details>

## Solution

The full answer is free on UIRound: [Two Sum using a hash map](https://uiround.com/questions/two-sum-using-a-hash-map). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2013%5D%20).
