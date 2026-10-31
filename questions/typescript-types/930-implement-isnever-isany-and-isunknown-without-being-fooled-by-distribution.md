# Implement IsNever, IsAny and IsUnknown without being fooled by distribution

**Track:** TypeScript type challenges  
**Level:** Medium  
**Time:** about 25 minutes

**[Solve it in the browser with tests](https://uiround.com/questions/implement-isnever-isany-and-isunknown-without-being-fooled-by-distribution)**: free, no account needed.

## Problem

Library code often needs to branch on the three special types: `never`, `any` and `unknown`. The obvious checks give wrong answers because of how conditional types treat these types.

Write three types. Each must return exactly `true` or `false`, never `boolean` or `never`:

- **`IsNever<T>`**: `true` only when `T` is `never`.
- **`IsAny<T>`**: `true` only when `T` is `any`. It is `false` for `unknown`, `never` and every other type.
- **`IsUnknown<T>`**: `true` only when `T` is `unknown`. It is `false` for `any`, `{}`, `object` and every other type.

```ts
type A = IsNever<never>; // true
type B = IsNever<string | undefined>; // false
type C = IsAny<any>; // true
type D = IsAny<unknown>; // false
type E = IsUnknown<unknown>; // true
type F = IsUnknown<any>; // false
```

## Starter code

```ts
type IsNever<T> = any;

type IsAny<T> = any;

type IsUnknown<T> = any;
```

## Hints

<details><summary>Hint 1</summary>

Each of these types is special in conditional types. Try the obvious version first and check what it gives for never and for any.

</details>

<details><summary>Hint 2</summary>

Wrap the checked type in a one-element tuple to stop distribution. For any, look for a test that only any can pass, such as intersecting it with a literal.

</details>

<details><summary>Hint 3</summary>

A conditional type on a bare type parameter maps over a union, and never is the empty union, so the obvious IsNever returns never instead of true.

</details>

## Solution

The full answer is free on UIRound: [Implement IsNever, IsAny and IsUnknown without being fooled by distribution](https://uiround.com/questions/implement-isnever-isany-and-isunknown-without-being-fooled-by-distribution). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20930%5D%20).
