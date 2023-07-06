---
title: Node.js로 간단한 서버구축하기
date: 2023-07-06 16:21:00 +09:00
categories: [study,nodeJS]
tags:
  [
    node, nodejs, server
  ]

---

   

### 시작하기 전에: Node.js 설치 확인

---

Node.js가 이미 컴퓨터에 설치되어 있음을 가정한다. 이를 확인하려면, 터미널 창에 다음 명령어를 입력하면 된다

```
node -v
```

이 명령어를 실행했을 때 버전 정보가 나오면 Node.js가 성공적으로 설치된 것이다.   

### Step 1: 서버 파일 생성

---

Node.js에서 HTTP 서버를 만들기 위해 우선 새로운 JavaScript 파일을 생성해야하는데...  `server.js`로 하자.   

### Step 2: HTTP 모듈 임포트하기

---

Node.js는 'http'라는 이름의 모듈을 기본적으로 제공하며, 이 모듈을 이용하여 HTTP 서버를 쉽게 만들 수 있다. 아래 코드를 `server.js` 파일에 추가한다.

```js
const http = require('http');
```

   

### Step 3: 서버 생성하기

---

`http` 모듈의 `createServer` 메소드를 이용하자. 

이 메소드는 요청이 들어올 때마다 실행되는 콜백 함수를 매개변수로 받습니다. 이 콜백 함수는 다시 두 개의 객체를 매개변수로 받는데, 이들은 각각 요청(request)과 응답(response)을 나타낸다.

```js
const server = http.createServer((req, res) => {
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Hello, World!\n');
});
```

이 서버는 모든 요청에 대해 'Hello, World!'라는 메시지를 응답한다.

   

### Step 4: 서버를 특정 포트에서 수신 대기하기

---

마지막으로, 서버가 어떤 포트에서 수신 대기할 것인지 지정해야 한다. 이를 위해 `listen` 메소드를 사용한다.

```js
const PORT = 3000;

server.listen(PORT, () => {
    console.log(`Server running at http://localhost:${PORT}/`);
});
```

이제 이 서버는 3000번 포트에서 수신 대기한다.

   

### Step 5: 서버 실행하기

---

서버를 실행하기 위해 터미널 창에서 다음 명령어를 입력한다.

```
node server.js
```

그러면 터미널에 'Server running at http://localhost:3000/'라는 메시지가 출력되고, 웹 브라우저를 열고 이 주소를 입력하면 'Hello, World!'라는 메시지를 볼 수 있다.

![image-20230706161947758](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230706161947758.png)

 

:bulb: **url에 따라서 html파일을 다르게 전송해주고싶다면?**

> fileSystem 불러오고, req.url의 값을 저장하여 해당 값이 무엇인가에 따라서 `.createReadStream`을 사용해 html을 넘겨주면 된다.