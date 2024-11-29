---
title: (우테코) 프리코스 Week2 - 🚗 자동차 경주 게임
author: yeji
date: 2020-12-08 00:00:00 +0900
categories: [WoowaCourse]
tags: [woowacourse]
---
* * *
## **🔗 Github 링크**

[cuza22/javascript-racingcar-precourse](https://github.com/cuza22/javascript-racingcar-precourse.git)

1주차는 '함수 분리'에만 집중했다면, 이번에는 '모듈 분리'에 신경을 써 보자.

* * *
## **🎈 모듈이란?**

[모듈 소개](https://ko.javascript.info/modules-intro#ref-2361)

모듈은 프로그램을 구성하는 부품과도 같다고 이해하면 된다. 

쉽게 말해 파일을 깔끔하게 여러 개로 분리하는 것이다. 

저번 과제에서는 나름대로 깔끔해 보이려고 게임의 흐름을 크게 start, end, reset으로 구분했다. 

하지만 모든 내용이 index.js라는 하나의 파일에 들어가있어서 한 눈에 잘 들어오지 않았다.

이번 주에는 각자 다른 기능을 하는 함수랑 string을 파일로 따로 구분해놓으면 좋을 것 같다.

* * *
## **🎈 생각하기**

필요한 기능을 크게 정리해보자. 

- **게임 진행**
    - 1분기의 게임 진행 → 심판 입장
    - 1판의 게임 진행 → 자동차 입장
    - 자동차의 전진 여부 판별
    - 게임 종료
    - 우승자 판별

    - **1분기** : 자동차가 한 칸 움직이는 것

    - **1판** : 게임 시작부터 게임 종료까지

- **입력**
    - 자동차 이름 입력
    - 이동 수 입력
- **출력**
    - 게임 진행 과정 출력
    - 우승자 출력
    - 오류 메세지 출력

모듈 분리 방법에도 ~~국룰~~컨벤션이 있을 것 같아서 주위에 물어보았다. 

게임에서 쪼갤 수 있는 가장 작은 단위까지 쪼개어 나가고, 거기서부터 뭘 붙일지 어떤 기능을 넣어야 할 지 고민하면 된다. Car을 가장 작은 단위로 생각하면 될 것 같다.

먼저 Abstraction을 만들고 더 잘게 쪼갤 수 있을 지 고민한다. 해당 abstraction의 속성 하나를 수정했을 때 다른 abstraction을 수정해야할 상황이 나오면 불필요한 세분화로 판단하고 다시 합친다. 

* * *
## **🔨 모듈 분리**

개개인의 의견이지만 게임을 설계하는 데 도움이 많이 되었다. 

내가 처음에 구분했던 게임의 기능과 주변인의 의견을 참고하여 다음과 같이 모듈을 분리하기로 하였다. 

```
📁 docs
└ README.md

📁 src
├ index.js
├ car.js # 자동차의 기능
├ utils.js # 게임 진행에 필요한 요소
├ input.js # 입력
├ output.js # 출력
└ constants.js # 하드코딩이 필요한 요소 정리

📄 index.html
📄 package.json # eslint 세팅
```

* * *
## **📌 함수 목록**

이에 맞춰 필요한 함수는 README.md에도 정리하였다.

- **index.js**
    - `RacingCarGame` - 1판의 게임 생성
        - `nowCount` - 현재 분기를 나타내는 속성
        - `totalCount` - 1판이 끝날 때까지의 분기 갯수
        - `carList` - 게임 진행 중인 Car 객체 리스트
        - `winnerList` - 우승자 Car 객체 리스트
- **utils.js**
    - `startGame` - RacingCarGame 생성자. nowCount 설정
    - `playGame` - 한 분기의 게임. nowCount 증가 & 각 자동차의 move 속성 변경.
    - `endGame` - getWinner을 호출하고 printResult을 호출한다.
    - `setTotalCount` - RacingCarGame에 totalCount(분기) 설정
    - `setCarList` - RacingCarGame의 속성으로 추가.
    - `setWinnerList` - RacingCarGame의 속성으로 추가.
    - `increaseCount` - gameBoard의 nowCount 1 증가.
    - `isGameEnd` - 1판의 게임이 끝났는지 판별. 입력받은 분기만큼의 실행이 끝났을 때 true 리턴.
    - `getWinner` - car들의 move속성을 비교하여 승자를 리스트로 리턴한다.
- **car.js**
    - `Car` - Car 객체 생성자. Car의 name값 설정, move는 0을 초기값으로 설정
    - `randomNumberCreator` - 0, 9사이의 random값 생성
    - `isMoved` - Car의 전진 여부. 숫자를 입력받아 4이상일 경우 true, 3이하면 false
    - `moveCar` - isMoved의 결과에 따라 Car객체의 move값 변화
    - `getCarMove` - Car객체의 move값 리턴
- **input.js**
    - `carNamesInput` - 입력받은 이름을 쉼표(,)로 구분하여 리스트로 리턴
    - `isCarNameValid` - 이름이 하나라도 5자를 넘어갈 경우 alert 후 false 리턴 + 빈칸, 중복된 이름도 추가로 제외함.
    - `countNumberOfCars` - 게임에 참가하는 자동차 수 리턴
    - `createCars` - 입력받은 car **이름** 리스트로 car **객체** 리스트 생성하여 리턴
    - `carNamesButtonEvents` - car-names-submit 버튼 연결 함수. carList와 관련된 함수를 연달아 호출한다.
    - `racingCountButtonEvents` - racing-count-submit 버튼 연결 함수.
- **output.js**
    - `carStatus` - Car객체의 move를 입력받아 자동차별로 결과 메세지 리턴
    - `printStatusMessage` - carStatus의 결과를 합쳐서 전체 게임 상황 메세지 리턴
    - `printResultMessage` - 승자 목록을 리스트로 받아서 출력한다.

* * *
## **🎯 기능 요구사항**

-  주어진 횟수 동안 n대의 자동차는 전진 또는 멈출 수 있다.
-  자동차에 이름을 부여할 수 있다. 전진하는 자동차를 출력할 때 자동차 이름을 같이 출력한다.
-  자동차 이름은 쉼표(,)를 기준으로 구분하며 이름은 5자 이하만 가능하다.'
    -  빈 칸이나 중복된 이름도 불가능하다.
-  사용자는 몇 번의 이동을 할 것인지를 입력할 수 있어야 한다.
-  전진하는 조건은 0에서 9 사이에서 random 값을 구한 후 random 값이 4 이상일 경우 전진하고, 3 이하의 값이면 멈춘다.
-  자동차 경주 게임을 완료한 후 누가 우승했는지를 알려준다. 우승자는 한 명 이상일 수 있다.
-  우승자가 여러명일 경우 ,를 이용하여 구분한다.


* * *
## **🎈 느낀점**

- 함수 목록을 먼저 작성하고 하나씩 구현해나갔다. README에 필요한 함수와 기능을 모두 정리해두고, 함수를 그대로 하나씩 구현해 준 후에 오류를 고쳐나갔다. 설계에 시간을 엄청 썼으나 머리가 덜 복잡했고 시간도 훨씬 덜 소모되었다.
- 설계대로 코딩하는 것은 맛을 보지 않고 요리하는 장금이가 된 기분이었다... 아직 장금이의 수준에는 못 다다랐는지 처음 계획한 모듈과 조금 다르게 완성되었다. 다음엔 더욱 완벽하게 설계해서 빠르게 미션을 끝내보고 싶다.
- 1주차와 마찬가지로 코드의 확장성을 고려하였고 메세지 등의 수정이 쉽도록 작성하였다.
- 처음에는 찰흙을 뭉쳐서 겨우 모양새만 갖췄다면, 함수와 모듈을 분리해서 코딩하다보니 레고블록으로 각 부위를 완성해서 마지막에 하나로 합치는 방법으로 코딩하는 기분이 든다.
- 1주차 미션에서 헤맸던 부분을 쉽게 해결할 수 있게 되었다. 버튼을 눌렀을 때 객체의 속성을 변경하는 것이 scope 문제 때문에 너무 어려웠는데, this를 인자로 넘기니까 깔끔히 해결되었다.
- for문의 새로운 용법(?)을 알아내었다.

    ```jsx
    // JavaScript
    for (let i of arr) {
    	 ... }
    ```

    ```python
    # Python
    for i in arr : 
        ...
    ```

    파이썬의 해당 문법처럼 자바스크립트에서도 for 문이 사용 가능하다.
