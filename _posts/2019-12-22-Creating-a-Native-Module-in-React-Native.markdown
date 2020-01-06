---
layout: post
title:  "Creating a Native Module in React Native"
date:   2019-12-22 10:57:18 +0900
categories: react-native
author: Donghwa Lee
---
## Create a Native Module
Native Module을 만드는 가장 손쉬운 방법은 `create-react-native-module`를 사용하는 것입니다. 먼저 이것을 global로 아래와 같이 설치해보겠습니다.
```shell
$ yarn global add create-react-native-module
```
방금 설치한 `create-react-native-module`를 통해서 이제 우리가 만들 모듈 생성을 시작해보겠습니다. 모듈 이름은 `MyModule`로 하고, 아래와 같이 생성할 수 있습니다.
```shell
$ create-react-native-module MyModule
```
모듈 이름으로 지정한 `MyModule`에 따라, `react-native-my-module` 디렉토리가 생성되었고, 해당 디렉토리 안에는 `ios`, `android` 디렉토리와 함께 Native Module을 정의하는데 필요한 기본 세트가 정의되어 있습니다. 이 디렉토리로 이동하고, 관련 dependency 설치를 위해 아래와 같이 명령을 실행합니다.
```shell
$ cd react-native-my-module
$ yarn install
```
자! 이제 Native Module을 개발할 수 있는 기본 준비가 끝났습니다.
<br/>
<br/>

## iOS Module
하위 디렉토리로 `android`, `ios`가 생성되어 있을텐데요. 우리는 먼저 ios 모듈 부터 작업해보겠습니다. `ios` 디렉토리에는 `MyModule.h`, `MyModule.m` 두 파일과 나머지 두 디렉토리가 있습니다. 우리가 작업할 대상은 이 중에서도 `MyModule.m`입니다. 아래는 초기 `MyModule.m`의 내용입니다.
```c
#import "MyModule.h"

@implementation MyModule

RCT_EXPORT_MODULE()

RCT_EXPORT_METHOD(sampleMethod:(NSString *)stringArgument numberParameter:(nonnull NSNumber *)numberArgument callback:(RCTResponseSenderBlock)callback)
{
    // TODO: Implement some actually useful functionality
    callback(@[[NSString stringWithFormat: @"numberArgument: %@ stringArgument: %@", numberArgument, stringArgument]]);
}

@end
```
기본으로 셋업되는 템플릿 소스를 확인할 수 있습니다. `sampleMethod`라는 이름을 가지며, 세 가지 인자를 받네요. 첫 번째는 `NSString` 타입, 두 번째는 `NSNumber` 타입, 마지막은 `callback` 함수로 보여집니다. 수행하는 일은 인자로 받은 callback 함수를 호출하면서 동시에 함께 받은 문자열과 숫자를 전달하네요. 우리는 추가 내용 없이 이 코드를 예시로 다음으로 진행하겠습니다.
<br/>
<br/>

## Android Module
`android` 디렉토리 하위 `src/main/java/com/reactlibrary`에 까지 이동하면 `MyModuleModule.java`, 그리고 `MyModulePackage.java` 두 개의 파일이 있습니다. 메소드를 정의하고 주요 코드를 작성할 파일은 `MyModuleModule.java`입니다. 초기 내용은 아래와 같습니다.
```java
package com.reactlibrary;

import com.facebook.react.bridge.ReactApplicationContext;
import com.facebook.react.bridge.ReactContextBaseJavaModule;
import com.facebook.react.bridge.ReactMethod;
import com.facebook.react.bridge.Callback;

public class ResizeImageModule extends ReactContextBaseJavaModule {

    private final ReactApplicationContext reactContext;

    public ResizeImageModule(ReactApplicationContext reactContext) {
        super(reactContext);
        this.reactContext = reactContext;
    }

    @Override
    public String getName() {
        return "ResizeImage";
    }

    @ReactMethod
    public void sampleMethod(String stringArgument, int numberArgument, Callback callback) {
        // TODO: Implement some actually useful functionality
        callback.invoke("Received numberArgument: " + numberArgument + " stringArgument: " + stringArgument);
    }
}
```

iOS와 마찬가지로 템플릿 메소드가 정의되어 있고, 이름은 `sampleMethod`, `String` 타입 인자와 `int` 타입 인자, `callback`을 전달하며, 수행하는 작업도 동일합니다.
<br/>
<br/>

## How to use in JavaScript
### Install module in your project
위와 같이 정의된 Native Module을 프로젝트에 사용하기 위해 먼저 해당 프로젝트에 설치하는 작업이 필요합니다. 이미 만들어져 있는 모듈을 불러 사용하고자 할 때 `npm install`, 또는 `yarn add` 명령으로 모듈을 설치하는데요. 이 명령을 사용하는 것은 npm 저장소에 이미 배포가 되어 있는 모듈일 때에만 해당합니다.

직접 생성한 Native Module이고, 아직 npm 저장소에 배포가 되기 전이라면 `react-native install` 명령을 사용해야 합니다. 먼저 모듈을 설치하고자 하는 프로젝트 디렉토리로 이동해서 Native Module이 위치한 상대 디렉토리 경로와 함께 아래와 같은 명령으로 설치합니다.
```shell
$ react-native install ../react-native-my-module
```
이후 iOS의 경우에는 프로젝트 내 `ios` 폴더에서 `pod install`하게 되면 방금 설치한 `react-native-my-module`이 iOS 프로젝트에 Pod로 인스톨 되어 반드시 여기까지 진행해야 JavaScript에서 호출이 가능합니다.

### Use in JavaScript
이제 이 Native Module을 실제로 JavaScript로 호출해보겠습니다. 사용하고자 하는 js 파일에서 아래와 같이 해당 모듈을 선언합니다.

```javascript
import MyModule from 'react-native-my-module';
```
그런 다음 모듈이 가지는 `sampleMethod` 함수를 아래와 같이 호출할 수 있습니다.
```javascript
MyModule.sampleMethod('some text', 0, function(text, num) {
    console.log(text, num);
});
```
문자열 데이터를 첫 번째, 숫자형 데이터를 두 번째, 그리고 `callback` 함수를 세 번째 인자로 전달했습니다. 실행결과는 `callback` 함수 내용에 따라 문자열과 숫자형 데이터가 각각 콘솔에 출력됩니다.
<br/>
<br/>

## Native Module 필요한 이유
iOS/Android 플랫폼에 직접적으로 액세스 하기 위해서는 Native Module이 필요하고, 다행히 아마 거의 대부분의 기능들은 이미 React Native 모듈이 만들어져 있을테니, 우리는 잘 찾고, 잘 사용하기만 하면 됩니다. 그럼에도 불구하고 **플랫폼 레벨의 고급 확장기능을 사용해야 한다거나, 고성능의 멀티스레드 코드 작성이 필요하다면** 우리는 Native Module을 직접 작성하는 것이 필요할 수 있습니다.