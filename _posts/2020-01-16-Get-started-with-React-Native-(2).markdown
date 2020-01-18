---
layout: post
title:  "React Native 따라하기 (2)"
date:   2020-01-16 10:51:28 +0900
categories: react-native
author: Donghwa Lee
---
## Navigation
### react-navigation 기본 설치
다양한 navigation 라이브러리들이 있지만 그 중에서 [React Navigation](https://reactnavigation.org/)을 사용합니다. 프로젝트 디렉토리에서 아래와 같이 react-navigation 모듈을 설치합니다.

```shell
$ npm install --save react-navigation
```

이어서 의존성을 가지는 추가 모듈들을 설치합니다.

```shell
$ npm install --save react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context
```

마지막으로 iOS에서 pod를 링크하기 위해, ios 디렉토리로 이동한 후 아래와 같이 명령을 실행합니다.
```shell
$ cd ios
$ pod install
$ cd ..
```
<br/>

### Stack Navigator 구현
Stack Navigator에 필요한 모듈들을 설치합니다.

```shell
$ npm install --save react-navigation-stack @react-native-community/masked-view
```
@react-native-community/masked-view 모듈은 pod 링크가 필요하므로, ios 디렉토리로 이동한 후 아래와 같이 명령을 실행합니다.
```shell
$ cd ios
$ pod install
$ cd ..
```
#### Home Screen 생성
Stack Navigator에서 사용할 기본 화면을 정의합니다. 이전 포스트에서 `App/index.js` 파일에서 화면 요소들을 정의한 것과 내용은 동일합니다. 다만 이제 디렉토리를 구분하겠습니다. `App` 디렉토리 내에 `screens`라는 디렉토리를 생성하고, 그 안에 아래와 같은 소스로 `HomeScreen.js` 파일을 만듭니다.

```react
import React from 'react';
import {View, Text, StyleSheet} from 'react-native';

export default class HomeScreen extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>Home Screen</Text>
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
#### Stack Navigator 생성
`App` 디렉토리 내에 `navigators`라는 디렉토리를 생성하고, 아래와 같은 소스로 `StackNavigator.js` 파일을 만듭니다.
```react
import { createStackNavigator } from 'react-navigation-stack';

import HomeScreen from '../screens/HomeScreen';

export default createStackNavigator({
  Home: HomeScreen,
});
```

#### App Container 생성
`HomeScreen.js`으로 화면을 정의했고, 이 화면으로 구성되는 Stack Navigator를 `StackNavigator.js`로 정의했습니다. 이제 이 Stack Navigator가 실질적으로 앱에서 사용될 수 있도록 합니다. `App/index.js`을 아래와 같이 편집합니다.
```react
import { createAppContainer } from 'react-navigation';

import StackNavigator from './navigators/StackNavigator';

export default createAppContainer(StackNavigator);
```

신규 파일들을 다수 만들었고, iOS Pod를 다수 설치했기 때문에 Metro Bundler를 다시 실행하고, 앱을 리로드합니다. 아래와 같이 Stack Navigator가 적용되면서 화면 상단에 Navigation bar가 생겼고, 기본 화면으로 Home Screen이 보입니다.

<img src="{{ site.url }}/assets/images/2020-01-16-01.png" width="320" />

지금까지의 작업을 commit 합니다.

```shell
$ git add .
$ git commit -m "Add a stack navigator"
```

다음 포스트에서는 Stack Navigator에 화면을 더 추가하고, 화면 간 이동을 다루겠습니다.