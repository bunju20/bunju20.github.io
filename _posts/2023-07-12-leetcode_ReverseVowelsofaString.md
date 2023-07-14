---
title: Leetcode 345. Reverse Vowels of a String
date: 2023-07-14 16:21:00 +09:00
categories: [coding test,leetcode]
tags:
  [
    leetcode
  ]

---



# 내풀이

```js
/*
I: string
O: 모음만 반전된 strig
C: 
1 <= s.length <= 3 * 105
s consist of printable ASCII characters.
-> 소문자도 대문자도 나타날수있다.
E:
if(s.length === 1)return s;

ds: set
algo: two pointer
solution:

- s를 배열
- l= 맨앞, r= 맨뒤
- 모음인지 아닌지 판별하는 함수
- while(l<r)
  - if(l이 모음 아니면)l++
  - if(r이 모음 아니면)r--
  - if(l이 모음이고 r이 모음이면){
    - swap
  }
-return s.join('')  

string의 길이: N
time:O(N)
space:O(N)
*/

var reverseVowels = function (s) {
  if (s.length === 1) return s;
  const vowels = new Set(["a", "e", "i", "o", "u", "A", "E", "I", "O", "U"]);
  const ar = s.split("");
  let l = 0;
  let r = ar.length - 1;
  while (l < r) {
    console.log(l,r)
    if (l<r&&!vowels.has(ar[l])) l++;
    if (l<r&&!vowels.has(ar[r])) r--;
    if (l<r&&vowels.has(ar[l]) && vowels.has(ar[r])) {
      [ar[l], ar[r]] = [ar[r], ar[l]];
      l++;
      r--;
    }

  }
  return ar.join("");
};
```

   

# 다른 솔루션

```js
var reverseVowels = function(s) {
    const vowels = s.split('').filter(a => /[aeiou]/i.test(a));
    return s.split(/[aeiou]/i).reduce((res, a) => res + a + (vowels.pop() || ''), '');
};
```

> `s.split('')`:  각 문자를 배열로 분리
>
> `.filter(a => /[aeiou]/i.test(a))` : filter함수를 이용해서 모음만 남긴다.
>
> - /[aeiou]/i : 대소문자를 무시하고 []안에 있는 것과 일치하는지 확인
> - test함수가 참인 요소만 남기고 걸러낸다.
>
> = 해당 배열엔 추출한 모든 모음이 포함됨.
>
> `s.split(/[aeiou]/i)` : 모음을 기준으로 분리
>
> `reduce((res, a) => res + a + (vowels.pop() || ''), '')` 
>
> * 각 배열을 순회하면서 하나의 값으로 줄여나감
> * vowls배열에서 가장 마지막 요소를 제거하고 반환하면서 진행함.
>
> = 최종적으로 뒤집한 문자열이 반환됨.

:thinking: 코드가 짧은 건 좋은데 가독성 측면에선 잘 모르겠다. 익숙해지면 괜찮을것 같기도?

