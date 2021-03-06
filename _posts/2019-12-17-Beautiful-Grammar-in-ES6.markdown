---
layout: post
title:  "ES6의 아름다운 문법들"
date:   2019-12-17 14:09:01 +0900
categories: javascript
author: Donghwa Lee
---
![ES6]({{ site.base_url}}/assets/images/2019-12-17-ES6의-아름다운-문법들.png)

## 비구조화
객체에서 데이터를 추출하는데 간편한 문법이다. 다음와 같은 객체가 있다고 하자.
```javascript
var myProfile = {
  name: 'Donghwa',
  sex: 'Male'
};
```
ES5 코드로는 아래와 같이 데이터를 추출할 수 있다.
```javascript
var name = myProfile.name;
var sex = myProfile.sex;
```
ES6 코드로 위 두 라인은 한 라인으로 간소화할 수 있다.
```javascript
var { name, sex } = myProfile;
```
<br/>
이러한 코드는 React Native 개발 시, Component들을 불러올 때 자주 볼 수 있을 것이다.
```javascript
var { View, Text } = require('react-native');
```
물론 아래와 ES6 import 구문을 사용할 때도 적용할 수 있다.
```javascript
import { View, Text } from 'react-native';
```
<br/>

## 모듈 불러오기
다른 모듈을 불러올 때는 `require`를, 내보낼 때는 `module.exports`에 값을 주는 방식을 아래와 같이 각각 사용하는데 이는 CommonJS 문법이다.
```javascript
var SomeComponent = require('./someComponent');
```
```javascript
module.exports = function(val) {
  // some code
};
```
ES6 문법으로는 이를 각각 `import`, 그리고 `export`로 사용한다. 위 코드들은 아래와 같이 구현될 수 있다.
```javascript
import SomeComponent from '/someComponent';
```
```javascript
export default function(val) {
  // some code
};
```
<br/>

## 화살표 함수
ES5 문법으로 아래와 같이 함수를 정의했다고 하자.
```javascript
var someFunction = function(val) {
  // some code
};
```
ES6 문법으로는 다음과 같이 쓸 수 있다.
```javascript
var someFunction = (val) => {
  // some code
};
```
표현식만 다른 것이 아니라 기능에도 차이가 있다. ES5 문법에서는 함수가 실행되는 context를 명확히 하기 위해서 아래와 같이 `bind` 명령을 추가한다.
```javascript
var someFunction = function(val) {
  // some code
}.bind(this);
```
그러나 ES6 문법에서는 이러한 명령을 따로 해줄 필요가 없다.
<br/>
<br/>

## 문자열 조립
이러한 문자열 조립을 자주 하거나 보았을 것이다.
```javascript
var DOMAIN = 'awesome-domain.com';
var url = 'http://' + DOMAIN + '/awesome-post.html';
```
'+'들로 지저분한 저 라인은 ES6 문법에서 아름답게 정리될 수 있다.
```javascript
var DOMAIN = 'awesome-domain.com';
var url = 'http://${DOMAIN}/awesome-post.html';
```
<br/>

## let, const 변수 선언
ES6 이전에는 변수를 선언할 때 `var`만 사용해왔다. 이 때 아래와 같이 동일한 변수 이름을 재선언 하는 것이 가능했었기 때문에 JavaScript를 욕하는 사람들이 참 많았다.
```javascript
var a = 1;
var a = 2;
```
ES6 문법에서는 변수 선언 시, `let`과 `const` 방법이 추가되었고, 이 둘은 변수 재선언이 불가능하다. `let`과 `const` 둘의 차이점은 immutable 가능여부이다. `let`으로 선언한 변수에는 값의 재할당이 가능하지만 `const`는 불가능하다.

추가로 `var` 방식은 function-scoped로 hoisting 되는 반면, `let`과 `const`는 block-scoped로 hoisting 된다.