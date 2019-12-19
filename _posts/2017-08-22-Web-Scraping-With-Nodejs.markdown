---
layout: post
title:  "Web Scraping With Node.js"
date:   2017-08-22 22:22:22 +0900
categories: nodejs
author: Donghwa Lee
---
번역 원문 :
[https://www.smashingmagazine.com/2015/04/web-scraping-with-nodejs/](https://www.smashingmagazine.com/2015/04/web-scraping-with-nodejs/)
<br/>
<br/>
![Node.js Web Scraping]({{ site.url }}/assets/images/2017-08-22-Web-Scraping-With-Nodejs.png)

Web Scraping은 프로그램을 이용해서 인터넷에서 정보를 검색하는 프로세스입니다. 웹에서 데이터량이 증가함에 따라 이러한 방식이 점차 보편화되고 있습니다. Web Scraping을 간편하게 하기 위해서 여러가지 강력한 서비스들이 등장했습니다. 하지만 대다수의 서비스들은 비용이 고가이거나, 기능이 제한적이거나 등의 단점이 있습니다. 우리는 그러한 서비스들을 이용하지 않고, Node.js를 사용해서 완전히 무료이면서 강력한 웹 스크래퍼를 만들 수 있습니다.

이 글에서는 다음 내용을 다룹니다.

- Web Scraping을 간편하게 하는 Node.js 모듈, Request와 Cheerio

또한 먼저 다음을 진행하기 전에 몇 가지 알아두어야 할 사항이 있습니다. 이 글에서는 Node.js에 대한 기본적인 이해가 필요합니다. 또 Web Scraping은 일부 웹 사이트의 서비스 약관을 위반할 수 있으므로 Scraping을 수행하기 전에 해당 웹 사이트에 문의 혹은 약관을 확인하셔야 합니다.
<br/>
<br/>

## Modules
앞에서 언급 한 Node.js 모듈을 사용하려면 Node Package Manager 인 NPM을 이용합니다. NPM은 Node.js와 함께 자동 설치되는 패키지 관리 유틸리티로 모듈을 간편하게 설치할 수 있도록 도와줍니다. 기본적으로 NPM은 모듈을 node_modules라는 폴더에 설치됩니다.

자, 그럼 본격적으로 시작해볼게요.

### REQUEST
Node.js는 HTTP 및 HTTPS 인터페이스를 통해 인터넷에서 데이터를 다운로드하는 간단한 방법을 제공하지만, Web Scraping으로 작업을 시작할 때 나타나는 리디렉션 및 기타 문제에 대해서는 별도로 처리해야 합니다. Request 모듈을 이용하면 그러한 골치아픈 것들을 따로 처리하지 않을 수 있습니다. 웹 페이지 소스를 메모리로 직접 다운로드합니다. Request 모듈을 설치하려면 프로젝트 디렉토리에서 npm install request를 실행하세요.
### CHEERIO
Cheerio를 사용하면 다운로드한 웹 페이지 소스를 jQuery와 동일한 구문을 사용하여 작업할 수 있습니다. 서버용으로 특별히 설계된 jQuery를 빠르고 유연하게 구현할 수 있고 Parsing보다는 데이터를 직접 다운로드하는데 집중할 수 있습니다. Cheerio 모듈을 설치하려면 프로젝트 디렉토리에서 npm install cheerio를 실행하세요.
<br/>
<br/>

## Implementation
아래 코드는 날씨 웹 사이트에서 온도를 감지할 수 있는 작은 애플리케이션입니다. URL의 끝에 지역번호가 붙는 것을 확인할 수 있고, 이 지역번호에 따라 해당 지역의 날씨정보를 얻을 수 있습니다.

```javascript
var request = require("request");
var cheerio = require("cheerio");
var url = "http://www.wunderground.com/cgi-bin/findweather/getForecast?&query=" + 02888;
  
request(url, function (error, response, body) {
  if (!error) {
    var $ = cheerio.load(body);
    var temperature = $("[data-variable='temperature'] .wx-value").html();
    console.log("It’s " + temperature + " degrees Fahrenheit.");
  } else {
    console.log("We’ve encountered an error: " + error);
  }
});
```
먼저 모듈을 액세스 할 수 있도록 모듈을 선언합니다. 그런 다음 url 변수에 다운로드 할 URL을 정의합니다.

Request 모듈을 사용해서 위에 지정된 URL에서 페이지를 다운로드합니다. Request 함수에 다운로드하고자하는 URL과 요청결과를 처리할 콜백 함수를 전달합니다. 페이지가 다운로드 되면 콜백이 호출되고 오류, 응답 및 본문 세 가지 변수가 전달됩니다. 요청에서 웹 페이지를 다운로드하는 데 문제가 발생하여 데이터를 검색할 수 없는 경우 오류 객체가 함수에 전달되고 본문 변수는 null이 됩니다. 데이터 작업을 시작하기 전에 오류가 없는지 확인합니다. 만약 오류가 있다면, 오류 내용이 무엇인지 볼 수 있도록 로그를 남깁니다.

오류 없이 정상적으로 페이지가 다운로드 되면 데이터를 Cheerio에 전달합니다. 그런 다음 표준 jQuery 구문을 사용하여 다른 웹 페이지처럼 데이터를 처리 할 수 있습니다. 우리가 원하는 데이터를 찾으려면 우리가 관심있는 요소를 페이지에서 가져올 수 있는 선택자(selector)를 알아내야 합니다. Chrome 브라우저에서 이 예제에 사용했던 URL로 이동하여 개발자 도구로 페이지를 탐색하면 선택자를 쉽게 알 수 있습니다. 선택자로부터 데이터를 가져와 콘솔에 기록하는 것은 간단합니다.

### IN YOUR BROWSER
1. 브라우저에서 스크랩하려는 페이지를 방문하고 URL을 기록합니다.
2. 데이터가 필요한 요소를 찾아 jQuery 선택자를 찾습니다.

### IN YOUR CODE
1. Request 모듈을 사용하여 URL에 페이지를 다운로드합니다.
2. 다운로드 된 데이터를 Cheerio에 전달하면 jQuery와 같은 인터페이스를 얻을 수 있습니다.
3. 미리 알아둔 선택기를 사용하여 페이지에서 데이터를 스크랩합니다.
<br/>
<br/>

## 추가정보 : Data Mining
데이터 마이닝은 Web Scraping의 고급 사용 사례입니다. 데이터 마이닝은 많은 웹 페이지를 다운로드하고 웹 페이지에서 추출된 데이터를 기반으로 보고서를 생성하는 작업입니다. Node.js는 이러한 성격의 애플리케이션에 적합합니다.

위에서 언급한 두 라이브러리를 보다 깊이 있게사용하는 방법을 보여주기 위해 Node.js에 100줄 미만의 작은 데이터 마이닝 프로그램을 작성했습니다. 이 앱은 Google 검색의 첫 페이지에 링크된 각 페이지의 텍스트를 분석하여 특정 Google 검색과 관련된 가장 인기있는 용어를 찾습니다.

이 앱에는 세 가지 주요 단계가 있습니다.

1. Google에서 검색합니다.
2. 모든 페이지를 다운로드하고 각 페이지의 모든 텍스트를 분석합니다.
3. 텍스트를 분석해서 가장 인기있는 단어를 제시합니다.
우리는 이러한 각각의 일이 일어나는데 필요한 코드를 간략하게 살펴볼 것입니다.

### DOWNLOADING THE GOOGLE SEARCH
우리가 해야할 첫 번째 일은 분석할 페이지를 찾는 것입니다. Google 검색에서 가져온 페이지를 보고 있기 때문에 원하는 검색을 위한 URL을 찾고 다운로드하고 결과를 분석해서 필요한 URL을 찾을 수 있습니다.

위의 예제에서처럼 Request를 사용하는 페이지를 다운로드하고 분석하기 위해 Cheerio를 다시 사용하겠습니다. 코드는 다음과 같습니다.

```javascript
request(url, function (error, response, body) {
  if (error) {
    console.log(“Couldn’t get page because of error: “ + error);
    return;
  }
  
  // load the body of the page into Cheerio so we can traverse the DOM
  var $ = cheerio.load(body);
  var links = $(".r a");
    
  links.each(function (i, link) {
    // get the href attribute of each link
    var url = $(link).attr("href");
    
    // strip out unnecessary junk
    url = url.replace("/url?q=", "").split("&")[0];
    
    if (url.charAt(0) === "/") {
      return;
    }
    
    // this link counts as a result, so increment results
    totalResults++;
  }
}
```

이 경우 전달할 URL 변수는 Google에서 ‘Data Ming’이라는 용어를 검색한 것입니다.

보시다시피 우리는 먼저 페이지 내용을 요청합니다. 그런 다음 페이지의 내용을 Cheerio에로드하여 관련 결과에 대한 링크가 있는 요소를 DOM으로 얻을 수 있습니다. 그런 다음 링크를 반복하고 Google에서 자체적으로 삽입하는 추가 URL 매개 변수를 제거합니다. Request 모듈을 사용하여 페이지를 다운로드 할 때 추가 매개 변수는 필요하지 않습니다.

마지막으로 모든 작업을 완료하면 URL이 /로 시작하지 않는지 확인합니다. 그렇다면 Google의 다른 URL에 대한 내부 링크이므로 다운로드를 하지 않습니다.

### PULLING THE WORDS FROM EACH PAGE
이제 우리 페이지의 URL을 얻었으므로 각 페이지에서 단어를 가져와야 합니다. 이 단계는 위에서 수행한 것과 거의 동일한 작업을 수행하는 것으로 구성됩니다. 이 경우 URL 변수는 위 반복구문에서 찾은, 처리된 페이지의 URL을 참조합니다.

```javascript
request(url, function (error, response, body) {
  // load the page into Cheerio
  var $page = cheerio.load(body);
  var text = $page("body").text();
}
```

다시 말하지만 Request와 Cheerio를 사용하여 페이지를 다운로드하고, DOM에 접근할 수 있습니다. 여기에서는 페이지의 텍스트 만 가져옵니다.

다음으로 페이지의 텍스트를 정리해야 합니다. 여분의 공백, 스타일, 때로는 JSON 데이터의 홀수 비트 등 유의미하지 않은 데이터들을 분별해야 합니다.

1. 모든 공백을 단일 공백으로 압축합니다.
2. 글자나 공백이 아닌 글자를 버립니다.
3. 모든 것을 소문자로 변환합니다.

일단 우리가 텍스트를 공백으로 나누면 페이지에 렝더링된 모든 단어가 들어있는 배열을 얻을 수 있습니다. 그런 다음 루프를 반복하여 변수 ‘corpus’에 추가할 수 있습니다.

코드로 보자면 다음과 같습니다.

```javascript
// Throw away extra white space and non-alphanumeric characters.
text = text.replace(/\s+/g, " ")
       .replace(/[^a-zA-Z ]/g, "")
       .toLowerCase();

// Split on spaces for a list of all the words on that page and loop through that list.
text.split(" ").forEach(function (word) {
  // We don't want to include very short or long words because they're probably bad data.
  if (word.length > 20) {
    return;
  }
        
  if (corpus[word]) {
    // If this word is already in our corpus, our collection of terms, increase the count for appearances of that word by one.
    corpus[word]++;
  } else {
    // Otherwise, say that we've found one of that word so far.
    corpus[word] = 1;
  }
});
```

### ANALYZING OUR WORDS
일단 모든 단어들을 변수 ‘corpus’에 데이터로 갖게 되면, 그것을 반복해서 인기에 따라 분류할 수 있습니다. 먼저 corpus가 객체이기 때문에 배열로 가공하겠습니다.

```javascript
// stick all words in an array
for (prop in corpus) {
  words.push({
    word: prop,
    count: corpus[prop]
  });
}
  
// sort array based on how often they occur
words.sort(function (a, b) {
  return b.count - a.count;
});
```

결과는 Google 검색 결과의 첫 페이지에 있는 모든 웹 사이트에서 각 단어가 얼마나 자주 사용되었는지를 나타내는 정렬된 배열입니다. 아래는 ‘Data Mining’이라는 검색어에 대한 결과 예시입니다.

```javascript
[
  { word: 'data', count: 981 },
  { word: 'mining', count: 531 },
  { word: 'that', count: 187 },
  { word: 'analysis', count: 120 },
  { word: 'information', count: 113 },
  { word: 'from', count: 102 },
  { word: 'this', count: 97 },
  { word: 'with', count: 92 },
  { word: 'software', count: 81 },
  { word: 'knowledge', count: 79 },
  { word: 'used', count: 78 },
  { word: 'patterns', count: 72 },
  { word: 'learning', count: 70 },
  { word: 'example', count: 70 },
  { word: 'which', count: 69 },
  { word: 'more', count: 68 },
  { word: 'discovery', count: 67 },
  { word: 'such', count: 67 },
  { word: 'techniques', count: 66 },
  { word: 'process', count: 59 }
]
```

앞으로 이 애플리케이션을 한 단계 업그레이드 할 수도 있겠습니다. 텍스트 파싱을 최적화하고, 검색 결과를 Google 결과의 여러 페이지로 확장하고, 핵심 용어가 아닌 일반적인 단어들은 제거할 수도 있습니다.