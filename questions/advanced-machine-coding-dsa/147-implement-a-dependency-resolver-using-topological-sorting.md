# Implement a dependency resolver using topological sorting

**Track:** Advanced machine coding & DSA  
**Level:** Hard  
**Time:** about 60 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/implement-a-dependency-resolver-using-topological-sorting)**: free, no account needed.

## Problem

Package managers, build tools and module bundlers all need to know what to install or build first. Implement:

1. `findOrder(numCourses, prerequisites)` (LeetCode 210): `prerequisites` are pairs `[a, b]` meaning "take `b` before `a`". Return **any** order that takes every course, or `[]` if it is impossible (a cycle).
2. `resolveInstallOrder(packages)`: `packages` maps a name to its dependency names, for example `{ app: ["react", "router"], router: ["react"], react: [] }`. Return the install order (dependencies before dependents). Make it **deterministic**: when several packages are ready, take them in alphabetical order. Throw an `Error`:
   - `Unknown dependency "x" required by "y"` when a dependency is not in `packages`;
   - `Circular dependency: a -> b -> a` (the actual cycle path) when there is a cycle.

## Starter code

```js
function findOrder(numCourses, prerequisites) {
  // Your code here
}

function resolveInstallOrder(packages) {
  // Your code here
}
```

## Hints

<details><summary>Hint 1</summary>

Reframe the problem as a graph: what are the nodes, and which direction should an edge point so the result reads left to right?

</details>

<details><summary>Hint 2</summary>

Count incoming dependencies for each node, start with the zero ones, and release dependents as you go. If nodes remain, there is a cycle.

</details>

<details><summary>Hint 3</summary>

For packages, validate unknown dependencies first, take ready packages in alphabetical order for determinism, and report the actual cycle path, not just that it failed. The course version returns `[]`.

</details>

## Solution

The full answer is free on FrontendPro: [Implement a dependency resolver using topological sorting](https://frontend.nextjoblist.com/questions/implement-a-dependency-resolver-using-topological-sorting). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20147%5D%20).
