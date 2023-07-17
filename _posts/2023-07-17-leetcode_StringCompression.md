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
solution은 아래에
time:O(N)
space:O(1)
*/
var compress = function(chars) {
    let write = 0, start = 0;
    
    for (let read = 0; read <= chars.length; read++) {
        if (read === chars.length || chars[read] !== chars[start]) {
            chars[write++] = chars[start];
            if (read > start + 1) {
                let count = '' + (read - start);
                for (let i = 0; i < count.length; i++) {
                    chars[write++] = count[i];
                }
            }
            start = read;
        }
    }
    console.log(chars)
    return write;
};
         
```

> `write` : 새로운 문자나 그룹의 길이를 기록할 위치를 가리킴
>
> `start`: 현재 읽고 있는 그룹의 시작 위치를 나타냄.
>
> * `read`포인터를 0부터 시작해서 배열의 끝까지 이동하면 문자를 읽는다.

```js
solution:

["a","a","b","b","c","c","c"]
  ^ start
  ^ write
  ^ read

["a","a","b","b","c","c","c"]
  ^ start
  ^ write
      ^ read

["a","a","b","b","c","c","c"]
  ^ start
  ^ write
          ^ read (start와 다르군!)
            read가 start의 +1보다 크니까 count를 써야지!
            for문 돌면서 count의 count의 수만큼 char[write]에 숫자를 넣어주고 write++
            start = read

["a","2","b","b","c","c","c"]
          ^ start
          ^ write
          ^ read

["a","2","b","b","c","c","c"]
          ^ start
          ^ write
              ^ read
["a","2","b","2","c","c","c"]
                  ^ start
                  ^ write
                  ^ read

["a","2","b","2","c","c","c"]
                  ^ start
                  ^ write
                      ^ read
["a","2","b","2","c","c","c"]
                  ^ start
                  ^ write
                          ^ read (끝까지 왔군.)
                          count의 수만큼으로 write를 채워준다.
["a","2","b","2","c","3","c"]
                  ^ start
                      ^ write

이렇게 해서 write를 리턴해주면 끝!
```



![images](https://raw.githubusercontent.com/bunju20/image_server/main/img_/images-1689581932136-1.jpeg)

> 결과값이 ["a","2","b","2","c","3","c"]이 나오는데... 테스트 케이스에는 이걸 ["a","2","b","2","c","3"]이라고 올려놨다. 반환하는 값으로 잘랐다고 판단하는건 알겠지만, 혼동이 올 수 밖에 없게 문제를 만들어놨다. 실제로 반환하는 배열의 모양이 아닌데도 그걸 결과로 올려놨고.
>
>    
>
> 워... 이런문제가 다있네 하면서 풀었다. leetcode에서 푼 문제중에 테스트케이스가 가장 별로인 문제였던것 같다. 다른 솔루션도 크게 다른 것 같진않아서 오늘은 optimal solution을 정리하진 않겠다 :stuck_out_tongue_closed_eyes:

   

#### :happy: 추천수는 거짓말을 하지 않는다.

![image-20230717171941251](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230717171941251.png)

