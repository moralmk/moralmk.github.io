---
layout: post
title:  "Hybrid Apps And React Native: A Time To Transition?"
date:   2017-08-23 22:22:22 +0900
categories: react-native
author: Donghwa Lee
---
번역 원문 :
[https://www.smashingmagazine.com/2017/06/transition-hybrid-apps-react-native/](https://www.smashingmagazine.com/2017/06/transition-hybrid-apps-react-native/)
<br/>
<br/>
![React Native]({{ site.url }}/assets/images/2017-08-23/01.png)

뮤지션에게는 현재 자신의 경력을 한 단계 더 발전시키기 위해 어느 순간에는 오래된 습관을 잊어야 할 때가 있습니다. 이것은 궁극적으로는 더 나은 수준이 되게 하지만 그 과정 상에는 종종 한시적으로 후퇴하게 만들기도 합니다. 새로운 기술이 습득되면 이전 기술로는 도저히 불가능했던 새로운 수준에 도달할 수 있습니다.

뮤지션과 마찬가지로 모든 전문가는 자신의 방법론에 자주 질문하고 다른 옵션이 있는지 확인해야 합니다. 한 접근법이 이전에 최고였던 것이 그것이 언제까지나 최상의 상태라는 것을 의미하지는 않습니다. 우리는 늘 더 나은 접근법에 대해서 고려해야 하고, 가장 익숙한 접근법에 지나치게 편향되어 있지는 않은지 생각해보아야 합니다.

이 글에서는 하이브리드 모바일 앱 개발에 대해서 React Native가 여러 가지면에서 우수한 솔루션이라고 할 수 있는 이유를 이야기합니다. 이를 위해 먼저 하이브리드 앱이 나타나게 된 배경을 살펴보고 현재까지 나와있는 방법을 알아보겠습니다. 그런 다음 컨텍스트 안에서 React Native가 어떻게 자리하는 논의하고, 대부분의 경우에 대해 React Native가 왜 더 나은 접근 방식인지를 설명합니다.
<br/>
<br/>

## An Origin Story
2010년입니다. A사는 jQuery를 사용하는 멋진 웹 애플리케이션을 사용합니다. HTML, CSS 및 JavaScript에 능숙한 개발자들로 이루어진 팀이 있습니다. 갑자기 모바일 앱을 만들어야 하는 이슈가 생겨났습니다. 팀원들은 자신만의 모바일 앱을 만드는 방법을 광란하게 연구하고 즉시 여러 가지 문제에 직면하게됩니다. 팀에는 Java 또는 Objective-C 개발자는 없고, 더욱이 별도의 두 가지 앱을 개발, 테스트 및 배포할 여력이 없는 상황입니다.

하지만 걱정할 필요가 없습니다. 하이브리드 모바일 앱이 해결책이 될 수 있습니다. 이 신기술을 사용하면 (이론적으로) 새로운 모바일 앱을 위해 코드와 노하우들을 쉽게 재사용 할 수 있습니다. Cordova, PhoneGap 등의 프레임워크를 선택해서 모바일 앱을 제작하거나 포팅할 수 있습니다!

위와 같은 방법으로 많은 기업과 개발자에게서 문제가 해결될 수 있었고, 그들은 자신만의 모바일 앱을 만들 수 있었습니다.
<br/>
<br/>

## Problems Arise
2010년 이래로 개발자포럼, 블로그 및 게시판에는 하이브리드 앱의 생산성, 효율성에 대한 논란이 가득합니다. 이전 단락에서 설명한 유연성과 이점에도 불구하고 하이브리드 앱은 매우 실제적인 문제점과 단점을 가지고 있습니다. 다음은 가장 주목할만한 몇 가지 문제입니다.
### USER-EXPERIENCE SHORTCOMINGS
지난 몇 년 동안 모바일 앱의 UX에 대한 관심과 니드가 극적으로 증가했습니다. 대부분의 스마트 폰 소유자는 소수의 프리미어 앱만 사용하며 대부분의 시간을 보냅니다. 사용자들은 아마도 Facebook, MLB TV, YouTube 및 Uber와 같은 세련된 UX의 앱을 기대합니다.

이 매우 높아진 기대치에 하이브리드 앱은 모든 것을 만족시키기가 매우 어렵습니다. 반응이 느리거나 제한된 애니메이션, 키보드 오작동 및 플랫폼 별 인식하는 제스처의 한계와 같은 문제는 모두 하이브리드 앱을 만족스럽다라고 생각하기 어렵게 합니다. 이 문제를 복잡하게하는 것은 하이브리드 애플리케이션이 오픈 소스 커뮤니티에 의존하여 네이티브 기능을 위한 래퍼런스를 작성하는 것입니다. 다음은 이러한 문제를 잘 표현해주는 어느 앱의 스크린샷입니다. 이 애플리케이션은 Ionic의 쇼케이스에서 소개되었으며, Morgan Stanley가 만들었습니다.

<figure>
  <img src="{{ site.url }}/assets/images/2017-08-23/02.png" />
  <figcaption>Screenshot of the app store listing for MS StockPlan</figcaption>
</figure>

몇 가지 내용은 즉시 명백하게 확인할 수 있습니다. 이 앱의 평점은 매우 낮습니다(별 2.5개). 모바일 앱처럼 보이지 않지만 분명히 모바일 웹 앱의 모습입니다. 고유하지 않은 세그먼트 컨트롤, 글꼴 크기, 텍스트 밀도 및 기본형이 아닌 탭 표시줄 등이 눈에 띕니다. 이 앱은 기본적으로 구현이 쉽지 않고, 특히 가장 중요한 점은 고객이 이러한 모든 문제를 파악하고 있으며, ‘오래되었다’라는 느낌이라고 평가합니다.
### USER INTERFACE CHALLENGES
대다수의 사용자는 새로운 앱을 제거하거나 잊어버리는 주기가 매우 짧습니다. 앱이 좋은 첫 인상을 보이고 사용자가 쉽게 이해할 수 있는 것이 중요합니다. 하이브리드 앱은 멋지게 보일 수 있지만, 웹 앱처럼 보이거나, 다른 플랫폼 독립적인 성격에 따라 다른 플랫폼의 모습으로 보일 수 있는 등의 문제를 동시에 가지고 있습니다.

앱을 설치하기 전에 많은 고객이 앱 스토어의 이미지를 검토합니다. 이러한 스크린샷이 매력적이지 않거나 불쾌감을주는 경우에는 앱이 전혀 다운로드되지 않을 수 있습니다. 다음은 그러한 앱의 한 예입니다. 이 앱은 Nationwide에서 제작했으며, 두 앱 모두 모바일 앱이 아닌 모바일 반응형으로 제작된 웹 사이트처럼 보입니다.

<div style="display: flex; flex-direction: row;">
  <figure>
    <img src="{{ site.url }}/assets/images/2017-08-23/03.png" width="320" />
    <figcaption>Screenshot of the Nationwide app on iOS</figcaption>
  </figure>
  <figure style="margin-left: 16px;">
    <img src="{{ site.url }}/assets/images/2017-08-23/04.png" width="320" />
    <figcaption>Screenshot of the Nationwide app on Android</figcaption>
  </figure>
</div>

앱 스토어 리뷰에서 이 앱에는 몇 가지 문제가 있지만 이러한 UI가 있는 앱은 새로운 고객을 유치할 가능성이 거의 없어 보입니다. 이 앱은 반드시 이 앱을 사용해야만 하는 기존의 고객들에 의해서만 사용될 것입니다.
### PERFORMANCE ISSUES
하이브리드 애플리케이션에 대한 가장 일반적인 불만은 성능, 버그 및 충돌입니다. 물론 모든 앱에서 이러한 문제가 나타날 수 있지만 성능 문제는 오랫동안 하이브리드 앱을 괴롭히고 있습니다. 또한 하이브리드 애플리케이션은 종종 오프라인 지원이 적고 열악한 네트워크 조건에서는 치명적으로 성능이 저하될 수 있습니다. 모든 개발자는 위에서 언급 한 내용 중 ‘버그’라고 하는 것을들은 적이 아마 있을 것이고, 결과적으로 공개적으로 벌점 처리된 앱을 보유하고 있을지도 모르겠습니다.
### OVERALL LACK OF PREMIER APPS
PhoneGap과 Ionic으로 개발된 애플리케이션들은 ‘Best App’으로 분류되는 리스트에서 잘 찾을 수 없습니다. 유망한 하이브리드 애플리케이션의 예로 ‘Untappd’가 있습니다. Untappd는 상당히 훌륭한 플랫폼임에도 불구하고 다운로드 횟수는 불과 5 백만회 미만입니다. 이것은 큰 숫자처럼 보일지 모르지만 가장 많이 사용되는 앱 목록에서 비교하면 상당히 저조한 숫자입니다.

또한 하이브리드에서 네이티브로 마이그레이션 한 많은 애플리케이션들이 있습니다. 이 목록에는 Facebook, TripAdvisor, Uber, Instagram 및 많은 사람들이 훌륭하다고 평가하는 앱입니다.

반대로 네이티브에서 하이브리드로 이동한 앱을 찾는 것은 상당히 어려울 것입니다.
### FINAL DEFENCE OF HYBRID APPS
이 섹션의 핵심은 하이브리드 앱을 지나치게 비판하는 것이 아니라 대안적인 접근 방식을 위한 여지가 있음을 보여주는 것입니다. 하이브리드 앱은 매우 중요한 기술이었으며 많은 경우에 성공적으로 사용되었습니다. Ionic 쇼케이스에서 보면 위에서 예를 든 앱들보다 더 좋아 보이는 여러 가지 앱이 있습니다. Baskin Robbins, Pacifica 및 Sworkit은 최근의 세 가지 예입니다.

지난 4년 동안 하이브리드 앱 개발자와 프레임워크는 앱을 개선하기 위해 열심히 노력했으며 훌륭한 일을 해왔습니다. 그러나 근본적인 문제와 단점이 남아 있지만, 만약 지금부터 새로운 앱을 제작한다면 더 나은 옵션을 찾을 수 있습니다.
<br/>
<br/>

## Another Approach
하이브리드 앱이 네이티브 앱을 완전히 대체하기에는 부족하지만, 그 장점과 성공은 무시할 수 없습니다. 하이브리드 앱은 리소스, 생산성 및 기능 문제 등 실질적인 문제를 해결하는데 도움이 됩니다. 하이브리드 애플리케이션의 단점을 제거하면서 장점을 그대로 가져갈 수 있는 접근 방법이 있다면 상당히 매력적일 것입니다. 그리고 여기에 React Native가 대답이 될 수 있습니다.
### OVERVIEW AND ADVANTAGES
React Native는 널리 사용되는 React 웹개발 프레임워크를 기반으로 하는 크로스 플랫폼 모바일 애플리케이션 개발 프레임워크입니다. React와 마찬가지로 React Native는 Facebook 및 Instagram의 개발자가 주로 관리하는 오픈 소스 프로젝트입니다.

이 프레임워크는 플랫폼 간 JavaScript 소스코드를 공유하는 기반으로 Android 및 iOS 앱을 만드는 데 사용됩니다. React Native 앱을 만들 때 모든 비즈니스 로직, API 호출 및 상태 관리를 JavaScript로 합니다. UI 요소와 그 스타일은 코드에서 일반화되지만 기본 뷰로 렌더링됩니다. 이를 통해 코드의 재사용성을 높은 수준으로 끌어 올리 수 있고, 각 플랫폼의 스타일 가이드 및 모범 사례를 따르는 UI를 사용할 수 있습니다.

또한 React Native를 사용하면 플랫폼 별 코드, 로직, 그리고 스타일을 필요한대로 작성할 수 있습니다. 이는 플랫폼 별 React 구성 요소를 보유하는 것만큼 간단할 수도 있고 React Native 앱에서 플랫폼 별 C Library를 사용하는 것만큼 고급일 수도 있습니다.
### SIMILARITIES TO HYBRID APPS
하이브리드 앱 프레임워크와 마찬가지로 React Native는 진정한 크로스 플랫폼 개발을 가능하게 합니다. Instagram은 React Native 프로젝트에 85–99 %의 코드를 재사용하고 있습니다. 또한 React Native는 많은 웹 개발자가 익숙하게 사용할 수 있는 기술(JavaScript 및 React)을 사용하여 만들어졌습니다. 개발자가 React에 익숙하지 않은 경우 Objective-C 또는 Java를 배우는 것보다 AngularJS, jQuery 또는 vanilla JavaScript에 익숙하면 배우는 것이 훨씬 쉽다는 의미입니다.

또한 React Native 앱 디버깅은 Chrome 브라우저의 개발자 도구를 사용할 수 있고 이는 웹 개발자에게 아주 익숙한 프로세스입니다. 에뮬레이터 또는 실제 기기에서 앱을 구동할 때 Chrome 개발자 도구를 통해서 코드 동작을 모니터링 할 수 있습니다. 추가로 개발자는 필요에 따라 더 많은 Native 디버거를 사용할 수도 있습니다.

<figure>
  <img src="{{ site.url }}/assets/images/2017-08-23/05.png" width="320" />
  <figcaption>iOS React Native debugger window</figcaption>
</figure>

여기에서 주의 깊에 볼만한 점은 React Native가 하이브리드 앱 프레임워크가 해결하려고 하는 핵심 문제를 해결한다는 것입니다.
### FURTHER IMPROVEMENTS OVER HYBRID APPS
하이브리드 앱과 달리 React Native 앱은 웹뷰를 통해서가 아닌, 기기 자체적으로 실행됩니다. 즉, JavaScript 인터프리터와 함께 동작하면서 속도를 저하시킬 수 있는 웹 기반 UI 요소에만 국한되지 않는다는 의미입니다. React Native는 기기 OS의 기본 UI 요소를 렌더링하므로 애플리케이션은 플랫폼에서 더 많은 것을 즉시 사용할 수 있으며, 때문에 사용자가 더 편안하게 사용할 수 있습니다. 또한 네이티브 툴링 및 프로파일링 유틸리티를 보다 완벽하게 사용할 수 있어 React Native는 개발생산성을 높입니다.

아래는 최근 공개된 어느 React Native 앱의 스크린 샷입니다. 이 이미지에서는 이 프레임워크를 사용하여 얻을 수 있는 플랫폼 별 인터페이스를 강조 표시했습니다. 보시다시피 각 앱은 기본지도를 사용하며 각 플랫폼의 디자인 가이드 라인을 따르는 문구가 있습니다. Android에서 설명영역은 지도의 맨 아래에서 위로 올라오는 형식입니다. iOS에서는 말풍선이 지도에서 선택한 요소에 표시되는 형식입니다. 두 애플리케이션에서 동일한 작업을 수행할 수 있으며 대부분의 코드가 공유되지만 플랫폼 별 특성을 각기 잘 나타낼 수 있는 UI를 구현할 수 있습니다.

<div style="display: flex; flex-direction: row;">
  <figure>
    <img src="{{ site.url }}/assets/images/2017-08-23/06.png" width="320" />
    <figcaption>Screenshot of the Vett Local app on iOS</figcaption>
  </figure>
  <figure style="margin-left: 16px;">
    <img src="{{ site.url }}/assets/images/2017-08-23/07.png" width="320" />
    <figcaption>Screenshot of the Vett Local app on Android</figcaption>
  </figure>
</div>

### HOW IS THIS DONE?
아래 샘플 소스가 있습니다. 웹 개발자가 이미 알고 있어야하는 영역을 강조하는 몇 가지 공통 요소를 보여줍니다. 코드 다음에는 각 섹션에서 수행중인 작업에 대한 설명이 나와 있습니다.
{% gist moralmk/b3acbdce8d1e2c5d7b44df4b3024b0d3 %}

위의 코드 대부분은 JavaScript이고 때문에 대다수의 웹 개발자에게 친숙할 것입니다. 렌더링 로직의 대부분은 새로운 것이지만, HTML에서 React Native 뷰로의 마이그레이션은 매우 간단합니다. 또한 스타일 속성은 CSS와 매우 유사합니다.
### WHO IS DOING THIS?
자신의 애플리케이션을 작성하는 방법을 결정할 때 업계 전문가로부터 배우는 것이 중요합니다. 그들은 수억원에 달하는 애플리케이션을 개발하면서 이미 깊이 있는 고민을 선행했을 것이고, 그런 그들을 통해서 우리는 짧은 시간에 실수나 경험을 간접적으로 배울 수 있습니다. Facebook, Instagram, Airbnb, Baidu, Discord, Tencent, Uber 및 Twitter : 앱에서 React Native를 사용하는 대기업들입니다.

이러한 앱의 대부분은 원래 다른 접근 방식을 사용하여 작성되었지만 React Native로 완전히 전환했거나 현재 React Native를 사용하여 기존 네이티브 애플리케이션을 보강하고 있습니다.

이전에는 대개의 기술 변화가 cross-platform에서 platform-specific에 이르기까지 다양했지만, 이제는 많은 프리미어 앱이 React Native를 통해서 크로스 플랫폼 솔루션으로 옮겨갔습니다. 이 변화는 단순히 무시하기에는 매우 의미있는 변화입니다.
<br/>
<br/>

## What Should You Do Now?
더 나은 커리어를 위해 접근 방식을 재고해야하는 뮤지션처럼 모바일 앱 개발자도 지속적으로 기술을 다시 생각해야 합니다. 사용가능한 최상의 옵션을 기반으로 의사결정을 내리고, 본인의 개발친숙도에만 의존하지 않는 것이 중요합니다. 변화를 실행하는 것이 처음에는 불편하고 노력이 요구되지만, 앱 마켓의 소비자들은 계속 발전할 것을 요구합니다.

React Native는 하이브리드 앱의 재사용성과 비용 효율성을 네이티브 앱의 성능과 결합시킨 매우 매력적인 기술입니다. 그것은 앞으로 빠른 속도로 전파될 것으로 예상되며, 다가오는 하이브리드 앱에 대한 대체 접근 방법이 될 것입니다.