---
layout: post
title:  "React Native 따라하기 (3)"
date:   2020-01-17 09:09:09 +0900
categories: react-native
author: Donghwa Lee
---
## Stack Navigation
### SubScreen 생성
Stack Navigator에 기반해 홈 화면에서 다른 화면으로 이동하도록 하겠습니다. 먼저 `App/screens` 디렉토리 안에 이동할 목적지 화면 `SubScreen.js`을 아래 소스로 작성합니다.

```react
import React from 'react';
import {View, Text, StyleSheet} from 'react-native';

export default class SubScreen extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>Sub Screen</Text>
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
네비게이션을 정의한 `App/navigators/StackNavigator.js` 파일에 방금 작성한 `SubScreen.js`를 추가합니다.

```react
import { createStackNavigator } from 'react-navigation-stack';

import HomeScreen from '../screens/HomeScreen';
import SubScreen from '../screens/SubScreen'; // import SubScreen.js

export default createStackNavigator({
  Home: HomeScreen,
  Sub: SubScreen, // Sub Screen 추가
});
```
<br/>

### 버튼 이벤트 추가
마지막으로 홈 화면 안에 Sub 화면으로 이동하게끔 하는 버튼을 추가하고 이벤트를 정의합니다.

```react
import React from 'react';
import {View, Text, StyleSheet, TouchableOpacity} from 'react-native';

export default class HomeScreen extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>Home Screen</Text>

        {/* 버튼 */}
        <TouchableOpacity onPress={this.navigateToSub} style={styles.button}>
          <Text>Navigate to Sub Screen</Text>
        </TouchableOpacity>
      </View>
    );
  }

  // 버튼 이벤트
  navigateToSub = () => {
    this.props.navigation.navigate('Sub');
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  // 버튼 스타일
  button: {
    marginTop: 16,
    width: 200,
    height: 40,
    alignItems: 'center',
    justifyContent: 'center',
    borderWidth: StyleSheet.hairlineWidth,
    borderColor: 'gray',
    borderRadius: 4,
    backgroundColor: 'white',
  }
});
```

이제 홈 화면에는 버튼이 추가되었고, 해당 버튼을 통해 Sub 화면으로 이동합니다.

<img src="{{ site.url }}/assets/images/2020-01-17-01.png" width="320" />
<img src="{{ site.url }}/assets/images/2020-01-17-02.png" width="320" />

지금까지의 작업을 commit 합니다.

```shell
$ git add .
$ git commit -m "Add a subscreen to stack navigator"
```