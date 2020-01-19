---
layout: post
title:  "React Native 따라하기 (1) : Create a project"
date:   2020-01-15 22:22:22 +0900
categories: react-native
author: Donghwa Lee
---
![React-Native]({{ site.url }}/assets/images/2020-01-15/00.png)

### 새로운 프로젝트 생성
프로젝트 이름을 `RNBoilerplate`로 하여 새로운 프로젝트를 만듭니다.

```shell
$ npx react-native init RNBoilerplate
```
이제 `RNBoilerplate` 디렉토리가 생성되었고, 그 디렉토리로 이동 후 프로젝트를 실행합니다.

```shell
$ cd ./RNBoilerplate
$ npx react-native run-ios
```
자동으로 터미널에서 Metro Bundler가 실행되고, 이어서 Simulator가 실행되어 잠시 뒤 아래와 같이 프로젝트 기본 화면을 볼 수 있습니다.

<img src="{{ site.url }}/assets/images/2020-01-15/01.png" width="320" />
<br/>
<br/>

### 프로젝트 개발 준비
#### Git 초기화
개발소스 형상관리를 위해 Git을 사용합니다. 프로젝트 디렉토리에서 Git 초기화 명령을 합니다.

```shell
$ git init
```
그리고 현재 상태의 소스들을 stage에 추가하고, commit 합니다.

```shell
$ git add .
$ git commit -m "Create react-native project"
```

#### 기본 소스 초기화
프로젝트 기본으로 구현되어 있는 화면 대신, 이 Boilerplate 프로젝트가 가질 화면으로 대체합니다. 기본 화면은 프로젝트 루트에 위치한 `App.js`에 정의되어 있습니다. 이것을 삭제하고, `App`이란 디렉토리와 그 하위에 `index.js`라는 파일을 생성하고 아래 소스를 씁니다.

```react
import React from 'react';
import {View, Text, StyleSheet} from 'react-native';

export default class App extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>RNBoilerplate</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
});
```
`App.js` 파일을 제거하고, 새로운 디렉토리와 파일을 생성했기 때문에 Metro Bundler를 다시 실행하는 것이 필요합니다. Metro Bundler가 실행되어 있는 터미널을 종료하고, 새로운 터미널에서 아래와 같이 실행합니다.

```shell
$ npm start
```
Simulator에서 Cmd + R 키로 앱을 reload 합니다. 여기까지 아래와 같은 화면을 볼 수 있습니다.

<img src="{{ site.url }}/assets/images/2020-01-15/02.png" width="320" />

지금까지의 작업을 commit 합니다.

```shell
$ git add .
$ git commit -m "Edit the default screen"
```
<br/>
다음 포스트에서는 Navigation 구성을 진행하겠습니다.