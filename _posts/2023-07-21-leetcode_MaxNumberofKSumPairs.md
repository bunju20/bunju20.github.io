---
title: Leetcode 1679. Max Number of K-Sum Pairs
date: 2023-07-21 20:40:00 +09:00
categories: [coding test,leetcode]
tags:
  [
    leetcode
  ]
---

# 내풀이

```js
var maxOperations = function (nums, k) {
    nums.sort((a,b)=>a-b)
    let res=0
    let left=0
    let right =nums.length-1
    while(left<right){
        let sum =nums[left]+nums[right]
        if(sum<k){
            left++
        }else if(sum>k){
            right--
        }else{
            res++
            left++
            right--
        }
    }
    return res
};
```

