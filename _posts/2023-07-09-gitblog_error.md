---
title: 깃허브 블로그Github Page commit 되돌아가기
date: 2023-07-09 14:21:00 +09:00
categories: [error,githubpage]
tags:
  [
    error, githubpage, blog, commit, push
  ]
---

  # 깃허브 블로그 오류

```
404
File not found

The site configured at this address does not contain the requested file.

If this is your site, make sure that the filename case matches the URL as well as any file permissions.
For root URLs (like http://example.com/) you must provide an index.html file.

Read the full documentation for more information about using GitHub Pages.

GitHub Status — @githubstatus
```

블로그를 꾸미다가 뭘 잘못 건들였는데 이런 화면이 뜨면서 뭐가 잘못 됐을 때의 해결 방법이다. 원래 커밋으로 돌아가면 되는게 결론이니 그 내용만 원하면 맨 아래로 가자. 

일단... 저 문제가 왜생겼나부터 짚고 넘어가자.

   

깃허브 블로그의 사이드바를 일렁거리는 모양으로 만들고싶어서,  commons.scss파일을 변경해서

```js
#sidebar {
  @include pl-pr(0);

  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  overflow-y: auto;
  width: $sidebar-width;
  z-index: 99;
  background: var(--sidebar-bg);

  /* Hide scrollbar for Chrome, Safari and Opera */
  &::-webkit-scrollbar {
    display: none;
  }
```

위와같은 코드를

```

  background: linear-gradient(to bottom, #0077ff, #00aaff);
  background-size: 100% 200%;
  animation: gradient 2s linear infinite;

@keyframes gradient {
  0% {background-position: 0% 50%;}
  50% {background-position: 100% 50%;}
  100% {background-position: 0% 50%;}
}

```

위와같은 값을 넣어서 추가하였다. 그런데 왠걸, 블로그 들어가니까 사이드 바는 끄떡없고 불쌍한 다른 포스팅만 404가 뜨는 것이 아닌가. 아마 코드상에서 문법오류가 있었던것 같다.

   

jekyll은 사이트를 빌드할때 scss파일을 css로 컴파일한다. 즉 이 과정에서 문제가 생기면, 결과로 생성되는 HTML파일이 부분적, 전체적으로 정상적인 생성을 하지 못할수도 있다.

> 즉 페이지는 못찾고 이게 404에러로 이어진다.  뭐를 하나를 바꿨으면 바로 두근거리면서 git push하지 말고 로컬에서 블로그 어떻게 변했는지 확인하고 빌딩을 해야한다는 당연한 사실을 알 수 있었다. :pensive:



### 그래서 뭐가 문제인가

---

원래 커밋으로 되돌아가서 push했고 빌딩을 했는데도 어찌된게 사이트가 업데이트도 안하고 가만히 있다.

![image-20230707034617421](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230707034617421.png)

위와같은 문제있는 파일이 있어서 

```
git reset <commit-id>
git stash
git push --force origin main
```

위와 같이 돌아갔는데,  push를 해도 `어 선생님 이거 그대론데용` 하면서 아무것도 해주지 않는다.

> 당연하다.
> `git reset <commit-id>`를 사용하면 로컬 저장소의 HEAD를 해당 커밋으로 이동시키지만, 이것은 파일 시스템의 상태를 변경하는게 아니다.
>
> git reset 명령은 주어진 커밋으로 현재 HEAD를 이동시키는데, 이때 --soft, --mixed, --hard 같은 옵션을 추가하면 Git이 어떻게 동작할지를 조절할 수 있다.
>
> 따라서 .scss 파일을 특정 커밋의 상태로 완전히 되돌리려면 git reset --hard <commit-id>를 사용해야 했다. 이와 같은 이유로 커밋을 되돌려도 원래 있던 대로 파일이 변화하지 않은 것이다.

즉 위의 코드에서 

```
git reset --hard <commit-id>
git stash
git push --force origin main
```

위와 같이 수정하면 제대로 돌아간다.



---

2023-07-06

> 오늘도 동일한 오류가 생겨서 위와 같이 했는데 이상하게 블로그가 업데이트가 안됐다.

깃허브의 Action에 들어가서
![image-20230726000734206](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230726000734206.png)

잘들어갔을때로 들어가서

![image-20230726000824635](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230726000824635.png)

Re-run을하면 블로그가 제기능을 하는걸 알수있다.

> 왜그러는진 나도 잘 모르겠다...
