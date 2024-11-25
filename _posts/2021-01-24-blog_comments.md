---
title: 블로그 뜯어고치기 [2] - utterances로 댓글 기능 추가하기
author: yeji
date: 2021-01-24 06:39:37 +0900
categories: [Blog]
tags: [blog]
---
* * *
이 블로그 테마는 아주 마음에 안 드는 점이 많다. 일단 댓글 기능이 없다. 

댓글 기능이 없는 건 말이 안 된다고 생각한다...

그래서 하나 가져와서 달았다.

## DISQUS? utterances?
지킬 블로그에 댓글 기능을 다는 방법은 크게 두 가지가 있다. 하나는 DISQUS이고 다른 하나는 utterances이다. 

대부분 DISQUS를 쓰는 것 같은데 나는 이 방법을 별로 쓰고 싶지 않았다. 

그 이유는...
* 생긴게 맘에 안 든다. (누르면 광고 엄청 튀어나올 것 같음)
* 댓글을 달기 위해 facebook이나 twitter로 로그인을 해야 한다. 혹은 DISQUS에 회원가입을 해야 한다. 
* 회원가입이나 다른 플랫폼을 이용한 로그인이 싫다면 'name', 'email', 'password'를 입력해야 한다. 조악한 제로보드를 떠오르게 한다.

좀 더 깔끔한 기능을 찾다가 발견한 것이 utterances이다. 

내가 느낀 장점은
* github 계정을 이용하므로 추가적인 회원가입이 필요 없다.(가장 중요) 로그인도 버튼 하나만 누르면 된다!
* 깔~끔하게 생겼다. 심지어 아이콘까지 귀엽다. 
* markdown 문법이 사용 가능하다. 

그래서 utterances를 이용하기로 결정했다. 

## 설치 방법
설치도 매우 쉽다. 
1. blog-comments라는 repository를 생성한다. 
이 repository의 Issues에서 댓글을 한꺼번에 관리하게 된다. 
![image](https://user-images.githubusercontent.com/66822201/105615136-960fb980-5e11-11eb-8431-481ac8d3231d.png)

2. https://utteranc.es/에 접속한다. 
![image](https://user-images.githubusercontent.com/66822201/105615103-58ab2c00-5e11-11eb-9007-65b81094cf91.png)

1. Repository에 방금 만든 repository의 이름을 넣고, 
![image](https://user-images.githubusercontent.com/66822201/105615160-d2dbb080-5e11-11eb-9cae-7746edcda738.png)

2. Blog Post ⇔ Issue Mapping에서 원하는 방식을 선택한다. 

    utterances는 github issue를 각 포스트와 연결해 댓글처럼 보여주는 것이므로(맞나?), issue에 댓글이 관리될 방식을 선택하면 된다. 

    나는 Issue의 제목에 page title을 집어넣는 방식을 택했다. 
    ![image](https://user-images.githubusercontent.com/66822201/105615182-fc94d780-5e11-11eb-839c-6c2cb5ce1d64.png)


3. Issue Label을 설정한다. 

    optional 사항이므로 빈 칸으로 남겨두어도 된다. 
    ![image](https://user-images.githubusercontent.com/66822201/105615187-0cacb700-5e12-11eb-8722-806bb80cba1e.png)


4. Theme을 선택한다. 블로그의 디자인에 어울리는 테마를 선택하자. 
    ![image](https://user-images.githubusercontent.com/66822201/105615191-133b2e80-5e12-11eb-9afb-1deb203c1808.png)


5. Enable Utterances의 코드를 복사한다!

    지금까지 선택한 설정에 맞춰 코드가 생성된 것이다. 
    ![image](https://user-images.githubusercontent.com/66822201/105615199-1c2c0000-5e12-11eb-9fdb-68705ecb9c38.png)


6. post.html의 footer에 해당 코드를 붙여넣는다. 

    나는 좀 더 깔끔하게 하기 위해서 comments.html을 만들고 include comments.html 로 댓글 기능을 추가했다. 

그럼 이제 모든 포스트에 댓글 기능이 추가되었다.
![image](https://user-images.githubusercontent.com/66822201/105615221-41b90980-5e12-11eb-90e7-01d650fa0f26.png)
(너무 이쁘잖아 ㅠㅠㅠ)

업그레이드된 블로그를 보니 정말 뿌듯하다 후후후후후 

좋은 주인이 되어줄게 블로그야 

끝