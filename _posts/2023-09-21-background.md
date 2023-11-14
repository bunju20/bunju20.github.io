---
title: [flutter]백그라운드에서도 앱 실행하게 하기
date: 2023-09-11 10:40:00 +09:00
categories: [front,flutter]
tags:
  [
    front,flutter, 백그라운드, 핸드폰꺼도,background
  ]

---

# 앱을 끄고있어도 특정시간 되면  백엔드로 api보내게 만들rl

`workmanager` **: 앱이 꺼져있을때 and 백그라운드 상태일때 모두 작동할수있게하는애.**

https://pub.dev/packages/workmanager

## **5분 지나면 백그라운드 상태일때  api응답을 확인한다.**

**api응답**은 다음과 같은 사이트 이용.  여기에 해당하는 url 찾아서 글로 겟하든 포스트하든 하면 얘네가 알아서 준비되어있는거 주던지 받아주던지 합니다. statecode는 200기준.

https://jsonplaceholder.typicode.com/



이 아래에 있는 Worker result SUCCESS for Work라는게, work request가 스케줄 되고 성공적으로 실행됨을 나타내는 로그 문장입니다. WorkManager 라이브러리에서 표시되는 로그이므로 로그 메시지를 변경할수는 없다고 하네요. 

→ 그니까 일단 백그라운드에서  어떤걸 진행했다. 라고 볼수있는건데

![image-20231114141919011](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20231114141919011.png)

→ 왜 안되지? [아 나머지는 백그라운드면서 callApi가 백그라운드가 아니었음.]

![image-20231114141942348](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20231114141942348.png)

15분 단위로 잘 오긴하는데 여전히 백그라운드 작업만 완료했다고 볼수있습니다. 

![image-20231114142014923](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20231114142014923.png)

위에 보시면 제가 todos로 get요청을 보냈고

![image-20231114142030618](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20231114142030618.png)

![image-20231114142040016](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20231114142040016.png)



# 아침 8시가 되면 `OR` 버튼을 누르면 API보내게 만들기

- 한 2~3시간 간격으로 현재 시간 알아보고, 지금 시간이 대략 5시이상 8시 이하면 api 요청 보내게 하기 `딜레이가 클것같진 않긴함` → 일단 이방법으로 진행은하겠음.
- 아침 8시기준꺼 api받아오고, 현재 시간을 기준으로 몇시간 뒤에 api보내야할지 정해놓고, 그다음부턴 24시간 간격으로 api보내기 `이건 애매한게 잘못하면 저 24시간이 밀릴수도 있을것같음.가령 핸드폰을 완전히 전원을 끈상태였다거나 하면 배경화면이 저녁에 바뀌는 불상사가 생길수도 있다는 점 -> 사실 핸드폰을 키면~~ 과 같은 변수 핸들링을 하면 되는데 그건 너무 노력대비 얻는게 없음.`

## TEST

>  💡 **[핸드폰은 화면 꺼놓는다.]** 
>
> **현재시각 2:42분**
>
> **15분 간격**으로 api를 보낼거고
>
> **3:00~3:40 사이일때만** API 요청보내기.



1. **2시 58분엔 요청이 안간거 확인** ✅ `설정한대로 아래 글씨 뜬다`

보는것처럼 아직 아까 온요청말고 늘어난 요청이 없다.

![image-20231114142134351](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20231114142134351.png)

2. **3시 13분엔 요청이 간거 확인✅**

![image-20231114142154682](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20231114142154682.png)

위와같이 요청이 제대로 들어온걸 확인할수 있습니다. 야호.

해당부분은 독립적으로 help.dart(…)에 저장해 놨습니다. 이부분은 나중에 main에 추가하도록 하겠습니다. 키기만해도 그냥 작동하게 만들어놔야할것같아요.



# 주의사항 → 나중에 생길 수 있는 이슈

1. 앱이 배터리 최적화의 영향을 받지 않도록 설정해야 함.
2. 일부 앱은 백그라운드에서 실행될 때 시스템에 의해 제한될 수 있음. 이는 특히 배경 데이터 사용이 제한되는 경우에 문제가 될 수 있음. 따라서 사용자에게 앱 설정을 확인하도록 안내할 필요가 있다.
3. 안드로이드 API 레벨 23 이상에서는 장치가 도즈 모드에 있을 때 알람이 정확한 시간에 발생하지 않을 수 있다. 이는 배터리를 절약하기 위해 시스템에서 일부 기능이 비활성화되기 때문.