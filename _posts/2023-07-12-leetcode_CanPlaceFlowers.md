---
title: Leetcode 605. Can Place Flowers
date: 2023-07-13 12:21:00 +09:00
categories: [coding test,leetcode]
tags:
  [
    leetcode
  ]

---

# 내풀이

```js
var canPlaceFlowers = function(flowerbed, n) {
  if (n === 0)return true;
  const length = flowerbed.length;
  let count = 0;
  let i = 0;

  while (i < length) {
    let condition = flowerbed[i] === 0 &&(i === 0 || flowerbed[i - 1] === 0) && (i === length - 1 || flowerbed[i + 1] === 0);
    
    if (condition) {
      flowerbed[i] = 1;
      count++;
    }
    if (count >= n)return true;
    i++;
  }

  return false;
};

```

 :white_check_mark: **Edge Case**

> n = 0 일때 처리.

:pen: **Solution**

> - i가 중간 idx라고 할때 (맨앞일때 맨 뒤일때 처리) 걔네가 다 0이면
> - 중간놈을 1로 바꿔주고, count++;
> - count가 n이상이면 true; i++;
>
> =>return false;

   

# 다른 솔루션

```js
var canPlaceFlowers = function(flowerbed, n) {
  for (let i = 0; i < flowerbed.length && n !== 0; i++) {
    if (
      flowerbed[i] === 0 &&
      flowerbed[i - 1] !== 1 &&
      flowerbed[i + 1] !== 1
    ) {
      n--;
      i++;
    }
  }
  return n === 0;
};
```

**:sweat: solution짤때 막 짜지말고 생각을 좀 더 해보자...**

> * for문 돌면서
>   * if(가운데거 , 왼쪽, 오른쪽 0이면)
>   * n --, i++
> * n == 0이면 true; 아니면 false;

= 로직은 동일하다.