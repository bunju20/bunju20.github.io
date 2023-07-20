---
title: react native로 잠금화면 설정하기
date: 2023-07-15 16:10:00 +09:00
categories: [toy,bossle]
tags:
  [
    project, react native, 잠금화면, 배경화면, flutter
  ]

---

# react native로 잠금화면?

> 먼저 결론부터 말하자면 react native**'만'** 사용해서 잠금화면을 설정하는건 불가능하다.

React Native는 앱의 UI를 빌드하고, 사용자 입력을 처리하며, 네트워크 요청을 보내고 받는 등의 기본적인 모바일 앱 기능을 처리할수 있다. 

단, OS에 대한 깊은 수준의 액세스 권한이 필요한 작업에 대해서는 제한이 있다.그래서 방법은 세가지.

```
1. react native를 사용하고, 직접 네이티브 모듈을 연동한다.(복잡)
2. react native말고 플러터를 사용한다. (간단)
3. 오픈소스 잘 찾아본다.
```



# 0. 오픈소스(java)

https://github.com/danimahardhika/wallpaperboard

> 사실상 우리가 구현하려는 기능은 전부 여기에있음. 이 코드를 잘 분석해서 배경화면이 아니라 잠금화면을 변경하게 하면 됨.
> 사이즈가 크고... 사이즈가 큰게 단점. 라이센스문제도 있다. (하지만 제일 좋음.)

https://github.com/muzei/muzei

> 여기에 있는 오픈소스 가져와서 배경화면 업데이트 부분만 가져올수 있음.

https://developer.android.com/reference/android/app/WallpaperManager

> 그냥 이거 보고  WallpaperManager클래스 사용해서 배경화면 변경할수도 있음. 앱에서 이미지를 선택하고 해당 이미지를 배경화면으로 설정하는 기능을 구현할 수 있음.

미완성
https://github.com/iamgauravn/Wallpaper_Maker



### 오픈소스 분석

https://github.com/danimahardhika/wallpaperboard

![image-20230719170841707](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230719170841707.png)

위의 그대로 세팅을 진행한다.

   

#### 1. 안드로이드 스튜디오의 최신버전 설치

https://ineedtoprogramandweb.tistory.com/entry/AndroidStudio-%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%8A%A4%ED%8A%9C%EB%94%94%EC%98%A4-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0-%EC%B5%9C%EC%8B%A0

> 위에 보고 그대로 따라하자.

   

### 2. Android-SDK Build tools v27을 설치

![image-20230719174347523](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230719174347523.png)

> 오른쪽 체크해서 나오는 것중에 27버전을 선택하고 설치한다.

### 3.API 26 SDK Platform을 설치

![image-20230719175020479](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230719175020479.png)

### 4. 최신 버전의 Android Support Library를 설치

https://developer.android.com/topic/libraries/support-library/setup?hl=ko#add-library

> 위의 링크를 참고한다.

`등등... 일단 이후에 진행`

>  규모 큰거 만들거면 이 오픈소스 쓰는것도 나쁘지 않다고는 생각하는데... 사과 깎으려고 10만원짜리 칼쓰는 느낌.

​     

# 1. 플러터

`장점`: UI같은 부분은 피그마에서 바로 코드 변환해서 99퍼 디자인 구현 가능함.

`단점`: 배워야함.

> 환경설정해서 아래와 같이 예제확인하는데 조금 걸리고

![image-20230720163635073](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230720163635073.png)

> 플러터의 배경화면 변경하는 라이브러리 이용해서 설정하는데 1시간쯤 걸렸음. 화면에 배경화면 변경버튼있고 누르면 이미지에서 사진 빼와서 설정할수있게.
> 동영상하고 gif도 됨.

![image-20230720164015543](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230720164015543.png)



![image-20230720164106152](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230720164106152.png)



![image-20230720164122255](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230720164122255.png)

> 직접 설정해보니 문법은 뭐가 뭔지 정확히는 몰라도 얼추는 이해할수 있고 UI같은 경우는 피그마 99퍼 사용할수 있다고 하니 크게 장벽이 있을것 같진 않음.

