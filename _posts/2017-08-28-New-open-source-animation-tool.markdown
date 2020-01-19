---
layout: post
title:  "Lottie : 새로운 오픈 소스 애니메이션 도구"
date:   2017-08-28 22:22:22 +0900
categories: trend
author: Donghwa Lee
---
아래는 Airbnb에서 Experience and Motion Designer로 일하고 있는 Salih Abdul-Karim(아래)의 글의 번역글이며, 원문 url은 아래와 같습니다.

번역 원문 :
[https://airbnb.design/introducing-lottie/](https://airbnb.design/introducing-lottie/)
<br/>

<figure>
  <img src="{{ site.url }}/assets/images/2017-08-28/01.jpg" />
  <figcaption>Salih Abdul-Karim is an Experience and Motion Designer at Airbnb.</figcaption>
</figure>

과거에는 Android, iOS 및 React Native 앱용 복합 애니메이션을 제작하는 것이 어렵고 긴 과정이었습니다. 각 화면 크기에 용량이 큰 이미지 파일을 추가하거나 1,000 줄이 넘는 관리하기 어려운 코드를 작성해야 했습니다. 이 때문에 대부분의 앱은 아이디어를 전달하고 강력한 사용자 경험을 창출하는 강력한 도구 임에도 불구하고, 애니메이션을 사용하지 않았습니다. 1 년 전, 우리는 그것을 바꾸기 시작했습니다.

오늘 우리는 우리의 솔루션을 소개하려고 합니다. Lottie는 After Effects 애니메이션을 실시간으로 렌더링하는 iOS, Android 및 React Native 라이브러리로, 정적 앱을 사용하는 것처럼 쉽게 기본 앱에서 애니메이션을 사용할 수 있습니다. Lottie는 [Bodymovin](https://github.com/airbnb/lottie-web) 이라는 오픈 소스를 이용한 After Effects 확장 기능에서 JSON 형식으로 추출한 애니메이션 데이터를 사용합니다 . 확장 기능은 웹상에서 애니메이션을 렌더링 할 수있는 JavaScript 플레이어와 번들로 제공됩니다. Bodymovin의 창시자 [Hernan Torrisi](https://twitter.com/airnanan)는 2015년 2월 이래로 매월 플러그인 기능과 개선사항을 추가하여 탄탄한 기반을 구축해왔습니다. 우리 팀([iOS](https://github.com/airbnb/lottie-ios)에는 [Brandon Withrow](https://github.com/buba447), [안드로이드](https://github.com/airbnb/lottie-android)에는 [Gabriel Peal](https://twitter.com/gpeal8), [React Native](https://github.com/react-native-community/lottie-react-native)에는 [Leland Richardson](https://twitter.com/intelligibabble), 그리고 [저는](https://twitter.com/therealsalih?lang=en) Experience Design을 담당)은 Torrisi의 놀라운 작업물을 시작으로 여정을 시작했습니다.

![Lottie]({{ site.url }}/assets/images/2017-08-28/02.gif)

Lottie를 사용하면 엔지니어가 다시 작성하는 번거로움 없이 풍부한 애니메이션을 제작할 수 있습니다. Nick Butcher의 [jump-through](https://medium.com/androiddevelopers/animation-jump-through-861f4f5b3de4) 애니메이션, Bartek Lipinski의 [햄버거 메뉴](https://android.jlelse.eu/animatedvectordrawablecompat-3d9568727c53#.fmiujhcdj), Miroslaw Stanek의 [Twitter heart](http://frogermcs.github.io/twitters-like-animation-in-android-alternative/)는 처음부터 애니메이션을 다시 만드는 것이 얼마나 어렵고 오래 걸리는지를 보여줍니다. Lottie를 활용하면 참조용을 위해 프레임워크를 파헤치고, 기간을 추측키만 하고, 직접 Bezier 곡선을 작성하고, 참조용 GIF로 애니메이션을 다시 만들어야 하는 일들이 과거가 될 것입니다. 이제 개발자는 디자이너의 의도를 정확하게 파악할 수 있습니다. 이를 증명하기 위해 우리는 샘플 애니메이션에서 각각의 애니메이션을 재 생성하고, After Effects 및 JSON 파일을 제공합니다.

우리의 목표는 가능한 한 많은 After Effects 기능을 지원하여 단순한 아이콘 애니메이션 이상의 것이 가능하도록 하는 것입니다. 우리는 라이브러리의 flexibility, richness 및 특별한 기능들을 보여줄 수 있는 몇 가지 샘플을 만들었습니다. 샘플 앱에는 기본 라인 아트, 문자 기반 애니메이션, 여러 각도와 컷이 포함된 동적 로고 애니메이션 등 다양한 종류의 애니메이션에 대한 소스 파일도 있습니다.

![Lottie]({{ site.url }}/assets/images/2017-08-28/03.gif)

이미 In-app 알림, 전체 프레임에서 움직이는 일러스트레이션 및 리뷰 플로우와 같은 여러 화면에서 자체 Lottie 애니메이션을 만들기 시작했습니다. 앞으로도 재미있고 유용한 방법으로 애니메이션 사용을 크게 확대할 계획입니다.

![Lottie]({{ site.url }}/assets/images/2017-08-28/04.gif)
<br/>
<br/>
<br/>

## 유연하고 효율적인 솔루션
Airbnb는 수백만 명의 게스트 및 호스트를 지원하는 글로벌 기업이므로 여러 플랫폼에서 재생할 수 있는 유연한 애니메이션 형식을 갖추는 것이 매우 중요했습니다. Marcus Eckert의 [Squall](http://www.marcuseckert.com/squall/) 이나 Facebook의 [Keyframes](https://github.com/facebookarchive/Keyframes)와 같은 Lottie와 유사한 라이브러리가 있지만 목표는 약간 다릅니다. Facebook은 주로 반응성에 초점을 맞추기 때문에 After Effects 기능을 지원하기 위해 작은 세트를 선택했지만, 우리는 최대한 많은 것을 지원하고자 합니다. Squall의 경우 Airbnb의 디자이너가 Lottie와 함께 사용합니다. 그 이유는 workflow의 필수적인 부분이 된 놀라운 After Effects 미리보기 앱이 있기 때문입니다. 그러나 iOS만 지원하며 엔지니어링 팀에서는 cross-platform 솔루션이 필요했습니다.

Lottie는 API를 보다 다양하고 효율적으로 만들 수 있는 몇 가지 기능을 API에 담고 있습니다. 네트워크를 통해 JSON 파일을 로드할 수 있으므로 A/B 테스트하기에 유용합니다. 또한 caching 메커니즘을 가지고 있어 자주 사용되는 애니메이션(예 : 위시리스트)은 캐시된 복사본을 매번 로드할 수 있습니다. Lottie 애니메이션은 제스처에 의해서 구동될 수 있으며, 애니메이션 속도는 간단한 값을 변경하여 조작할 수 있습니다. iOS는 런타임 시 애니메이션에 추가적인 native UI를 추가하는 기능을 지원하기 때문에 복잡한 애니메이션 전환에 사용할 수 있습니다.

지금까지 작업한 모든 After Effects 기능 및 API 추가 외에도 많은 아이디어가 있습니다. 여기에는 Lottie 애니메이션에 뷰를 매핑하고, Lottie로 뷰 전환을 제어하고, [Battle Axs의 RubberHose](https://www.battleaxe.co/rubberhose/)를 지원하고, 그라디언트, 타입 및 이미지 지원이 포함됩니다. 가장 어려운 것은 다음에 해결할 기능 하나를 선택하는 것입니다.

![Lottie]({{ site.url }}/assets/images/2017-08-28/05.png)
<br/>
<br/>
<br/>

## 커뮤니티 구성
오픈소스로 무언가를 공개하는 것은 모두가 사용할 수 있도록 공개하는 것 이상의 의미입니다. 이것은 사람들을 연결하고 커뮤니티를 만드는 다리입니다. 우리가 GitHub을 통해 디자이너와 엔지니어에게 Lottie를 공개할 때가 가까워짐에 따라, 우리는 애니메이션 관련 folks들과도 소통하고 싶었습니다.

우리는 [9 Squares](https://9-squares.tumblr.com/), [Motion Corpse](https://motioncorpse.tumblr.com/) 및 [Animography](https://animography.net/products/mobilo)가 만든 커뮤니티에서 영감을 받았습니다 . 이 세 명 모두는 공공 애니메이션 프로젝트에 협력하기 위해 전세계 사람들을 모았습니다. 이 프로젝트는 수개월의 작업과 각 팀의 많은 조직 및 논쟁을 가지고있지만 의심의 여지없이 애니메이션 커뮤니티 전체에 막대한 가치를 제공합니다. Motion Corpse 및 Animography는 After Effects 소스 파일도 공개적으로 공유하므로 사람들의 작업방식에 대한 통찰력을 제공합니다.

그들의 공동 연구 결과에 따라 우리는 세 팀 모두에게 샘플 앱에 애니메이션을 제공했습니다. JR Canest가 제작한 Motion Corpse의 애니메이션, 9 Square 프로젝트의 Al Boardman의 사각형 중 하나, Animography의 Mobilo 애니메이션 서체를 사용한 애니메이션 키보드가 포함되어 있습니다. 이 서체에는 24명이 넘는 아티스트의 작품이 있습니다. 우리는 이러한 애니메이션 커뮤니티와 강력한 개발 커뮤니티가 합쳐져 ​​뭔가 특별한 것을 만들어 내기를 바랍니다.

![Lottie]({{ site.url }}/assets/images/2017-08-28/06.gif)

디자이너, 애니메이터 또는 개발자든 상관없이 Lottie를 어떻게 사용하고 있는지 듣고 싶습니다. 당신의 생각, 의견 및 통찰력과 함께 lottie@airbnb.com으로 직접 문의해주세요. 우리는 상상도 못했던 방식으로 Lottie를 사용하기 시작했을 때, 전세계 사람들이 어떤 일을 할 것인지 알게 되다면 매우 기쁠 것입니다.
<br/>

**다운로드 [Bodymovin](https://github.com/airbnb/lottie-web), 로티 [iOS](https://github.com/airbnb/lottie-ios), [안드로이드](https://github.com/airbnb/lottie-android) 및 [React Native](https://github.com/react-native-community/lottie-react-native)**

[Brandon Withrow](https://github.com/buba447), [Gabriel Peal](https://twitter.com/gpeal8) 및 [Salih Abdul-Karim](https://twitter.com/therealsalih?lang=en)