---
title: Leetcode 334. Increasing Triplet Subsequence
date: 2023-07-16 16:24:00 +09:00
categories: [coding test,leetcode]
tags:
  [
    leetcode
  ]


---

# 내풀이

```js
/*
I: int array
O: bool
C:
1 <= nums.length <= 5 * 105
-231 <= nums[i] <= 231 - 1
E:if(nums.length <=2)return false;

ds:x
algo: 
solution:
4:16 ~ 4:26
- 한 idx를 기준으로 왼쪽에 작은거, 오른쪽에 큰거 있으면 되는거임.
- 왼쪽에서 지나오면서 min을 갱신해. -> 배열
- 오른쪽에서 지나오면서 max를 갱신해 -> 배열
- 현재 배열에서 현재 값이 min배열보다 크고 max배열보다 작은게 하나라도 있으면 true
- 아니면 false

배열의 길이: N
time: O(N)
space: O(N)

*/

var increasingTriplet = function(nums) {
  if(nums.length <= 2)return false;
  let min = new Array(nums.length).fill(Infinity);
  let max = new Array(nums.length).fill(-Infinity);
  min[0] = nums[0];
  max[nums.length-1] = nums[nums.length-1];
  for(let i = 1; i < nums.length; i++)min[i] = Math.min(min[i-1], nums[i]);
  for(let i = nums.length-2; i >= 0; i--)max[i] = Math.max(max[i+1], nums[i]);
  
  for(let i = 0; i < nums.length; i++){
      if(nums[i] > min[i] && nums[i] < max[i])return true;
  }
  return false;
};
```

> 시간복잡도는 당연히 O(N)이 나오게 만들어야 하니 위와같이 만들었다.
> 암만 생각해봐도 포인터 3개로 공간을 줄일수 있을 것같은데 떠오르지 않았다. 
>
> 분명... 더... 좋은 방법이 있을건데...

   <img src="https://raw.githubusercontent.com/bunju20/image_server/main/img_/images.jpeg" alt="images" style="zoom:150%;" />    > 

   

:bulb: 일단 **위의 풀이의 컨셉은 다음과 같다.**

* 한개의 원소를 기준으로 왼쪽에 원소보다 작은값, 오른쪽에 원소보다 큰 값이 있으면 된다.
* 따라서 해당 인덱스에서 여태까지 왼쪽에서 본것중 제일 작은 값을 원소에 표시하는 min배열과
* 오른쪽에서 볼것중 큰 값들을 원소에 표시하는 max배열을 만들어서
* nums배열과, min,max배열을 같은 인덱스로 반복하며 해당 인덱스에 있는 원소가 타당한 원소면 true, 아니면 false를 반환하게 한다.

   

# Optimal Solution

> 공간을 `O(N)` => `O(1)`으로 줄일수 있는 솔루션이다.

```js
var increasingTriplet = function(nums) {
  let firstNumber = Infinity;
  let secondNumber = Infinity;
  
  for (let currentNumber of nums) {
    if (currentNumber > secondNumber && currentNumber > firstNumber) {
      return true;
    }
    if (currentNumber > firstNumber) {
      secondNumber = currentNumber;
    } else {
      firstNumber = currentNumber;
    }
  }
  return false;
};
```

![image-20230716164612878](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230716164612878.png)

![image-20230716164618274](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230716164618274.png)

![image-20230716164623517](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230716164623517.png)

> 해당 알고리즘의 개념은 아래와 같다.
>
> ```
> 3개의 포인터 1,2,3이 있는데 
> * 3을 읽고있는데 1,2가 모두 3보다 작으면 true
> * 1보다 3이 크면 2 = 3
> * 이외에는 1 = 3
> ```
>
> 즉, 
>
> * 세개의 포인터가 모두 오름차순이면 true
> * 현재 보는게 제일 작은 포인터보다 크다면 현재 포인터를 두번째로 작은 포인터로 만들고
>
> * 3이 1보다 작거나 같으면 3개가 오름차순이라는게 성립하지 않으니까
>   1을 3으로 바꿔준다.
>
> 라고 보면 된다.

![image-20230716171811104](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230716171811104.png)

```
이 예시로 설명하면 다음과 같다.
[2,1,5,0,4,6]
 ` (infinity) - first
 ` (infinity) - second
 `
 
[2,1,5,0,4,6]
 ^
 `
 ^
 
 [2,1,5,0,4,6]
    ^
 `   
    ^ => 현재거가 더 작으니까 first를 바꾸자!

 [2,1,5,0,4,6]
    ^
      ^
      ^
 [2,1,5,0,4,6]
    ^
      ^
        ^ => 현재거가 더 작으니(이하생략)
 [2,1,5,0,4,6]
        ^
          ^
          ^
 [2,1,5,0,4,6]
        ^
          ^
            ^ => 오 현재것보다 first와 second가 다르니 true반환!
            
           
```

> 다음엔 시간을 좀 더 쓰더라도 그림을 하나하나 그려가면서 생각해보자.

