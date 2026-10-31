# Implement UnionToIntersection with contravariant inference

**Track:** Advanced TypeScript types  
**Level:** Hard  
**Time:** about 45 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-uniontointersection-with-contravariant-inference)**: free, no account needed.

## Problem

Union-to-intersection is the building block behind typed plugin systems, overloaded handlers and merged config types. Distribution turns a union into its members easily; turning it into an intersection needs one trick of the type checker.

Write two types:

- **`UnionToIntersection<U>`**: the intersection of every member of the union `U`. `UnionToIntersection<A | B | C>` is `A & B & C`.
  - A single type comes back unchanged.
  - `never` (the empty union) becomes `unknown`, the identity of `&`.
  - Members that cannot overlap collapse as usual: `string | number` becomes `never`, and so does `boolean` (which is `true | false`).
- **`MergeUnion<U>`**: for a union of object types, one flat object type with every property of every member. `MergeUnion<{ a: 1 } | { b: 2 }>` is `{ a: 1; b: 2 }`, a single object type, not the intersection `{ a: 1 } & { b: 2 }`. Keep `readonly` and optional modifiers.

Do not use the built-in `Exclude` or `Extract` helpers to fake it; the point is the inference trick.

```ts
type Handlers = ((e: "click") => void) | ((e: "key") => void);
type Both = UnionToIntersection<Handlers>; // ((e: "click") => void) & ((e: "key") => void)

type Config = MergeUnion<{ port: number } | { host?: string }>; // { port: number; host?: string }
```

## Starter code

```ts
type UnionToIntersection<U> = any;

type MergeUnion<U> = any;
```

## Hints

<details><summary>Hint 1</summary>

Distribution splits a union into members, but every conditional type joins its results back into a union. You need a place where the compiler combines candidates with & instead.

</details>

<details><summary>Hint 2</summary>

When `infer` sits in a parameter position and gets several candidates, TypeScript intersects them. Wrap each member in a function parameter, then infer that parameter once.

</details>

<details><summary>Hint 3</summary>

The final `extends (x: infer I) => void` check must not distribute, or you infer one member at a time. And `{ a: 1 } & { b: 2 }` is not `Equal` to `{ a: 1; b: 2 }` until you flatten it with a mapped type.

</details>

## Solution

The full answer is free on UIRound: [Implement UnionToIntersection with contravariant inference](https://frontend.nextjoblist.com/questions/implement-uniontointersection-with-contravariant-inference). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20944%5D%20).
