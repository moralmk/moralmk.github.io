---
layout: post
title:  "Node.js with Express was pretty good."
date:   2019-12-19 11:28:03 +0900
categories: nodejs
author: Donghwa Lee
---
올해 1월 개인 비즈니스로 하는 프로젝트에서 10만 이상 유저가 사용하는 모바일 애플리케이션을 론칭했었는데요. Frontend는 React Native, 그리고 Backend는 Node.js + Express로 구성했었습니다. **Node.js + Express로 구성하게 되는데 주요했던 요인**들을 공유해보려고 합니다.

![Node.js + Express]({{ site.base_url }}/assets/images/2019-12-19-Nodejs-with-Express-was-pretty-good.png){: .callout}

## 생산성
개인적인 욕심에서 Frontend는 반드시 React Native로 한다는 전제가 있었습니다. 때문에 당장 아래 두 가지는 Backend로 Node.js를 선택하는데 크게 작용했었습니다.
- Frontend/Backend 모두 JavaScript로 개발할 수 있으니 멤버들이 full-stack 개발을 경험할 수 있다는 점
- 역시 프로젝트를 JavaScript로만 진행할 수 있으니 빠르고, 효과적이고, 다른 시너지도 기대할 수 있다는 점

물론 기대는 예상하던 성과로 나타났습니다. 👍 물리적으로 Frontend/Backend 서로가 구분은 되었지만, **Refactoring, Trouble shooting 등의 실무에서 역할의 경계가 눈에 띄게 사라졌고,** 덕분에 시간이라는 가장 비싼 리소스를 아낄 수 있었습니다. 이로 인해서 차후에는 프로젝트 전체 비용도 더 효율화 시킬 수 있을 것이라는 다음 단계의 기대도 해볼 수 있었고요. 😃
<br/>
<br/>

## 성능
Node.js의 성능에 대해서는 의심의 여지가 없었습니다. 과거의 개인 프로젝트에서 부터 Node.js + Express 조합으로 개발과 운영을 경험하면서 production에서도 충분히 신뢰할 수 있다는 믿음이 있었는데요. 특히 **해당 프로젝트의 서비스는 B2C 멤버십 서비스로 유저에게 실시간 처리를 제공해야 한다는 점, 타사 멤버십 core 시스템과 긴밀하게 상호작용 해야한다는 점**은 Node.js가 아니어야 하는 이유를 찾기 어려웠습니다.

가볍고, 그래서 빠르고, 많은 양의 동시 연결을 처리할 수 있어 실시간 처리에 탁월하고 등등... 구체적인 수치들을 근거로 공유할 수 있다면 좋겠지만 그럴 수가 없어 아쉽네요. 😅 다만 Walmart, Ebay, Uber 등 다수의 IT 자이언트들이 그들의 서버사이드에 Node.js를 사용하고 있다고 하니, 성능은 더 말해봐야 무슨 소용이 있나요.

포스팅을 위해 관련 내용을 더 조사하다가 새롭게 알게된 사실로, [NASA](https://www.nasa.gov/)에서도 자체 End-to-end 데이터 시스템에 Node.js를 사용[[참고]](https://foundation.nodejs.org/wp-content/uploads/sites/50/2017/09/Node_CaseStudy_Nasa_FNL.pdf)한다고 하니 더(x2) 말해봐야 무슨 소용이 있나요.
<br/>
<br/>

## 건강한 커뮤니티
Express는 Node.js 프레임워크 중에 가장 유명하고, 그래서 가장 큰 오픈소스 커뮤니티가 운영되고 있습니다. 개발 뿐만이 아니라 향후 운영까지 고려해야 하는 프로젝트였기에 **기반 기술들이 앞으로 얼마나 안정적이고 지속적으로 support 될 수 있는가는 선택 기준에 매우 중요한 포인트**가 되었습니다. 그렇기 때문에 다수의 프레임워크 중에서 Express를 선택해내는 과정은 전혀 어렵지 않았었네요. 문서화된 자료나 구글링 되는 결과가 풍부하다는 점도 마음 한 구석이 든든해지게 했었구요.
