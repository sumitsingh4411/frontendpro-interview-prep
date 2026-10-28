# Valid parentheses using a stack

**Track:** Strings, objects & algorithms  
**Level:** Easy  
**Time:** about 15 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/valid-parentheses-using-a-stack)**: free, no account needed.

## Problem

Implement `isValid(s)`. The string contains only the characters `(`, `)`, `[`, `]`, `{` and `}`. Return `true` when every bracket is closed by the same type of bracket, in the correct order.

```js
isValid("()[]{}"); // true
isValid("{[]}"); // true
isValid("(]"); // false
isValid("([)]"); // false
```

**Requirements**

- Every opening bracket must be closed by a bracket of the same type.
- Brackets must close in the reverse order they were opened.
- An empty string is valid.
- Solve it in O(n) time.

## Starter code

```js
function isValid(s) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

Which bracket gets closed first when brackets are nested? Think about what data structure matches that order.

</details>

<details><summary>Hint 2</summary>

Push each opener onto a stack. On a closer, pop and check that it is the matching type, using a map from closer to opener.

</details>

<details><summary>Hint 3</summary>

A closer arriving on an empty stack is invalid, and a string like `(((` ends with leftovers on the stack, so check it is empty at the end.

</details>

## Solution

The full answer is free on FrontendPro: [Valid parentheses using a stack](https://frontend.nextjoblist.com/questions/valid-parentheses-using-a-stack). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%2012%5D%20).
