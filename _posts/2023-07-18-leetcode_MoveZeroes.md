---
title: Leetcode 443. String Compression
date: 2023-07-17 16:24:00 +09:00
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

[0,1,0,3,12]
 z = forZero
 n = forNum

  -if z가 0
    -n이 0이 아닐때까지 n++
    -n이 nums.length면 return
    -z와 n을 바꿈
    -z++
  -else
    -z++

time: O(N)
space: O(1)
*/

var moveZeroes = function(nums) {
  if(nums.length == 1)return nums;
  let zeroPnt = 0;
  let numPnt = 0;

  while(zeroPnt < nums.length && numPnt < nums.length){
    if(nums[zeroPnt] == 0){
      while(nums[numPnt] == 0){
        numPnt++;
        if(numPnt == nums.length)return nums;
      }
      [nums[zeroPnt],nums[numPnt]] = [nums[numPnt],nums[zeroPnt]]
    }
    zeroPnt++; numPnt++; 
  }
  return nums;

```

> 이번 코드는 충분히 optimal하게 나와서 다른 솔루션을 소개 하지 않아도 될 것같다. 따로 글로 로직을 설명하지는 않는다.
>
> 그림을 그려 설명하면 아래와 같다. 아래 예시를 이용한다.

![image-20230718121625469](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230718121625469.png)

![image-20230718123207724](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230718123207724.png)

![image-20230718123222528](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230718123222528.png)

![image-20230718123238418](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230718123238418.png)

![image-20230718123254321](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230718123254321.png)

![image-20230718123309397](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230718123309397.png)

![image-20230718123333725](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230718123333725.png)

![image-20230718123349952](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230718123349952.png)