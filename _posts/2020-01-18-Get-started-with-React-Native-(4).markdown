---
layout: post
title:  "React Native 따라하기 (4) : Drawer Navigation"
date:   2020-01-18 10:26:31 +0900
categories: react-native
author: Donghwa Lee
---
### react-navigation-drawer 모듈 설치
Drawer Navigator 구현을 위해 필요한 `react-navigation-drawer` 모듈을 아래와 같이 설치합니다.

```shell
$ npm install --save react-navigation-drawer
```
<br/>

### Drawer Screen 생성
Drawer 화면에 해당하는 파일을 `App/screens` 디렉토리 내 `DrawerScreen.js` 파일명으로 아래와 같이 작성합니다.

```react
import React from 'react';
import {View, Text, StyleSheet} from 'react-native';

export default class DrawerScreen extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>Drawer Screen</Text>
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
<br/>

### Navigation 정의
Stack Navigator에 이어 Drawer 네비게이션을 정의할 Navigator를 `App/navigators` 디렉토리 내 `DrawerNavigator.js` 파일로 작성합니다. Drawer Navigator는 Stack Navigator를 포함하고, Drawer에서 사용할 Content component로 방금 작성한 `DrawerScreen.js`를 정의합니다.

```react
import { createDrawerNavigator } from 'react-navigation-drawer';

import StackNavigator from './StackNavigator';
import DrawerScreen from '../screens/DrawerScreen';

export default createDrawerNavigator({
  Default: StackNavigator, // Stack Navigator 포함
}, {
  contentComponent: DrawerScreen, // Content component 정의
});
```
<br/>

### Open Drawer 버튼 이벤트
이제 Drawer를 오픈하게 하는 버튼을 홈 화면에 추가합니다. 아래와 같이 버튼을 정의하는 코드를 삽입합니다.

```
<TouchableOpacity onPress={this.openDrawer} style={styles.button}>
  <Text>Open Drawer</Text>
</TouchableOpacity>
```

그리고 `this.openDrawer`로 정의된 함수와 함께 여기에 Drawer를 오픈하는 코드를 작성합니다.

```javascript
openDrawer = () => {
  this.props.navigation.toggleDrawer();
}
```

이제 홈 화면에 Drawer를 오픈하는 버튼이 추가되었고, 해당 버튼을 누르면 Drawer가 열립니다.

<img src="{{ site.url }}/assets/images/2020-01-18/01.png" width="320" />
<img src="{{ site.url }}/assets/images/2020-01-18/02.png" width="320" />

지금까지의 작업을 commit 합니다.

```shell
$ git add .
$ git commit -m "Add a drawer"
```