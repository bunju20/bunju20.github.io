---
title: Leetcode 392. Is Subsequence
date: 2023-07-19 13:40:00 +09:00
categories: [coding test,leetcode]
tags:
  [
    leetcode
  ]


---

# 내풀이

```js
/*
solution:
- 포인터 두개 두고
- for문 돌면서
  - 만약에 두 값이 같으면 sIdx++;
- return sIdx === s.length; 
time O(N)
space: O(1)

*/

var isSubsequence = function(s, t) {
  if(s.length === 0) return true;
  if(s.length > t.length) return false;

  let sIdx = 0;
  for(let tIdx = 0; tIdx < t.length; tIdx++) {
    if(s[sIdx] === t[tIdx]) {
      sIdx++;
    }
  }
  return sIdx === s.length;
};
```

