---
title: Leetcode 643. Maximum Average Subarray I
date: 2023-07-22 20:40:00 +09:00
categories: [coding test,leetcode]
tags:
  [
    leetcode
  ]

---

# 내풀이

```js
var findMaxAverage = function(nums, k) {
  let l = 0;
  let r = 0;
  let max = -Infinity;
  let curNum = 0;
  for (let i = 0; i < nums.length; i++) {
    if (r < k) {
      curNum += nums[r++];
    } else {
      max = Math.max(max, curNum);
      curNum += nums[r++] - nums[l++];
    }
  }
  max = Math.max(max, curNum);
  return max / k;
};
```

