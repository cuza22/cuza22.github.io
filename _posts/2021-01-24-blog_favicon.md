---
title: 블로그 뜯어고치기 [3] - favicon 추가하기
author: yeji
date: 2021-01-24 07:49:35 +0900
categories: [Blog]
tags: [blog]
---
* * *
이번엔 favicon을 추가해보았다. 

## favicon이란?
위키백과의 설명에 따르면 
> "인터넷 웹 브라우저의 주소창에 표시되는 웹사이트나 웹페이지를 대표하는 아이콘"

이라는데 이런 설명보다는 이미지로 보면 바로 이해된다. 

![image](https://user-images.githubusercontent.com/66822201/105615629-95792200-5e15-11eb-8365-fea596ba0909.png)

이렇게 탭에 뜨는 귀여운 아이콘이다. 

기본 아이콘보다는 알록달록한 아이콘을 쓰는 것이 좀 더 아기자기하지 않을까?? 하는 생각에 다른 기능은 제쳐두고 파비콘부터 추가하기로 했다. 

## favicon은 이미지 파일을 사용해야 한다. 
윈도우키 + ';' 를 누르면 나오는 아이콘을 그대로 파비콘으로 사용하는 것은 불가능하다. 

이미지 파일을 따로 업로드해주어야한다. 

## favicon 적용 방법
1. 베이스가 되는 이미지 파일을 준비한다. 

    나는 구글에서 'orange icon'을 검색해서 나온 결과 중 마음에 드는 png파일을 골랐다.

2. [favicon-generator](https://www.favicon-generator.org/) 사이트에 접속한다. 

3. 원하는 이미지를 업로드하고 'Create Favicon'을 누르면
    ![image](https://user-images.githubusercontent.com/66822201/105616016-171d7f80-5e17-11eb-846c-eeda13510e88.png)

4. 알아서 웹, 모바일에 맞게 이미지 리사이징을 해주고 코드까지 만들어준다. 'Download the generated favicon'을 누르자. 
    ![image](https://user-images.githubusercontent.com/66822201/105616011-05d47300-5e17-11eb-9901-237753573ac2.png)

    세상이 이렇게 발달했다... 넘 편하군 

5. zip파일을 압축해제한 후 `/assets/img/favicon/` 에 업로드해준다. 
    
    assets/img/ 내부에 'favicon'이라는 폴더는 직접 만들어야 한다!

6. 4번에서 만들어진 소스코드의 경로를 수정한다. 

    Before:

    `<link ... href="/favion-32x32.png">`

    After:

    `<link ... href="/assets/img/favicon/favicon-32x32.png>`

7. head.html 파일에 해당 소스코드를 추가한다. 

8. commit후 push하면 끝!!

모바일이나 컴퓨터에서 귀여운 아이콘이 잘 보인다.

모두 파비콘을 이용해서 자신의 블로그를 더 귀엽게 만들어보자. 

끗끗