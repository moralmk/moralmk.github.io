---
layout: post
title:  "React Native 따라하기 (3) : Stack Navigation"
date:   2020-01-17 11:25:49 +0900
categories: react-native
author: Donghwa Lee
---
React Navigation 모듈 설치와 Stack Navigation 기초 구현은 [React Native 따라하기 (2) : Navigation](https://moralmk.github.io/react-native/2020/01/16/Get-started-with-React-Native-(2).html) 편을 참고하세요.
<br/>
<br/>

### Sub Screen 생성
Stack Navigator에 기반해 홈 화면에서 다른 화면으로 이동하도록 하겠습니다. 먼저 `App/screens` 디렉토리 안에 이동할 목적지 화면 `SubScreen.js`을 아래 소스로 작성합니다.
{% gist moralmk/0d9bf649ceb56a4869286618a520e2aa SubScreen.js %}
<br/>

### Navigation 정의
네비게이션을 정의한 `App/navigators/StackNavigator.js` 파일에 방금 작성한 `SubScreen.js`를 추가합니다.
{% gist moralmk/0d9bf649ceb56a4869286618a520e2aa StackNavigator.js %}
<br/>

### 버튼 이벤트 추가
마지막으로 홈 화면 안에 Sub 화면으로 이동하게끔 하는 버튼을 추가하고 이벤트를 정의합니다.
{% gist moralmk/0d9bf649ceb56a4869286618a520e2aa HomeScreen.js %}
이제 홈 화면에는 버튼이 추가되었고, 해당 버튼을 통해 Sub 화면으로 이동합니다.

<img src="{{ site.url }}/assets/images/2020-01-17/01.png" width="320" />
<img src="{{ site.url }}/assets/images/2020-01-17/02.png" width="320" />

지금까지의 작업을 commit 합니다.

```shell
$ git add .
$ git commit -m "Add a subscreen to stack navigator"
```