# Mark up a recipe page with semantic HTML only

**Track:** HTML & CSS  
**Level:** Easy  
**Time:** about 15 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/mark-up-a-recipe-page-with-semantic-html-only)**: free, no account needed.

## Problem

Screen readers, search engines and reader modes understand a page through its elements, not its classes. A recipe built from `<div>`s looks fine but gives them nothing. Mark one up with semantic HTML only.

Write a React component **`RecipePage({ recipe })`**. `recipe` looks like this (`tip` is optional):

```js
{
  title: "Masala chai",
  summary: "Spiced milk tea simmered on the stove.",
  author: "Asha Rao",
  published: "2026-02-10",
  prepMinutes: 5,
  cookMinutes: 75,
  servings: 2,
  image: { src: "/chai.jpg", alt: "Two glasses of chai on a steel tray", caption: "Serve it hot." },
  ingredients: ["2 cups water", "1 cup milk", "2 tsp tea leaves"],
  steps: ["Boil the water with the spices.", "Add the tea and simmer.", "Add the milk and strain."],
  tip: "Crush the cardamom just before you use it.",
}
```

Render this structure:

- One `<main>` that contains one `<article>`.
- The article's `<header>` holds an `<h1>` with the title, a `<p>` with the summary, and a `<p>` that reads `By Asha Rao on 10 February 2026`, where the date is a `<time datetime="2026-02-10">`. Format the date as day, full month name and year (`en-GB`, read in UTC).
- A `<figure>` with an `<img>` (its `src` and `alt`) and a `<figcaption>` with the caption.
- A `<dl>` with three pairs, in this order: `Prep time`, `Cook time`, `Serves`. The two times are `<time>` elements with an ISO 8601 duration in `datetime` and readable text:
  - under 60 minutes: `datetime="PT5M"`, text `5 min`
  - 60 or more: `PT1H15M` and `1 hr 15 min`; a whole hour is `PT1H` and `1 hr`
- A `<section>` whose `<h2>` reads `Ingredients`, with the ingredients in a `<ul>`.
- A `<section>` whose `<h2>` reads `Method`, with the steps in an `<ol>`.
- Each section is named by its heading: `aria-labelledby` points at the `<h2>`'s `id`. Ids must be unique when two recipes render on one page.
- If there is a `tip`, an `<aside>` with an `<h2>` reading `Tip` and a `<p>` with the text. No tip, no aside.
- Use no `<div>`, `<span>` or `<br>` anywhere, and exactly one `<h1>`.

## Starter code

```jsx
import { useId } from "react";

function RecipePage({ recipe }) {
  // Replace the div with semantic markup.
  return <div className="recipe">{recipe.title}</div>;
}

// Preview
const CHAI = {
  title: "Masala chai",
  summary: "Spiced milk tea simmered on the stove.",
  author: "Asha Rao",
  published: "2026-02-10",
  prepMinutes: 5,
  cookMinutes: 15,
  servings: 2,
  image: { src: "https://picsum.photos/seed/chai/480/240", alt: "Two glasses of chai on a steel tray", caption: "Serve it hot." },
  ingredients: ["2 cups water", "1 cup milk", "2 tsp tea leaves", "2 cardamom pods", "Sugar to taste"],
  steps: ["Boil the water with the crushed cardamom.", "Add the tea leaves and simmer for 2 minutes.", "Add the milk and sugar, bring to a boil and strain."],
  tip: "Crush the cardamom just before you use it.",
};
function App() {
  return <RecipePage recipe={CHAI} />;
}
```

## Hints

<details><summary>Hint 1</summary>

Before writing any tag, list the parts of the page: a title block, a picture, some facts, two lists and a side note. Each one has an element made for it.

</details>

<details><summary>Hint 2</summary>

Ingredients have no order, so they are a ul; steps do, so they are an ol. Facts like prep time are name and value pairs, which is what dl, dt and dd are for.

</details>

<details><summary>Hint 3</summary>

A time element needs a machine-readable datetime. Durations use the ISO form PT1H15M, not 75m. Also check that each section heading id is unique when two recipes render.

</details>

## Solution

The full answer is free on FrontendPro: [Mark up a recipe page with semantic HTML only](https://frontend.nextjoblist.com/questions/mark-up-a-recipe-page-with-semantic-html-only). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20956%5D%20).
