# Implement Pick and Omit as TypeScript utility types

**Track:** TypeScript utility types  
**Level:** Easy  
**Time:** about 15 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-pick-and-omit-as-typescript-utility-types)**: free, no account needed.

## Problem

`Pick` and `Omit` are the utility types you reach for most when shaping props and API payloads, and rebuilding them is the usual first question in a TypeScript round.

Write two types without using the built-in `Pick`, `Omit` or `Exclude`:

- **`MyPick<T, K>`**: an object type with only the properties of `T` named in `K`. `K` must be a key of `T`, so `MyPick<User, "nope">` is a compile error.
- **`MyOmit<T, K>`**: an object type with every property of `T` except those named in `K`. Unlike `MyPick`, `K` only has to be a property key, and keys `T` does not have are ignored.

Both must keep each property's `readonly` and optional (`?`) modifiers.

```ts
type User = { readonly id: number; name: string; email?: string };

type Preview = MyPick<User, "id" | "name">; // { readonly id: number; name: string }
type Draft = MyOmit<User, "id">; // { name: string; email?: string }
```

## Starter code

```ts
type MyPick<T, K> = any;

type MyOmit<T, K> = any;
```

## Hints

<details><summary>Hint 1</summary>

A mapped type `{ [P in Keys]: ... }` builds an object type with one property per member of a union of keys.

</details>

<details><summary>Hint 2</summary>

For `MyPick`, constrain the keys with `K extends keyof T` and read each property as `T[P]`. For `MyOmit`, filter `keyof T` with a conditional type that turns the removed keys into `never`.

</details>

<details><summary>Hint 3</summary>

Keep `readonly` and `?` modifiers: map over `keyof T` itself (a homomorphic mapped type) or use key remapping with `as`, instead of building a fresh key union.

</details>

## Solution

The full answer is free on FrontendPro: [Implement Pick and Omit as TypeScript utility types](https://frontend.nextjoblist.com/questions/implement-pick-and-omit-as-typescript-utility-types). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20917%5D%20).
