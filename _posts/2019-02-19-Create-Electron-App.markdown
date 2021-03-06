---
layout: post
title:  "Electron 앱 만들기 맛보기"
date:   2019-02-19 22:22:22 +0900
categories: javascript
author: Donghwa Lee
---
[Electron](https://electronjs.org/)을 이용하면 Chromium과 Node.js를 사용하여 HTML, CSS, 그리고 JavaScript 만으로 데스크톱 애플리케이션을 만들 수 있습니다. 특히 Mac, Windows, Linux 세 가지 플랫폼에서 빌드되고 동작하기 때문에 아주 효율적입니다.

Skype, [Github Desktop](https://desktop.github.com/), [GitKraken](https://www.gitkraken.com/), [Visual Studio Code](https://code.visualstudio.com/), [Slack](https://slack.com/intl/en-kr/), [Atom](https://atom.io/)... 개발자라면 익숙해할 이 데스크톱 애플리케이션들이 모두 Electron으로 설계된 것들 입니다.
<br/>
<br/>

## 프로젝트 생성 및 준비
먼저 프로젝트 폴더를 생성한 후 초기화 합니다. 그리고 electron을 설치합니다. 여기에서 프로젝트명은 `snicat` 으로 하겠습니다.
```shell
$ mkdir snicat && cd snicat
$ npm init
$ npm install --save-dev electron
```
<br/>

## 애플리케이션 구동 파일 작성
`main.js` 파일을 작성합니다. 애플리케이션이 준비되면 브라우저 윈도우를 800x600 사이즈로 생성한 뒤 `index.html` 페이지를 표시하는 내용입니다.
{% gist moralmk/aa01da085027a5b36836121ed6e4d2b3 main.js %}
<br/>

## 페이지 파일 작성
`index.html` 파일을 작성합니다.
{% gist moralmk/aa01da085027a5b36836121ed6e4d2b3 index.html %}
이와 같은 결과를 보여주는 페이지입니다.
![Hello World!]({{ site.url }}/assets/images/2019-02-19-Electron-앱-만들기-맛보기.png)
<br/>
<br/>

## 실행 스크립트 추가
프로젝트 초기화 시에 생성된 `package.json` 내용을 수정합니다.
{% gist moralmk/aa01da085027a5b36836121ed6e4d2b3 package.json %}
5번째 라인은 앞서 작성한 `main.js` 파일입니다. 그리고 8번째 라인은 애플리케이션 실행을 위한 스크립트 명령입니다.
<br/>
<br/>

## 애플리케이션 실행
마지막으로 아래 명령으로 애플리케이션을 실행합니다.
```shell
$ npm start
```