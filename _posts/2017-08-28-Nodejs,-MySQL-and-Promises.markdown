---
layout: post
title:  "Node.js, MySQL and Promises"
date:   2017-08-28 22:22:22 +0900
categories: nodejs
author: Donghwa Lee
---
번역 원문 :
[https://codeburst.io/node-js-mysql-and-promises-4c3be599909b](https://codeburst.io/node-js-mysql-and-promises-4c3be599909b)
<br/>
<br/>
![Node.js Promises]({{ site.url }}/assets/images/2017-08-28-Nodejs,-MySQL-and-Promises.jpg)

Node.js에서 데이터베이스 액세스는 대부분의 I/O 작업과 마찬가지로 비동기로 작동합니다. 결과를 기다리는 동안 다른 작업을 수행할 수 있기 때문에 매우 매력적인 기능입니다. 그러나 이 기능은 다른 프로그래밍 언어를 사용한다면 정말 짜증납니다.

PHP로는 다음과 같이 작성할 수 있습니다.

```php
$results = $connection -> query('SELECT * FROM some_table');
// the following code is executed after the query is executed
```

물론 query() 메서드는 실행하는데 약간의 시간이 걸릴 수 있지만 개발자의 관점에서는 큰 문제가 되지 않습니다. SQL 쿼리를 실행해서 결과를 반환하는 단일 연산으로 작동합니다.

Node.js에서는 다음과 같이 작성해야 합니다.

```javascript
connection.query('SELECT * FROM some_table', (err, rows) => {
  // do something with the results here
});
// the following code is executed *before* the query is executed
```

예에서는 MySQL 클라이언트 라이브러리를 사용하고 있지만, no-SQL 엔진을 포함한 다른 모든 데이터베이스에서도 마찬가지입니다. 🙂

일단 위의 예는 그리 나쁘지 않습니다. 그러나 몇 가지 쿼리를 순차적으로 수행해야한다고 가정해볼까요? 마지막에는 비동기 작업이기도 한 데이터베이스 연결을 끊는 작업까지 한다면 아래와 같습니다.

```javascript
connection.query('SELECT * FROM some_table', (err, rows) => {
  connection.query('SELECT * FROM other_table', (err, rows2) => {
    connection.close(err => {
      // ... do something with all the results
    }
  }
}
```

이런 방식으로 10개의 중첩된 쿼리가 있다고 상상해보세요. 그리고 각각의 쿼리 블락에서 오류 처리를 다루어야 합니다. 어느 레벨에서 오류가 발생하더라도 데이터베이스 연결이 정상적으로 닫히는지 확인해야 합니다.

이러한 작업은 위와 같은 방식으로 쓰는 것이 매우 어렵습니다. 중간에 또 다른 쿼리를 삽입해야하는 경우 수정하기도 어렵습니다. 그리고 무엇보다 소스코드를 읽고 이해하는데 큰 어려움을 줍니다.
<br/>
<br/>

## Using promises
Promises가 이러한 문제들을 해결할 수 있습니다. Promise 개념이 익숙하지 않다면 사전에 소개를 읽는 것이 좋습니다. (예 : 여기 또는 여기) 저는 순차적인 데이터베이스 쿼리 수행에 있어서 Promise의 실제적인 사용법을 보여주고자 합니다. 그래서 저는 일단 당신이 기본적인 개념에 대해서는 이미 알고 있다고 가정하겠습니다.

먼저 데이터베이스 클라이언트를 ‘Promisfy’ 해야 합니다. 수동으로 할 필요는 없습니다. 여기에 설명된 것과 같이 자동화 도구를 사용할 수도 있지만 MySQL 클라이언트에 대한 Wrapper 클래스를 만드는 것은 매우 간단합니다.
{% gist moralmk/fac720c09c7ca382067b30ad030d0048 usingPromises.js %}

생성자는 createConnection()으로 간단하게 MySQL에 연결합니다. 선언 시점에 연결이 되지 않고 첫 번째 쿼리가 실행될 때 자동으로 연결됩니다. 그래서 연결을 만드는 것이 비동기 작업이 아닙니다.

query() 메서드는 SQL 문자열과 쿼리에 전달할 매개 변수의 선택적 배열을 사용합니다. 그리고 Promise 객체를 리턴합니다. Promise는 쿼리가 실행을 끝내면 ‘reslove’ 되고, 쿼리수행 결과는 Promise의 결과가 됩니다. 오류가 발생하면 약속은 ‘reject’ 됩니다.

close() 메서드도 유사합니다. 데이터베이스 연결이 닫힐 때 Promise는 ‘resolve’ 됩니다. 결과는 없습니다.
query() 메서드는 여전히 쿼리가 실행되기 전에 즉시 반환됩니다. 결과를 얻으려면 반환된 Promise의 then() 메서드를 호출하고, 쿼리 실행이 끝날 때 호출될 callback 함수를 지정해야 합니다.

새로운 Database 클래스는 다음과 같은 방식으로 사용할 수 있습니다.

```javscript
database.query('SELECT * FROM some_table').then(rows => {
  // do something with the result
});
// the following code is executed *before* the query is executed
```

위 코드는 첫 번째 예제와 거의 같습니다. 그러나 callback과 달리 Promise는 매우 쉽게 연결될 수 있습니다. 몇 가지 쿼리를 순차적으로 수행하고 마지막으로 연결을 닫으려면 다음과 같이 할 수 있습니다.

```javascript
database.query('SELECT * FROM some_table')
  .then(rows => database.query('SELECT * FROM other_table'))
  .then(rows => database.close());
```

이것은 훨씬 더 가독성이 높고, 필요한 경우 쉽게 수정하고, 확장할 수 있습니다. 그러나 이 방법에는 여전히 두 가지 문제점이 있습니다.
<br/>
<br/>

## Extracting the results
첫 번째 문제는 각 callback 함수에서 마지막 쿼리의 결과만을 액세스 할 수 있다는 것입니다. 따라서 두 쿼리의 결과를 이용해서 무언가를 가공하고 싶다면 로컬 변수에 저장해야 합니다.
{% gist moralmk/fac720c09c7ca382067b30ad030d0048 extracting.js %}

쿼리들의 결과를 다음 then()에서 사용하려면 함수가 query() 메서드에서 Promise를 반환해야 합니다. 만약 return 키워드를 쓰지 않는다면 다음의 then() 메서드에서 이전 쿼리의 결과는 undefined 입니다.
<br/>
<br/>

## Error handling and closing connection
또 우리는 오류를 처리하는 것이 필요합니다. Promise 내 작업에서 오류가 발생하고 이 오류를 catch 하지 않으면 프로그램은 중단되게 됩니다.

Promise를 사용하면 체인의 끝에 하나의 catch() 함수를 추가하는 것만으로 충분합니다. 모든 단계 어디에서라도 오류가 발생하면 이후의 모든 then() 메서드는 실행이 생략되고 catch() 메서드가 실행됩니다. 이는 try/catch 블록과 매우 유사합니다.

이 솔루션의 문제점은 오류가 발생하면 데이터베이스 연결이 끊어지지 않는다는 것입니다. 동기식 프로그램에서는 try/catch 블록에 finally 절을 추가해서 이를 방지할 수 있지만, 아쉽게도 JavaScript Promise에는 finally() 메서드가 없습니다.

오류가 발생하더라도 데이터베이스 연결이 잘 닫히도록 하려면 다음과 같이 쓸 수 있습니다.
{% gist moralmk/fac720c09c7ca382067b30ad030d0048 errorHandling.js %}

then()에 전달된 두 번째 함수(굵은 글꼴로 표시)는 체인의 이전 단계에서 오류가 발생되면 호출됩니다. 그럼 여기에서 데이터베이스 연결을 닫은 다음 오류를 다시 throw하여 최종적으로 catch()에 도달하게 합니다.

이 패턴을 자주 사용하는 경우 다음과 같이 별도의 함수로 연결을 만들고 닫을 수 있습니다.
{% gist moralmk/fac720c09c7ca382067b30ad030d0048 dbExecute.js %}

다음은 위 함수를 사용하여 다시 작성한 내용입니다.
{% gist moralmk/fac720c09c7ca382067b30ad030d0048 final.js %}

비슷한 기술을 사용하여 트랜잭션을 래핑할 수 있습니다. 트랜잭션은 모든 쿼리가 성공적으로 실행되거나 중간에 오류가 발생하면 rollback 될 때 자동으로 commit 합니다.
<br/>
<br/>

## Final notes
Promise는 까다롭고 익숙해지기까지 시간이 걸릴 수 있습니다. 그러나 실제로 비동기 코드는 항상 까다롭습니다. Promise는 callback 보다 작성하고 예상하는 것이 쉽습니다. 만약 제 말을 믿지 못한다면, ‘callback hell’로 검색을 해보셔도 좋습니다. 🙂

Promise 보다 비동기 코드를 쉽게 작성하게 하는 새로운 방법으로 async/await 키워드를 사용하는 것입니다. 저는 이것을 C#에서 얼마동안 사용해왔고, 정말 좋아합니다. Node.js 6에서는 지원되지 않지만 Node.js 8 또는 Babel로 사용할 수 있습니다. 하지만 그건 다른 글에서 다루겠습니다.
