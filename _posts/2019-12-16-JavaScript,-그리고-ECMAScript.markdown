---
layout: post
title:  "JavaScript, 그리고 ECMAScript"
date:   2019-12-16 09:45:01 +0900
categories: es
---
# **JavaScript의 Java는 대체 왜?**
JavaScript의 **Java**는 우리가 흔히 아는 Java와 전혀 상관이 없습니다. 1995년 당시 Java의 인기를 얻어 걸린 듯 같이 한번 누려보겠다는 일종의 마케팅 꼼수에서 생겨난 이름입니다.

>열흘 내로 브라우저에서 스킴(함수형 프로그래밍 언어)이 동작하는 것을 보여주겠다.

1995년 5월, [브렌던 아이크(Brendan Eich, 1961)](https://en.wikipedia.org/wiki/Brendan_Eich)는 위와 같은 입사조건으로 Netscape에서 일하기 시작했고, 정말 단 10일 만에 브라우저에서 동작하는 언어를 만들었습니다.

Netscape의 설립자 [마크 엔드리슨(Marc Andreessen, 1971)](https://en.wikipedia.org/wiki/Marc_Andreessen)은 이 언어에 잠시 *Mocha*라는 이름을 붙였고, 4개월 후인 9월 [Netscape Navigator 2](https://en.wikipedia.org/wiki/Netscape_Navigator_2)에 *LiveScript*라는 이름으로 등장하였습니다. 같은 해 말 Netspace에서는 다시 한번 이 언어의 이름을 바꾸고자 했고, 당시 Sun Microsystems(현 Oracle)에서 소유하고 있던 JavaScript 상표의 라이선스를 12월에 획득한 후, 최종적으로 지금의 **JavaScript**가 되었습니다.
<br/>
<br/>
# **JavaScript, 그리고 ECMAScript**
Netscape는 JavaScript를 지속적으로 발전시켜 나가기 위해 1996년 이를 ECMA에 공유하고, 표준으로 자리잡게 하기 위한 작업에 기여했습니다. 당시 Microsoft의 Internet Explorer 3에도 *JScript*라는 언어가 탑재되었는데, 이것이 JavsScript와 매우 유사하였고, Netscape는 이에 자극을 받아 표준화를 위한 공개를 결정했을 것이라는 주장이 있기도 합니다.

아무튼 그 뒤 1997년 6월 *ECMAScript* 라는 이름으로 공식 표준안이 수립되었고, JavaScript는 이렇게 스스로 ECMAScript의 Netscape용 방언이 되었습니다. 방언이라지만 출신이 다른 만큼 ECMAScript 표준을 가장 충실하게 구현한 언어입니다. 이후 이 표준안을 기반으로 다수의 방언들이 등장하게 되었고, 그 중 하나가 당시 Macromedia의 Flash(지금은 Adobe의 Flash)에 탑재된 ActionScript가 되겠네요.
<br/>
<br/>
# **ECMAScript의 줄임말 'ES', ES 버전**
**ES**는 ECMAScript의 줄임말입니다. ES는 바로 뒤에 따라오는 숫자와 함께 각 버전을 의미합니다. 1997년도 부터 1999년 까지 매해 ES1, 2, 3가 차례대로 발표되었고, ES4는 많은 우여곡절로 인해 발표가 되지 않습니다. 이후 10년의 공백기간이 있었고, 2009년도 12월에 ES5가 발표되었습니다.

ES6는 6년 후 2015년도 6월에 발표됩니다. 이 때부터 커미티에서는 ECMAScript 버전을 연단위로 발표하기로 결정하였고, 그러한 변화에 따라 ES6는 **ES2015**로 쓰여지게 되었습니다. 그에 따라 지금까지 매해 새로운 버전이 발표되고 있고, 이 글을 작성하는 2019년 12월 현재는 *ES2019(ES10)*까지 발표되어 있습니다.
