# Truncate text with an ellipsis on one line and clamp it to three lines

**Track:** HTML & CSS  
**Level:** Easy  
**Time:** about 15 minutes

**[Solve it in the browser with tests](https://frontend.nextjoblist.com/questions/truncate-text-with-an-ellipsis-on-one-line-and-clamp-it-to-three-lines)**: free, no account needed.

## Problem

Cards in a feed have a fixed size, but titles and excerpts do not. The usual fix is to cut the title to one line with "…" and the excerpt to three lines. Write the CSS for this card.

Write a React component **`ArticleCard({ title, date, excerpt })`** that renders exactly this markup, plus a `<style>` element with your CSS as the first child of the article:

```html
<article class="card">
  <style>/* your CSS */</style>
  <header class="card-header">
    <h3 class="card-title" title="{title}">{title}</h3>
    <time class="card-date" datetime="{date}">{date}</time>
  </header>
  <p class="card-excerpt">{excerpt}</p>
</article>
```

Rules the tests check:

- The card is as wide as its container (no fixed width).
- `.card-header` is a flex row: the title on the left, the date on the right. The date is always fully visible, even when the title is very long.
- `.card-title` stays on one line. When it is too long, it ends with an ellipsis (`text-overflow: ellipsis`), and its `title` attribute holds the full text so it can still be read on hover.
- `.card-excerpt` shows at most three lines and is cut after the third, using `-webkit-line-clamp: 3`. A short excerpt keeps its natural height.
- Both the title and the excerpt use `font-size: 16px` and `line-height: 24px`, and have no margin.

## Starter code

```jsx
const CSS = `
/* Your CSS here */
`;

function ArticleCard({ title, date, excerpt }) {
  return (
    <article className="card">
      <style>{CSS}</style>
      <header className="card-header">
        <h3 className="card-title" title={title}>
          {title}
        </h3>
        <time className="card-date" dateTime={date}>
          {date}
        </time>
      </header>
      <p className="card-excerpt">{excerpt}</p>
    </article>
  );
}

// Preview
function App() {
  return (
    <div style={{ width: 320, fontFamily: "sans-serif" }}>
      <ArticleCard
        title="How we cut our bundle size in half without rewriting a single component"
        date="2026-03-02"
        excerpt="We measured first, then removed two date libraries, split the editor into its own chunk and moved icons to a sprite. Each change was small. Together they took the main bundle from 410 kB to 190 kB and made the first load a second faster on mid-range phones."
      />
    </div>
  );
}
```

## Hints

<details><summary>Hint 1</summary>

A single-line ellipsis needs three things at once: the text must not wrap, the overflow must be hidden, and only then does text-overflow have something to replace.

</details>

<details><summary>Hint 2</summary>

For several lines, the -webkit-line-clamp property does the counting. It works together with display: -webkit-box, -webkit-box-orient: vertical and overflow: hidden.

</details>

<details><summary>Hint 3</summary>

A flex item will not shrink below its content width while overflow is visible, so the title pushes the date out. Hidden overflow lets it shrink. Keep the full title in a title attribute.

</details>

## Solution

The full answer is free on FrontendPro: [Truncate text with an ellipsis on one line and clamp it to three lines](https://frontend.nextjoblist.com/questions/truncate-text-with-an-ellipsis-on-one-line-and-clamp-it-to-three-lines). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/frontendpro-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20957%5D%20).
