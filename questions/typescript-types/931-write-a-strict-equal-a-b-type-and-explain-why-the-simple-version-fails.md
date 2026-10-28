# Write a strict Equal<A, B> type and explain why the simple version fails

**Track:** TypeScript type challenges  
**Level:** Medium  
**Time:** about 30 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/write-a-strict-equal-a-b-type-and-explain-why-the-simple-version-fails)**: free, no account needed.

## Problem

Every type-level test needs an equality check, and the obvious one is wrong. This is the starter version:

```ts
type MyEqual<A, B> = A extends B ? (B extends A ? true : false) : false;
```

It checks that each type is assignable to the other. That is not the same as being the same type, and the conditional type also distributes over unions.

Rewrite `MyEqual<A, B>` so it returns exactly `true` when `A` and `B` are the same type and exactly `false` otherwise. It must:

- tell `any` apart from every other type, including `unknown`
- return `false`, not `boolean`, when one side is a union and the other is a member of it
- return `true` for `MyEqual<never, never>`, not `never`
- tell `{ readonly a: string }` apart from `{ a: string }`

Name it `MyEqual`, because `Equal` is already defined by the test helpers.

```ts
type A = MyEqual<string, string>; // true
type B = MyEqual<any, string>; // false
type C = MyEqual<string | number, string>; // false
type D = MyEqual<{ readonly a: string }, { a: string }>; // false
```

## Starter code

```ts
// Mutual assignability: looks right, but fails for any, unions, never and readonly.
type MyEqual<A, B> = A extends B ? (B extends A ? true : false) : false;
```

## Hints

<details><summary>Hint 1</summary>

Run the starter against each test and note which pairs it gets wrong: any, unions, never and readonly properties.

</details>

<details><summary>Hint 2</summary>

Compare two generic function types instead of A and B directly. The compiler checks deferred conditional types in their bodies by identity, not by assignability.

</details>

<details><summary>Hint 3</summary>

Do not put A or B alone on the left of extends. That makes the check distribute over unions and gives boolean or never instead of true or false.

</details>

## Solution

The full answer is free on FrontendPro: [Write a strict Equal<A, B> type and explain why the simple version fails](https://frontend.nextjoblist.com/questions/write-a-strict-equal-a-b-type-and-explain-why-the-simple-version-fails). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20931%5D%20).
