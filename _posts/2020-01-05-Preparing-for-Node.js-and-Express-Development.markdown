---
layout: post
title:  "Node.js & Express 개발 준비"
date:   2020-01-05 22:22:22 +0900
categories: nodejs
author: Donghwa Lee
---
## Node.js 설치
[https://nodejs.org/en/](https://nodejs.org/en/)으로 이동합니다. LTS(Long Term Support) 버전과, 가장 최신의 Current, 두 가지를 다운로드 할 수 있는 녹색 버튼이 있습니다. 가장 최신의 사양을 필요로 하는 아주 특별한 경우가 아니면, LTS 버전으로 설치하기를 추천합니다.

![Node.js]({{ site.url }}/assets/images/2020-01-05/01.png)

터미널에서 아래와 같이 설치된 Node.js의 버전을 확인함으로써 정상설치 여부를 확인할 수 있습니다.
```shell
$ node -v
v12.14.0
```
<br/>

## Visual Studio Code 설치
[https://code.visualstudio.com/](https://code.visualstudio.com/)에서 다운로드 할 수 있습니다.

![VSCode]({{ site.url }}/assets/images/2020-01-05/02.png)

### Extension 설치
VSCode 사용을 편리하게 하는 각종 확장도구들을 설치합니다. VSCode 실행 후 `command + shift + X`로 Extensions View를 열고, 설치할 Extension을 검색 후 Install 버튼으로 설치합니다. 아래는 몇 가지 추천하는 Extension들입니다.

#### Beautify
<img src="https://hookyqr.gallerycdn.vsassets.io/extensions/hookyqr/beautify/1.5.0/1556863124877/Microsoft.VisualStudio.Services.Icons.Default" width="80" />

[Beautify](https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify)는 JavaScript, JSON, CSS, Sass, HTML 소스들을 아름답게 정리합니다.

#### Bracket Pair Colorizer
<img src="https://coenraads.gallerycdn.vsassets.io/extensions/coenraads/bracket-pair-colorizer/1.0.61/1542132753296/Microsoft.VisualStudio.Services.Icons.Default" width="80" />

[Bracket Pair Colorizer](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer)는 소스코드에서 서로 쌍이 되는 동일한 레벨의 괄호들을 색상으로 표현해서 식별을 용이하게 합니다.
<br/>
<br/>

## iTerm2 설치
macOS에서 기본으로 제공하는 터미널이 있지만 그보다 훨씬 강력한 기능을 가진 [iTerm2](https://iterm2.com/downloads.html) 터미널 에뮬레이터를  추천합니다.

![iTerm2]({{ site.url }}/assets/images/2020-01-05/03.png)
<br/>
<br/>

## Node 프로젝트 생성
프로젝트 디렉토리를 만들고, 해당 디렉토리에서 다음 명령으로 Node 프로젝트를 생성합니다. 명령어 실행 후 이어지는 질문에는 입력값 없이 enter 키를 눌러 진행할 수 있습니다. 입력값은 이후 생성되는 package.json 파일을 직접 수정하는 방법으로 변경할 수 있습니다.
```shell
$ npm init
```
이어서 `index.js` 이름으로 파일을 생성하고, 아래 내용을 파일에 작성합니다.
```javascript
console.log('Hello World!');
```
방금 만든 JavaScript 파일을 아래와 같이 Node.js로 실행하면 결과가 출력됩니다.
```shell
$ node index.js
Hello World!
```
<br/>

## Express 모듈 설치
Express는 Node.js에서 사용하는 package module입니다. Express를 사용하고자 하는 Node 프로젝트 디렉토리에서 아래와 같이 package 설치 명령으로 Express를 설치합니다.
```shell
$ npm install express --save
```
설치 프로젝트 디렉토리에는 `node_modules`라는 하위 디렉토리가 생성되었고, 여기에는 Express 모듈과 동시에 dependency가 있는 기타 모듈들이 함께 설치되었습니다.

이어서 Express 사용 예제들은 공식 웹 문서에서 제공하는 [다음](https://expressjs.com/ko/starter/hello-world.html)을 참고하기를 추천합니다.