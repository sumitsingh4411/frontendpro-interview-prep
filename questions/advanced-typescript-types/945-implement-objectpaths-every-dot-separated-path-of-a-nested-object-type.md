# Implement ObjectPaths: every dot-separated path of a nested object type

**Track:** Advanced TypeScript types  
**Level:** Hard  
**Time:** about 50 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-objectpaths-every-dot-separated-path-of-a-nested-object-type)**: free, no account needed.

## Problem

Form libraries, i18n helpers and `get`/`set` utilities take a string path such as `"address.city"`. Typing that argument means computing every valid path of an object type.

Write two types:

- **`ObjectPaths<T>`**: the union of every dot-separated path in `T`, including paths to nested objects themselves. For `{ a: { b: string } }` that is `"a" | "a.b"`.
- **`LeafPaths<T>`**: only the paths that end at a leaf value, so `"a.b"` but not `"a"`.

Rules for both:

- **Leaves** are primitives (`string`, `number`, `boolean`, `bigint`, `symbol`, `null`, `undefined`), functions, arrays and tuples, and `Date`. Do not descend into them.
- **Optional and nullable properties** are followed: for `profile?: { bio: string } | null` the paths include `"profile.bio"`.
- **Unions of objects** contribute the paths of every member.
- **Keys**: string keys are used as they are; numeric keys appear in their string form (`{ 0: string }` gives `"0"`); symbol keys are skipped.
- An empty object type has no paths (`never`). For `LeafPaths`, a nested empty object is not a leaf and adds nothing.
- A primitive `T` has no paths.

Nesting depth is limited by the compiler's recursion limit (about 50 levels of instantiation), far more than real data types need. Recursive types such as a tree node that contains itself are out of scope.

```ts
type Form = { name: string; address: { city: string; zip?: number }; tags: string[] };

type All = ObjectPaths<Form>; // "name" | "address" | "address.city" | "address.zip" | "tags"
type Leaves = LeafPaths<Form>; // "name" | "address.city" | "address.zip" | "tags"
```

## Starter code

```ts
type ObjectPaths<T> = any;

type LeafPaths<T> = any;
```

## Hints

<details><summary>Hint 1</summary>

Start with one level: a mapped type over the keys whose value for key K is K itself, indexed with [keyof T] to turn the object into a union of its values.

</details>

<details><summary>Hint 2</summary>

For nested objects, map each key to itself or to a template literal that joins the key, a dot and every path of the value. A union in a placeholder expands to one string per member; `never` empties it.

</details>

<details><summary>Hint 3</summary>

Decide what a leaf is before you recurse. Arrays, functions and Date are objects too, so without a check you get paths like `tags.length` or `createdAt.getTime`.

</details>

## Solution

The full answer is free on FrontendPro: [Implement ObjectPaths: every dot-separated path of a nested object type](https://frontend.nextjoblist.com/questions/implement-objectpaths-every-dot-separated-path-of-a-nested-object-type). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20945%5D%20).
