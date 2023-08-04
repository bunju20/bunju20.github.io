---
title: 자바스크립트 애니메이션을 동영상으로 만들어 전송하기
date: 2023-08-01 15:10:00 +09:00
categories: [toy,bossle]
tags:
  [
    js, javascript, mp4, 동영상, 애니메이션,CCapture.js,CCapture
  ]
---

> 자바스크립트로 만들어져있는 애니메이션들이 있는데, 이걸 동영상으로 만들고 백엔드한테 보낼것이다.
>
> 앱내에서의 배경화면은 변경할수 있는데, 안드로이드에서 배경화면을 변경하려면 mp4파일만 되기때문.

   [GitHub - ptluaan/-raindrop_effect: Raindrop effect](https://github.com/ptluaan/-raindrop_effect) 

만드는데사용되는 소스는 위와 같다.

   



# JavaScript 애니메이션을 MP4로

### 0. 웹서버를 만들어둔다.

![rain](https://raw.githubusercontent.com/bunju20/image_server/main/img_/rain-1690874865460-3.gif)

위와같은 애니메이션이 나오게 한다. 그럼 이제 이걸 비디오로 바꿔보자.

   

### 1. mp4로 변환

`Puppeteer`  : Chrome을 Headless 모드로 실행할 수 있는 Node.js 라이브러리. 먼저 테스트 코드부터 잘 작동하는지 확인한다.

```js
const puppeteer = require('puppeteer');
const fs = require('fs');
const { execSync } = require('child_process');

(async () => {
    const browser = await puppeteer.launch();
    const page = await browser.newPage();
    await page.goto('http://localhost:8000'); // 웹페이지 URL

    // 화면 녹화 시작
    await page.tracing.start({ path: 'trace.json', screenshots: true });

    // 5초 대기
    await new Promise(resolve => setTimeout(resolve, 5000));

    // 화면 녹화 종료
    await page.tracing.stop();

    await browser.close();

    // JSON 트레이스를 MP4로 변환
    execSync('chrome-trace-events-to-video trace.json > output.mp4');

    // 불필요한 파일 삭제
    fs.unlinkSync('trace.json');
})();

```

이렇게 간단하게 할수 있지만...

![images](https://raw.githubusercontent.com/bunju20/image_server/main/img_/images-1691116659932-1.jpeg)

> ... 왜이렇게 비효율적인것 같지?
>
> 기본적으로 웹을 캡쳐하는거라서 아래와 같은 버튼을 누르는 액션을 하지 않고는 녹화를 해놓을수 없게 만들어져있다.

![image-20230804113832166](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230804113832166.png)



   

 저건 안되겠으니 `Whammy.js` 라는 JavaScript 라이브러리를 사용한다.

### **1단계: Whammy.js 포함하기**

먼저 HTML 파일에 Whammy.js 라이브러리를 포함시켜야 합니다. Whammy.js 라이브러리를 다운로드 받아서 프로젝트의 적절한 위치에 저장하고, 해당 위치를 기준으로 script 태그를 통해 불러온다.

```html

<script src="node_modules/whammy/whammy.js"></script>
```

> npm i whammy한 뒤에 내 path는 저랬다.

   

### **2단계: 캔버스 요소 그리기**

프레임을 그릴 캔버스 요소를 선언한다. 이것은 이미되어있으니 패스. `대략 이렇게 생긴게 있으면 된다`

```html
<canvas id="Canvas" width="500" height="500"></canvas>
```

   

### **3단계: Whammy 객체 생성 및 프레임 추가**

다음으로 JavaScript 파일에 Whammy Video 객체를 생성하고, 그리고자 하는 각 프레임에 대해 캔버스를 그리고 그것을 Whammy Video 객체에 추가해야 한다.

```js
// 캔버스와 그래픽 컨텍스트에 대한 참조를 가져옵니다.
var canvas = document.getElementsByTagName("canvas")[0];

// Whammy Video 객체를 생성합니다.
var video = new Whammy.Video(15); // 15는 FPS (frames per second)입니다.

// 주어진 시간 동안(예: 10초), 일정 간격으로(예: 100밀리초) 캔버스를 캡처합니다.
var duration = 10; // 10초
var interval = 100; // 100밀리초 간격

var captureFrames = setInterval(function() {
    // 캔버스를 이미지 데이터로 변환합니다.
    var dataURL = canvas.toDataURL('image/webp');

    // 이미지 데이터를 Whammy Video 객체에 추가합니다.
    video.add(dataURL);
}, interval);

// 지정된 시간이 경과한 후에 캡처를 중지하고 비디오를 컴파일합니다.
setTimeout(function() {
    clearInterval(captureFrames);

    // 동영상 데이터를 생성합니다.
    var output = video.compile();

    // 생성된 동영상 데이터를 이용해 다운로드 링크를 만듭니다.
    var url = URL.createObjectURL(output);
    var link = document.createElement('a');
    link.href = url;
    link.download = 'output.webm';
    link.click();

}, duration * 1000); // duration을 밀리초로 변환합니다.

```

   

이런 식으로, 각각의 프레임을 그리고 저장하고, 그 이미지들을 합쳐 동영상을 만드는 과정을 구현할 수 있다. 

