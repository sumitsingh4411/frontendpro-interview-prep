# Predict which color wins: specificity, !important and cascade layers

**Track:** Browser & DOM fundamentals  
**Level:** Easy  
**Time:** about 20 minutes  
**Reported at:** Flipkart

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/predict-which-color-wins-specificity-important-and-cascade-layers)**: free, no account needed.

## Problem

Every case below styles the same markup, unless a case says otherwise:

```html
<div class="card" id="box">
  <p class="text" id="t">Hello</p>
</div>
```

For each case, decide which color the paragraph `#t` ends up with, **without running it**. Fill in `answers.a` to `answers.h` with `"red"`, `"blue"`, `"green"` or `"purple"`.

```css
/* Case A */
.card .text { color: red; }
p.text { color: blue; }

/* Case B */
:where(#box) .text { color: red; }
.text { color: blue; }

/* Case C */
:is(#box, .card) .text { color: red; }
div .text.text { color: blue; }

/* Case D */
@layer base, components;
@layer components { #box #t { color: red; } }
.text { color: blue; }

/* Case E */
@layer base, components;
@layer components { .text { color: green; } }
@layer base { #box #t.text { color: red; } }

/* Case F */
@layer base, components;
@layer base { .text { color: red !important; } }
@layer components { .text { color: green !important; } }
.text { color: blue !important; }

/* Case G: the paragraph is <p class="text" id="t" style="color: purple"> */
#t { color: red !important; }

/* Case H */
#box { color: red; }
p { color: blue; }
```

## Starter code

```js
const answers = {
  a: "",
  b: "",
  c: "",
  d: "",
  e: "",
  f: "",
  g: "",
  h: "",
};

// Try it: render one case and look at the preview.
document.getElementById("root").innerHTML = `
  <style>.card .text { color: red; } p.text { color: blue; }</style>
  <div class="card" id="box"><p class="text" id="t">Hello</p></div>`;
```

## Hints

<details><summary>Hint 1</summary>

The cascade is a checklist, not just specificity. Work out which step decides each pair before counting anything.

</details>

<details><summary>Hint 2</summary>

Order of checks: importance, inline style, layer order, specificity (IDs, classes, elements), then source order. Stop at the first step where the two declarations differ.

</details>

<details><summary>Hint 3</summary>

Remember `:where()` adds zero specificity while `:is()` takes its most specific argument, layers beat specificity for normal rules but invert for `!important`, and a rule on a parent only inherits.

</details>

## Solution

The full answer is free on FrontendPro: [Predict which color wins: specificity, !important and cascade layers](https://frontend.nextjoblist.com/questions/predict-which-color-wins-specificity-important-and-cascade-layers). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20180%5D%20).
