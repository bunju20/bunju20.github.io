---
title: Leetcode 1431. Kids With the Greatest Number of Candies
date: 2023-07-12 15:21:00 +09:00
categories: [coding test,leetcode]
tags:
  [
    leetcode
  ]



---

# 내풀이

```js
/**
 * @param {number[]} candies
 * @param {number} extraCandies
 * @return {boolean[]}
 */
const kidsWithCandies = (candies, extraCandies) => {
  const ret = [];
  let max = 0;
  for (const val of candies) {
    val > max && (max = val);
  }
  for (let i = 0; i < candies.length; ++i) {
    ret.push(candies[i] + extraCandies >= max);
  }
  return ret;
};
```

