---
title: notion으로 REST APIs 디자인하기
date: 2023-07-15 20:40:00 +09:00
categories: [study,api]
tags:
  [
    notion, api, apis, 설계
  ]

---

# REST API가 뭐지?

**API**

> 다른 소프트웨어가 특정 프로그램이나 응용 프로그램과 통신할수 있도록 하는 방법

   

**REST(Representational State Transfer)API**

> 웹 서비스 간에 정보를 주고받는 방식 중 하나로, 웹의 기본 아키텍처와 동일한 아키텍처를 따른다.



**:bulb:어떤 작업을 수행할 수 있나?**

```js
GET: 서버에서 정보를 가져오는 데 사용.
POST: 서버에 새로운 정보를 생성하도록 요청하는 데 사용.
PUT: 서버의 기존 정보를 업데이트하는 데 사용.
DELETE: 서버의 정보를 삭제하는 데 사용.
```

   

# 어떻게 작성하나?

> REST API를 설계하는데에도 rule이 있다. 아래는 api를 설계할때 지켜야할 내용들이다.

1. **소문자를 사용**

```
❌https://bunju20.github.io/posts/FirstPost/Post-Comments
⭕https://bunju20.github.io/posts/FirstPost/post-comments
```

> 이는 일관성과 가독성, 호환성을 위함이다.
> **호환성** 측면에서 좀 더 설명하자면, URL은 대소문자를 구분하지 않는경우가 많은데, 대부분의 웹서버는 대소문자를 구분해서 오류가 발생할 수 있다.

   

2. **언더바 대신 하이픈**

```
❌ https://bunju20.github.io/posts/FirstPost/post_comments
⭕ https://bunju20.github.io/posts/FirstPost/post-comments
```

> 언더바는 가려지거나 숨겨질 수있으므로 언더바 대신 하이픈을 사용한다. 같은 맥락으로 내 포스팅을 보면 대부분의 파일명을 언더바로해서 주소가 언더바로 구성되어있는걸 확인할 수 있는데... 수정하는 것이 좋다.

   

3. **마지막에 /(슬래시)는 포함하지 않기**

```
❌ https://bunju20.github.io/posts/FirstPost/
⭕ https://bunju20.github.io/posts/FirstPost
```

> 일관성, 가독성 측면도 있지만
> URL은 리소스의 고유 식별자여서 서로 다르면 리소스도 다르다고 간주한다. 즉 동일한 리소스에 대해서 두가지 형식을 사용하면 리소스가 중복될 수 있다.

   

4. **행위를 포함하지 않기**

```
❌ POST http://dev-cool.tistory.com/users/post/1
⭕ PUT http://dev-cool.tistory.com/users/1
```

> 행위는 URL이 아니라 Meathod를 사용해서 전달한다.



---

**참고사이트**

https://cocoon1787.tistory.com/540