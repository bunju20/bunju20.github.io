---
title: Leetcode 1071. Greatest Common Divisor of Strings
date: 2023-07-11 21:21:00 +09:00
categories: [coding test,leetcode]
tags:
  [
    leetcode
  ]


---

# 내풀이

```js
/**
 * @param {string} str1
 * @param {string} str2
 * @return {string}
 */

 /*
 18:30 ~ 18: 50
 I: str1, str2
 O: 두개의 스트링을 나눌수 있는 제일큰 string 
 C:
 1 <= str1.length, str2.length <= 1000
str1 and str2 consist of English uppercase letters.
 E:x
 algo:x
 ds:x
 solution: 이거 옵티멀은 아니다
 - 짧은놈 긴놈 정하고
 - for(len = 0 ~ 작은놈 길이)
    if(작은놈하고 긴놈이 len으로 나눠떨어지면)
    subStr = 작은놈.slice(0,len)
    if(둘다 subStr로 잘 나눠진다면)return subStr;
    -> 안나눠지면 ''

checkDivide(str,subStr)
- for(subStr길이만큼 더함)
    - if(길이로 잘랐는데 그게 subStr이 아니면)return false;
-return true;

N : 가장 긴 문자열 길이
 time:O(N^2)
 space:O(N) -> string이므로

 */
var gcdOfStrings = function(str1, str2) {
    let shorter = str1.length <= str2.length ? str1 : str2;
    let longer = str1.length > str2.length ? str1 : str2;
    
    for (let len = shorter.length; len > 0; len--) {
        if (shorter.length % len === 0 && longer.length % len === 0) {
            let subStr = shorter.slice(0, len);
            if (checkDivide(shorter, subStr) && checkDivide(longer, subStr)) {
                return subStr;
            }
        }
    }
    return '';
};

function checkDivide(str, subStr) {
    for (let i = 0; i < str.length; i += subStr.length) {
        if (str.slice(i, i + subStr.length) !== subStr) {
            return false;
        }
    }
    return true;
}
```

   

# 다른 솔루션

```js
/**
 * @param {string} str1
 * @param {string} str2
 * @return {string}
 */
const gcdOfStrings = (str1, str2) => {
  if (str1 + str2 !== str2 + str1) return ''; //같은패턴으로 구성되어있는지
  const gcd = (a, b) => (0 === b ? a : gcd(b, a % b));
  return str1.substring(0, gcd(str1.length, str2.length));
};
```

**:bulb:유클리드 알고리즘**

> 두 양의 정수의 최대 공약수를 찾는 방법 중 하나
> **두 양의 정수 a와 b (a > b)에 대하여 a를 b로 나눈 나머지를 r이라 하면, a와 b의 최대공약수는 b와 r의 최대공약수와 같다는 것**
>
> = a와 b의 최대공약수를 구하는 것은 b와 a를 b로 나눈 나머지의 최대공약수를 구하는 것과 같다.이러한 방식으로 계속 반복하면, 결국 나머지가 0이 되는 시점에서의 나누는 수가 a와 b의 최대공약수가 된다.

 `gcd`는 두 인자 `a`와 `b`를 받아서 `b`가 0이 될 때까지 `a`와 `b`의 나머지로 재귀적으로 호출한다.

   

> 1. 같은 패턴인지 문자열을 더해서 확인하고
> 2. 최대공약수의 길이만 구하면 된다. 
>
> **:sweat: 1번은 꼭 알아두자.**