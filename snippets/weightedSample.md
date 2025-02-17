---
title: weightedSample
tags: array,random,advanced
firstSeen: 2019-12-31T11:34:26+02:00
lastUpdated: 2020-10-22T20:24:44+03:00
---

Gets a random element from an array, using the provided `weights` as the probabilities for each element.

- Use `Array.prototype.reduce()` to create an array of partial sums for each value in `weights`.
- Use `Math.random()` to generate a random number and `Array.prototype.findIndex()` to find the correct index based on the array previously produced.
- Finally, return the element of `arr` with the produced index.

```js
const weightedSample = (arr, weights) => {
  const roll = Math.random();
  return arr[
    weights
      .reduce(
        (acc, w, i) => (i === 0 ? [w] : [...acc, acc[acc.length - 1] + w]),
        []
      )
      .findIndex((v, i, s) => roll >= (i === 0 ? 0 : s[i - 1]) && roll < v)
  ];
};
```

```js
weightedSample([3, 7, 9, 11], [0.1, 0.2, 0.6, 0.1]); // 9
```
