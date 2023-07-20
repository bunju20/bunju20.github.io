---
title: Leetcode 11. Container With Most Water
date: 2023-07-20 21:40:00 +09:00
categories: [coding test,leetcode]
tags:
  [
    leetcode
  ]



---

# 내풀이

```js
var maxArea = function(height) {
    if(height.length === 2)return Math.min(height[0],height[1]);

    let l = 0;
    let r = height.length - 1;
    let max = -Infinity;
    
    while(l < r){
        let curAmount = (r-l) * Math.min(height[l],height[r]);
        max = Math.max(max,curAmount);
        if(height[l] < height[r])l++;
        else r--;
    }
    return max;

};
```

