---
title: react native로 잠금화면 설정하기
date: 2023-07-15 16:10:00 +09:00
categories: [toy,bossle]
tags:
  [
    project, react native, 잠금화면, 배경화면
  ]

---

# react native로 잠금화면?

> 먼저 결론부터 말하자면 react native**'만'** 사용해서 잠금화면을 설정하는건 불가능하다.

React Native는 앱의 UI를 빌드하고, 사용자 입력을 처리하며, 네트워크 요청을 보내고 받는 등의 기본적인 모바일 앱 기능을 처리할수 있다. 

단, OS에 대한 깊은 수준의 액세스 권한이 필요한 작업에 대해서는 제한이 있다.그래서 방법은 두가지이다.

```
1. react native를 사용하고, 직접 네이티브 모듈을 연동한다.(좀 복잡)
2. react native말고 플러터를 사용한다. (간단)
```

>  `react native`를 많이 다뤄봤으므로 가급적 눈가리고 1번을 하고싶으니... 일단 알아보긴 하자.



### 0. 오픈소스

https://github.com/danimahardhika/wallpaperboard

> 사실상 우리가 구현하려는 기능은 전부 여기에있음. 이 코드를 잘 분석해서 배경화면이 아니라 잠금화면을 변경하게 하면 됨.
> 사이즈가 크고... 사이즈가 큰게 단점. 라이센스문제도 있다. (하지만 제일 좋음.)

https://github.com/muzei/muzei

> 여기에 있는 오픈소스 가져와서 배경화면 업데이트 부분만 가져올수 있음.

https://developer.android.com/reference/android/app/WallpaperManager

> 그냥 이거 보고  WallpaperManager클래스 사용해서 배경화면 변경할수도 있음. 앱에서 이미지를 선택하고 해당 이미지를 배경화면으로 설정하는 기능을 구현할 수 있음.

미완성
https://github.com/iamgauravn/Wallpaper_Maker



### 1. 오픈소스 분석

https://github.com/danimahardhika/wallpaperboard

> 위에걸 한번 써보자!
