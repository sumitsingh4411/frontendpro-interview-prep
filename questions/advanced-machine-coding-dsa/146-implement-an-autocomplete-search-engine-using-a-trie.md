# Implement an autocomplete search engine using a Trie

**Track:** Advanced machine coding & DSA  
**Level:** Hard  
**Time:** about 60 minutes  
**Reported at:** Google, Uber

**[Solve it in the browser with tests](https://uiround.com/questions/implement-an-autocomplete-search-engine-using-a-trie)**: free, no account needed.

## Problem

Implement a `Trie` class that powers search-box suggestions:

- `insert(word, weight = 1)`: add a word, or add `weight` to an existing word's score (for example its search count).
- `search(word)`: `true` if the exact word was inserted.
- `startsWith(prefix)`: `true` if any inserted word starts with `prefix`.
- `delete(word)`: remove the word and return `true` (or `false` if absent). Remove nodes that no longer lead to any word.
- `suggest(prefix, limit = 5)`: up to `limit` words starting with `prefix`, highest score first, ties in alphabetical order.
- `size`: the number of distinct words.

Everything is **case-insensitive**: store and compare lower-case. It must stay fast with 50,000 words.

```js
const trie = new Trie();
trie.insert("react", 50);
trie.insert("redux", 20);
trie.insert("react native", 30);
trie.suggest("re"); // ["react", "react native", "redux"]
```

## Starter code

```js
class Trie {
  insert(word, weight = 1) {}
  search(word) {}
  startsWith(prefix) {}
  delete(word) {}
  suggest(prefix, limit = 5) {}
  get size() {}
}
```

## Hints

<details><summary>Hint 1</summary>

Think about what many words share. Storing each word separately repeats work that a shared structure could do once.

</details>

<details><summary>Hint 2</summary>

Use nodes keyed by character, with the end node holding the weight. For suggestions, jump to the prefix node and collect words from that subtree, keeping only the top results.

</details>

<details><summary>Hint 3</summary>

Lower-case everything, `delete` must prune nodes that no longer lead to a word, and insert on an existing word adds to its score. Order by score, then alphabetically.

</details>

## Solution

The full answer is free on UIRound: [Implement an autocomplete search engine using a Trie](https://uiround.com/questions/implement-an-autocomplete-search-engine-using-a-trie). It has a tested solution, a step-by-step explanation, edge cases, follow-up questions with model answers, and the tests to run your own code against.

Found a mistake in this question? [Report it](https://github.com/sumitsingh4411/uiround-interview-prep/issues/new?template=content-error.yml&title=%5BQuestion%20146%5D%20).
