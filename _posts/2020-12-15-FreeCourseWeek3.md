---
title: (우테코) 프리코스 Week3 - 🚇 지하철 노선도 미션
author: yeji
date: 2020-12-15 00:00:00 +0900
categories: [WoowaCourse]
tags: [woowacourse]
---
* * *

## **🔗 Github 링크**

[cuza22/javascript-subway-map-precourse](https://github.com/cuza22/javascript-subway-map-precourse)

1, 2주차에 비해 많이 어렵게 느껴진다. 추가된 요구사항인 'data속성'과 'localStorage'를 먼저 알아보자.

* * *
## **🎈 생각하기**

### 🎈 data속성이란?

[데이터 속성 사용하기](https://developer.mozilla.org/ko/docs/Learn/HTML/Howto/%EB%8D%B0%EC%9D%B4%ED%84%B0_%EC%86%8D%EC%84%B1_%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)

HTML태그에서 'data-'로 시작하는 속성이다. 임의로 속성을 만들어서 특정한 데이터를 저장하고 싶을 때 사용 가능하다. 

3주차 과제에서는 각 역에는 '노선'과 '순서'에 해당하는 속성을  저장하면 좋을 것 같다. 

### 🎈 localStorage란?

[Window.localStorage](https://developer.mozilla.org/ko/docs/Web/API/Window/localStorage)

'새로고침하더라도 가장 최근에 작업한 정보들을 불러올 수 있도록' 하는 기능인 것 같다. 

그래서 이번 과제의 'index.js'에서는 1, 2주차 과제와 달리 new로 객체를 생성하지 않는 것 같다. (new로 게임을 진행하는 경우 새로고침 했을 때 새 객체가 생성되어서 지금까지의 진행상황이 날아가니까!)

사용자가 수정하게 되는 '역에 관한 정보'를 localSotrage에 저장하고, 해당 값을 불러와서 페이지가 작동하게 하면 될 것 같다. 

(벌써 너무 복잡하다... @_@)

### 🎈 정리

요구하는 기능을 크게 정리해보았다.

 0. **메뉴 관리** - 4개의 버튼을 띄우고, 각 버튼을 누를 때마다 필요한 화면을 아래에 띄운다.

1. **역 관리**  - 존재하는 모든 역을 출력한다. 
2. **노선 관리** - 1, 2, 3호선 등 호선을 종점역과 함께 출력한다. (각 노선의 중간 역은 상관없다)
3. **구간 관리** - 각 노선의 중간 역을 출력하고 관리 가능하다. 
4. **지하철 노선도 출력** - 존재하는 노선을 구간과 함께 출력한다.

- database가 있어야 할 것 같았다. '역 관리'에 필요한 **station목록**, '노선 관리, 구간 관리'에 필요한 **line 목록**으로 두 개가 필요하다. 이것을 localStorage에 저장해주면 될 것 같다. → 이러면 문제가 한 역이 여러 호선에 포함될 때 데이터가 중복된다.
- 메뉴별 화면을 어떻게 구성해야할 지 정말! 많이! 고민했는데... index.html에 모두 저장해두고 각각 id를 다르게 해서 버튼을 누를 때마다 visibility를 다르게 할 것이다.
- select 목록에 존재하는 역 이름을 'data속성'으로 지정하자

* * *
## **🔨 모듈 분리**

```
📁 docs
└ README.md

📁 src
├ 📁 ui
│	├ init-ui.js
│	├ station-ui.js
│	├ line-ui.js
│ ├ 📁 section
│	│	├ section-selection-ui.js
│	│	├ section-management-ui.js
│	│	└ section-management-table-ui.js
│	└ map-ui.js
│
├ 📁 util
│	├ station.js
│	├ line.js
│	├ section.js
│	└ storageAccess.js
│
├ index.js
└ constants.js

📄 index.html
```

- 웹에 표시되는 'ui'와 관련된 파일과 작동과 관련된 'util' 파일을 분리하였다.
- 예를 들어 '역 목록'에서 역을 하나 삭제한다고 할 때 화면에 보이는 표에서 행이 하나 사라지는 것은 'ui'로, localStorage에서 해당 역이 사라지는 것은 'util'로 배치하였다.
- 따라서 유효성을 검사하는 함수는 util에 있다.
- localStorage를 DB라고 생각하고, DB에 접근하기 위한 함수를 starageAccess.js에 따로 모아두었다.
- 저번주와 마찬가지로 이후에 변동 가능하거나 상수 취급이 가능한 요소는 모두 'constatns.js'에 정리하였다.

* * *
## **🚀 기능 요구사항**

⭐**: 예외사항** 

### 🧩 메뉴 관련 기능

-  메뉴 버튼을 누르면 해당 페이지가 로드된다.

### 🧩 지하철 역 관련 기능

-  지하철 역을 등록하고 삭제할 수 있다.
-  (단, 노선에 등록된 역은 삭제할 수 없다) ⭐
-  중복된 지하철 역 이름이 등록될 수 없다. ⭐
-  지하철 역은 2글자 이상이어야 한다.⭐
-  지하철 역의 목록을 조회할 수 있다.

### 🧩 지하철 노선 관련 기능

-  지하철 노선을 등록하고 삭제할 수 있다.
-  중복된 지하철 노선 이름이 등록될 수 없다. ⭐
-  노선 등록 시 상행 종점역과 하행 종점역을 입력받는다.
-  지하철 노선의 목록을 조회할 수 있다.

### 🧩 지하철 구간 추가 기능

- 지하철 노선에 구간을 추가하는 기능은 노선에 역을 추가하는 기능이라고도 할 수 있다.
    - 역과 역사이를 구간이라 하고 이 구간들의 모음이 노선이다.
-  하나의 역은 여러개의 노선에 추가될 수 있다.
-  역과 역 사이에 새로운 역이 추가 될 수 있다.
-  노선에서 갈래길은 생길 수 없다. ⭐
-  추가하려는 역의 index가 out of range가 아니다. ⭐

### 🧩 지하철 구간 삭제 기능

-  노선에 등록된 역을 제거할 수 있다.
-  종점을 제거할 경우 다음 역이 종점이 된다.
-  노선에 포함된 역이 두개 이하일 때는 역을 제거할 수 없다. ⭐

### 🧩 지하철 노선에 등록된 역 조회 기능

-  노선의 상행 종점부터 하행 종점까지 연결된 순서대로 역 목록을 조회할 수 있다.

* * *
## **✅ 프로그래밍 요구사항**

### 🌱 **메뉴 버튼**

-  역 관리 button 태그는 `#station-manager-button` id값을 가진다.
-  노선 관리 button 태그는 `#line-manager-button` id값을 가진다.
-  구간 관리 button 태그는 `#section-manager-button` id값을 가진다.
-  지하철 노선도 출력 관리 button 태그는 `#map-print-manager-button` id값을 가진다.

### 🌱 **지하철 역 관련 기능**

-  지하철 역을 입력하는 input 태그는 `#station-name-input` id값을 가진다.
-  지하철 역을 추가하는 button 태그는 `#station-add-button` id값을 가진다.
-  지하철 역을 삭제하는 button 태그는 `.station-delete-button` class값을 가진다.
-  지하철 역 목록 Array를 localStorage에 저장하고 이름은 `stationList` 로 한다.

### 🌱 **지하철 노선 관련 기능**

-  지하철 노선의 이름을 입력하는 input 태그는 `#line-name-input` id값을 가진다.
-  지하철 노선의 상행 종점을 선택하는 select 태그는 `#line-start-station-selector` id값을 가진다.
-  지하철 노선의 하행 종점을 선택하는 select 태그는 `#line-end-station-selector` id값을 가진다.
-  지하철 노선을 추가하는 button 태그는 `#line-add-button` id값을 가진다.
-  지하철 노선을 삭제하는 button 태그는 `.line-delete-button` class값을 가진다.
-  지하철 노선 목록 Array를 localStorage에 저장하고 이름은 `lineList`로 한다.

### 🌱 **지하철 구간 추가 기능**

-  지하철 노선을 선택하는 button 태그는 `.section-line-menu-button` class값을 가진다.
-  지하철 구간을 설정할 역 select 태그는 `#section-station-selector` id값을 가진다.
-  지하철 구간의 순서를 입력하는 input 태그는 `#section-order-input` id값을 가진다.
-  지하철 구간을 등록하는 button 태그는 `#section-add-button` id값을 가진다.
-  지하철 구간을 제거하는 button 태그는 `.section-delete-button` class값을 가진다.

* * *
### 🌱 **지하철 노선도 출력 기능**

-  지하철 노선도 출력 버튼을 누르면 `<div class="map"></div>` 태그를 만들고 해당 태그 내부에 노선도를 출력한다.

* * *
## **📌 함수 목록**

- **ui**
    - **station-ui.js**
        - resetStationTable - data에 맞춰 역 목록 재설정
        - addStationTableRow - 역 목록 행 추가
        - createStationDeleteButton - 역 목록 삭제 버튼 생성
        - deleteStationTableRow - 역 목록 행 삭제
    - **line-ui.js**
        - resetLineTable - data에 맞춰 노선 목록 재설정
        - resetStartOption - data에 맞춰 '상행종점'의 역 목록 재설정
        - resetEndOption - data에 맞춰 '하행종점'의 역 목록 재설정
        - addLineTableRow - 노선 목록 행 추가
        - deleteLineTableRow - 노선 목록 행 삭제
        - createLineDeleteButton - 노선 목록 삭제 버튼 생성
    - **section-selection-ui.js**
        - resetLineButtons - data에 맞춰 노선 버튼 재설정 + 초기화
        - addLineButtons - data에 맞춰 노선 버튼 재설정
        - createLineButton - 노선 버튼 생성
    - **section-management-ui.js**
        - openLineManagement - 'xx노선 관리' 창 열기
        - resetAddButtonLine - 등록 버튼이 가리키는 노선 재설정
        - resetStationOption - data에 맞춰 '구간등록'의 역 목록 재설정
    - **section-management-table-ui.js**
        - resetSectionTable - 'xx노선'에 해당하는 data에 맞춰 구간 목록 재설정
        - addSectionTableRow - 'xx노선' 구간 목록 행 추가
        - deleteSectionTableRow - 'xx노선' 구간 목록 행 삭제
        - createSectionDeleteButton - 'xx노선' 구간 목록 행 삭제 버튼 생성
        - resetTableIndexColumn - 'xx노선' 구간 목록 인덱스 재설정
    - **map-ui.js**
        - createMap - 지하철 노선도 추가
        - createLineTitle - 지하철 노선 제목 생성
        - createLineList - 지하철 노선 목록 생성
- **util**
    - **storageAccess.js -** localStorage와의 연결 담당
        - initStorage - localStorage 비어있을 경우 초기화
        - addItem - 해당 리스트에 item 추가
        - deleteItem - 해당 리스트에서 item 삭제
        - getIndex - 해당 리스트에서 item의 index 리턴
        - getList - 해당 리스트를 리턴
        - createStationOption - 역 목록 원소(?) 생성
    - **station.js**
        - (⭐html태그로 이동)EventListener - 역 추가 버튼 클릭 이벤트
        - addStationStorage - DB에 역 추가
        - deleteStationStorage - DB에서 역 삭제
        - isStationNameValid - 역 이름 종합 가능 여부
        - hasStationName - 역 이름 중복 여부 검사
        - isStationNameShort - 역 이름 길이 검사
        - isStationDeletionValid - 역 삭제 종합 가능 여부
        - isStationInLine - 역이 노선에 포함되었는지 검사
    - **line.js**
        - (⭐html태그로 이동)EventListener - 노선 추가 버튼 클릭 이벤트
        - addLineStorage - DB에 노선 추가
        - deleteLineStorage - DB에서 노선 삭제
        - isLineNameValid - 노선 이름 종합 가능 여부
        - hasLineName - 노선 이름 중복 여부 검사
        - isLineLengthValid - 노선 길이 종합 가능 여부
    - **Section.js**
        - addSectionStorage - DB에 노선 구간 추가
        - deleteSectionStorage - DB에서 노선 구간 삭제
        - isAdditionValid - 구간에서 역 추가 종합 가능 여부
        - hasStaionInLine - 구간이 역을 포함하는지 검사
        - isIndexOutOfRange - 입력받은 값이 노선 구간의 범위를 벗어나는지 검사
        - isDeletionValid - 구간에서 역 삭제 종합 가능 여부
        - hasEnoughStations - 구간에 역의 개수가 충분한지 검사

* * *
## **🎈 느낀점**

### 🎈 2주차 피드백 반영사항

- **기능 구현 목록을 재검토한다 -** 함수 목록을 먼저 완성하고 그대로 구현하는 게 좋은 방법인 줄 알았는데, 2주차 피드백을 보니 그게 아니라는 것을 알게 되었다. '함수 목록'을 삭제하고 전체적인 구조를 전달하려 했다. 예외사항은 눈에 띄게 따로 표시하였다.
- **상수를 활용한다 -** 결과 메세지와 같은 'string'값은 상수화할 생각은 했는데, 이동/정지 기준처럼 눈에 안 띄는 int값은 상수화할 생각은 못 했다. 이번에는 잊지 않고 '역 이름 길이' 기준을 상수화했다. 이후 로직을 변경할 때 훨씬 수월할 것 같다.
- **Boolean을 return하는 경우 간결하게 한다 -** 몰랐던 사실이다.. 예외사항을 처리하는 isValid 함수를 되도록이면 return 한 줄로 구현했다.
- **불필요한 변수를 줄이기 위해 노력한다 -** 초보자의 입장에서는 새 변수를 계속해서 만들게 되는 것 같아서.. let이나 const를 사용하더라도 새 변수를 최대한 적게 선언하려 했다. var을 금지시킨 이유를 알 것 같았다.
- **비지니스 로직과 UI로직을 분리해라 -** 3주차 과제는 '비즈니스 & 로직'을 기준으로 파일을 분리해보았다!
- **git을 통해 관리할 자원에 대해서도 고려한다 -** ㅠㅠ eslint 관련 파일은 커밋하지 않았다.

### 🎈 개인적으로 고려한 사항

- 예외사항을 'isValid' 류의 함수로만 관리하였다. 예를 들어 이름이 중복되는지 검사하는 hasNameOnList, 길이가 적절한지 검사하는 isLengthOutOfRange를 따로 만들고, 이런 예외사항을 한꺼번에 검사하는 최종(?)함수 isNameValid에 모두 담았다.
- 나의 코드를 처음 보는 사람도 이해하기 쉽게 하려고 노력하였다. 또 코드가 너무 복잡해지면 내가 쓴 코드임에도 버그를 찾을 때 시간이 너무 오래 걸렸기 때문이다. 내 능력 하에서 다른 사람이 봤을 때 수정이 쉬울 수 있도록 작성하였다.
    - 예컨대 모듈을 최대한 직관적으로 분리하고 각 파일의 길이가 너무 길어지지 않도록 했다.
    - 또한 'constants.js'에 분리해 둔 상수도 직관적으로 이름을 붙이려 했다. 예를 들어 '역 이름 길이 제한'은 'STATION.VALIDNAMELENGTH' 로 접근할 수 있다.
- 문제가 생기면 함수가 한 가지 기능만을 하는지 & "정말 제대로" 작동하는지 확인 후 수정했다.
    - 완벽하고 간결한 함수는 머리가 너무 복잡해지는 것을 막아주었다.
    - local storage에 추가하는 동작과 table에 추가하는 동작을 'addStation'이라는 함수로 묶으려다가 분리했다.

- 메뉴 구성 고민한 방법 순서대로 정리
- localStorage를 어떻게 구성했는지 정리
- innerHTML에 대한 생각

### 🎈 저번 주차에 비해 발전한 사항

- 한 파일의 길이가 줄어들었다. 파일 하나에 너무 많은 함수가 포함되어있으면 코드를 파악하기 힘들다.
    - '3. 구간 관리'에 해당하는 파일이 너무 길어져서 selection, managment, table 로 분리해서 관리했다.

### 🎈 여담

- 아직 JS스러운 코드를 잘 못 짜겠다... 코딩을 PS로 입문했더니 C스러움을 떨쳐버릴수가 없다.
- commit 메세지를 어떻게 해야할 지 모르겠다. 저번주에는 중간 저장하듯이 계속해서 커밋을 했는데, 이번에는 중간부터 깔끔하게 커밋했다... 언제 커밋해야할 지 기준을 모르겠다 ㅠㅠ
- 다른 분들의 결과물을 보면 배경지식의 차이가 느껴진다. 객체지향 프로그래밍이라든지.. 이건 정확히 공부해야 할 사항 같다.
- 너무 피곤하다. ... 재무경제 던졌다. ㅎㅏ...... 꼭 붙고싶다.
- 각종 위장병과 계절학기 재수강을 얻었다 제발붙여주세요 ㅠ.ㅠ 간절한 4학년
