---
title: 깃허브 액션 사용해보기
date: 2023-08-07 14:40:00 +09:00
categories: [study,developer]
tags:
  [
    github,action,study,자동화
  ]


---



## 깃허브 액션의 5가지 Actions

* **Events `어떤일이 발생했는지`**

> 깃허브에서 일어날수 있는 일들을 event로 지정할수 있다.
>
> main 브랜치로 머지할때나, 커밋을 푸쉬할때나, 이슈를 누가 열거나 했을때

   

* **Workflows `위같은 일이 발생했을때 내가 뭘하고싶나?`**

> 자동화 하고싶은 내용들이 이 워크플로우 안에 들어가 있다.

   

* **Jobs `workflow에 있는 것`**

> unit test를 하는 job, E2E test를 하는 job 등등 하나의 워크플로우에 여러개의 job이 있을수 있다.

![image-20230806191637850](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230806191637850.png)

* **Actions**

> 이미 잘 만들어진 공개적인 액션들.  깃허브에서 제공해준다.

   

* **Runners `job을 실행하는 것`**

   

## 실제로 사용해보자!

프로젝트 경로 안에 `workflows`라는 폴더를 만들고, 그 안에 `workflow.yml` (이름은 마음대로!)라는 파일을 만든다. 나는 만들고있던 심플한 프로젝트를 가져오겠다.

![image-20230806223637101](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230806223637101.png)

본인 레포지토리의 `action`란에 들어가면 위와같은 화면이 나온다. 위에서 보면 여러 템플릿이 있는데
![image-20230806224520629](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230806224520629.png)

난 이걸 써보도록 하겠다. 저 위에 있는 버튼 `configure`을 누르면 아래와 같은 화면이 나온다.

![image-20230806224633314](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230806224633314.png)

왼쪽에 써있는 코드는기본적인 템플릿.

오른쪽에서는 다양한 액션들을 확인할수 있고, Documentation 탭에서는 기본적인 문서를 확인가능하다. 나는 따로 건드린게 없는데 하고싶은게 있다면 찾아서 위의 코드에 적용하면 된다.

![image-20230807162626829](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230807162626829.png)

저걸 올리고 나니 핸드폰으로 알림이 온다. 

![image-20230807162741142](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230807162741142.png)

무언가 문제가 생긴듯 하다!

![image-20230807162945820](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230807162945820.png)

이부분에서 다른 버전에서도 해당 코드가 작동하는지 확인하고 싶어한것 같은데, 나는 이부분은 필요없으므로 지운다.

![image-20230807175052471](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230807175052471.png)

이런 모양이나오면 성공한것이다. 만약 테스트에 맞지 않게 원래 파일을 일부로 틀리게 만들면 빨간불이 뜬다.

마찬가지로 pull리퀘스트를 할때 `나 merge할래!`  틀린 브랜치로 보내면 다음과 같이 자동으로 워크플로우를 보여준다.

![image-20230807175437909](https://raw.githubusercontent.com/bunju20/image_server/main/img_/image-20230807175437909.png)

   

   



> 참고
>
> https://docs.github.com/ko/actions/using-github-hosted-runners/about-github-hosted-runners

