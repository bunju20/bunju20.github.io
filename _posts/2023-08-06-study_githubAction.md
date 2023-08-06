---
title: 깃허브 액션 사용해보기
date: 2023-08-06 14:40:00 +09:00
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





> 참고
>
> https://docs.github.com/ko/actions/using-github-hosted-runners/about-github-hosted-runners

