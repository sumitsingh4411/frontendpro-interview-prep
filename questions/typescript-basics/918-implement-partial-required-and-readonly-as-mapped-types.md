# Implement Partial, Required and Readonly as mapped types

**Track:** TypeScript utility types  
**Level:** Easy  
**Time:** about 12 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-partial-required-and-readonly-as-mapped-types)**: free, no account needed.

## Problem

Form state, patch payloads and frozen config objects all start from an existing type and change only whether its properties are optional or writable. TypeScript ships `Partial`, `Required` and `Readonly` for this, and each is a one-line mapped type.

Write three types without using the built-in `Partial`, `Required` or `Readonly`:

- **`MyPartial<T>`**: every property of `T` becomes optional.
- **`MyRequired<T>`**: every property of `T` becomes required, and the `undefined` that came from the `?` marker goes away.
- **`MyReadonly<T>`**: every property of `T` becomes `readonly`, so assigning to it is a compile error.

Each type changes one modifier and keeps the other. They are shallow: nested objects are left as they are. Arrays and tuples must keep their shape, so `MyReadonly<string[]>` is `readonly string[]`.

```ts
type Settings = { readonly theme: string; fontSize?: number };

type Draft = MyPartial<Settings>; // { readonly theme?: string; fontSize?: number }
type Full = MyRequired<Settings>; // { readonly theme: string; fontSize: number }
type Frozen = MyReadonly<Settings>; // { readonly theme: string; readonly fontSize?: number }
```

## Starter code

```ts
type MyPartial<T> = any;

type MyRequired<T> = any;

type MyReadonly<T> = any;
```

## Hints

<details><summary>Hint 1</summary>

All three types copy every property of `T` and change only a modifier, so each one is a mapped type over `keyof T`.

</details>

<details><summary>Hint 2</summary>

Mapped types can add or remove modifiers: `?` and `readonly` add them, and a leading minus such as `-?` or `-readonly` removes them.

</details>

<details><summary>Hint 3</summary>

Removing `?` with `-?` also drops the `undefined` that the optional marker added, so a required version of `name?: string` is plain `string`.

</details>

## Solution

The full answer is free on UIRound: [Implement Partial, Required and Readonly as mapped types](https://frontend.nextjoblist.com/questions/implement-partial-required-and-readonly-as-mapped-types). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20918%5D%20).
