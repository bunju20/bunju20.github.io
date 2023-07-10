---
title: Leetcode 1768.Merge Strings Alternately
date: 2023-07-09 16:21:00 +09:00
categories: [coding test,leetcode]
tags:
  [
    leetcode
  ]

---

# 내 풀이

```javascript
/**
 * @param {string} word1
 * @param {string} word2
 * @return {string}
 */

 /*
 14:39 ~ 14:47
I: string두개
O: 병합된 string 한개
C:
1 <= word1.length, word2.length <= 100
word1 and word2 consist of lowercase English letters.
E:x

algo:two pointer
ds:x

solution:
- 두개의 포인터 만듬
- while(둘중의 하나가 끝까지 보기전까지)
    - word1 푸시 l++
    - word2 푸시 r++
- l과 r의 남은걸 측정
- 남은 놈들만 더해서 배열에 추가
- return 배열을 string으로 만듦.

N: 가장 긴 문자열의 길이
time: O(N)
space: O(N)
 */
var mergeAlternately = function(word1, word2) {
    let l = 0;
    let r = 0;
    let result = [];
    while(l < word1.length && r < word2.length){
        result.push(word1[l]);
        result.push(word2[r]);
        l++;
        r++;
    }
    let leftL = word1.length - l;
    let leftR = word2.length - r;
    if(leftL)result.push(word1.slice(l));
    if(leftR)result.push(word2.slice(r));
    return result.join('');

};
```

# 다른 solution 분석

> 위의 코드가 로직상 optimal이라 밑의 코드는 시간, 공간 복잡도에서의 이득은 없음.
> 아래 코드는 solution 상에서는 O(N)이라고 했지만, string에 char을 += 한다. string의 불변성으로 인해서 더할 때 마다 O(N)의 시간복잡도가 발생. 즉, 가장 긴 문자열의 길이가 N이라고할때
>
> `O(N^N)`이 가능해짐. 즉 시간복잡도가 비효율적임.

```js
const mergeAlternately = (a, b) => {
  const maxLength = Math.max(a.length, b.length)
  let result = ''

  for (let i = 0; i < maxLength; i++) {
    result += (a[i] ?? '') + (b[i] ?? '')
  }

  return result
}
```

`maxLength` : 더 긴 배열의 길이를 저장. 

`result`: 빈배열 (str도 push처럼 쓸수있으므로)

> for문을 돌면서 각 요소를 번갈아가며 추가한다. 
>
>  `(a[i] ?? '')`는 `a` 배열의 `i`번째 요소를 가져오는데, 만약 해당 요소가 존재하지 않으면 빈 문자열(`''`)을 대신 사용

:bulb: 위의 코드에서 result를 배열로 선언하고, +=대신 push를 하고, return 할때 join('')을 하면 시간복잡도는 적고 간결한 코드가 된다.

