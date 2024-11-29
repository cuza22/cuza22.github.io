---
title: 블로그 뜯어고치기 [1] - mathjax로 수식 사용하기
author: yeji
date: 2021-01-24 05:39:59 +0900
categories: [Blog]
tags: [blog]
math: true
---
* * *
최대한 심플해보이는 테마를 적용시켰더니 블로그에 기능이 없어도 너무 없다. 

블로그를 만들면서 가장 먼저 담고 싶었던 내용은, 아무래도 내가 통계를 공부중이다 보니 관련된 내용을 정리해두면 좋겠다는 생각을 했다. 

복잡한 수식을 표현할 수 있는 기능이 반드시 필요했기 때문에 MathJax를 사용하게 되었다. 

## 사용 방법
1. _includes 폴더에 mathjax.html이라는 파일을 만들고 다음 내용을 입력한다.
    ```html
    <script type="text/javascript" async
    src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
    </script>
    ```
    cdn.mathjax.org는 한참 전에 지원이 끝났기 때문에 위의 주소를 사용해야 한다.
    
    그 아래에 바로 이어서 다음 내용을 추가한다. '$'나 '\\\\(' ')\\\\'로 감쌌을 때 수식으로 변환하겠다는 뜻이다. 
    ```html
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}});
    </script>
    ```


2. head.html파일에 다음과 같은 코드를 추가한다. 
    ```html
    <head>
    ...
        {% if page.use_math %}
            {% include mathjax.html %}
        {% endif %}
    ...
    </head>
    ```
    포스트에 use_math가 true일 때만 mathjax.html을 불러오게 된다. 

    이 글을 예시로 들자면 이런 식으로 mathjax를 포스트에 불러올 수 있다. 
    ```html
    ---
    layout: post
    title: 블로그 뜯어고치기 [1] -  mathjax로 수식 사용하기
    category: etc
    tags: [blog]
    use_math: true ## <- 여기~~!
    ---
    ```

3. 사용해보기

    $1+1=2$
    ```html
    $1+1=2$
    ```
    \\(1+1=2\\)
    ```html
    \\(1+1=2\\)
    ```
    \\[1+1=2\\]  (얘는 왜 가운데맞춤인거지..?)
    ```html
    \\[1+1=2\\]
    ```

    셋 중 편한 방법으로 수식을 쓰자!!


## 여담
더 찾아보니 MathJax보다는 KaTeX가 표현할 수 있는 수식은 적어도 훨씬 빠르다고 한다. 이후에 KaTeX로 바꿀 수도 있겠다. 

끗