---
title: Leetcode 1456. Maximum Number of Vowels...
date: 2023-07-23 14:40:00 +09:00
categories: [coding test,leetcode]
tags:
  [
    leetcode
  ]

---



# 내풀이

```js
var maxVowels = function(s, k) {
    let set = new Set(['a','e','i','o','u']);
    let l = 0;
    let r = 0;
    let max = 0;
    for(r; r < k; r++){
        if(set.has(s[r]))max++;
    }

    let curNum = max;
    while(r < s.length){
      if(set.has(s[r]))curNum++;
      if(set.has(s[l]))curNum--;
      r++;l++;
      max = Math.max(max, curNum);
    }
    return max;

  };
```

