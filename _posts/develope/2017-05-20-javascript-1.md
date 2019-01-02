---
layout: amp
title: "자바스크립트 this (1)"
description: "자바스크립트 this 용법 알기"
tag: [javascript]
category: develope
sitemap:
  changefreq: daily
---

# 💁🏻 들어가기
자바스크립트 this의 용법에 대해서 알아보겠습니다.


# 목차
- this? this!
- 함수 실행:
  - 함수 실행에서의 this
  - 엄격 모드 함수 실행에서의 this
  - 내부 함수에서 this를 사용할 때 실수하는 부분
- 메소드 실행
  - 메소드 실행에서의 this
  - 객체로부터 메소드를 분리할 때
- 생성자 실행
  - 생성자 실행에서의 this
  - new를 깜빡할 때
- 간접 실행
  - 간접 실행에서의 this
- 바인딩 함수
  - 바인딩 함수에서의 this
- 화살표 함수
  - 화살표 함수에서의 this
  - 화살표 함수로 메소드를 정의할 때 실수

# 1. this? this!
`javascript`에서 4가지 함수 실행 타입이 있다.

- 함수 실행 : alert('Hello World')
- 메소드 실행 : console.log('Hello World')
- 생성자 실행 : new RegExp('\d')
- 간접 실행 : alert.call(undefined, 'Hello World')

각 타입은 서로 다른 문맥을 갖는다.
`this`키워드를 이해할 수 있는 방법은 함수 실행이 문맥에 어떤 영향을 미치는지에 대해 확실히 이해하는 것이다. 시작하기 전에 아래의 용어들과 친숙해지자.

<pre>
- 실행이란, 함수 내부에 있는 코드를 수행하는 것 = 함수호출
- 실행 시점에서의 문맥은 함수 내부에서의 값
- 함수의 스코프는 변수, 객체, 내부 함수들의 집합
</pre>


# 2. 함수 실행
함수 표현식은 { 인자1, 인자2, ... }로 수행된다.
ex. parseInt('18')
이 표현식은 myObject.myFunction과 같이 메소드를 실행하기 위해 사용하는 속성 접근자가 될 수 없다. 예를 들어 [1,5].join(',')은 함수 실행이 아니라 메소드 호출이다.

```javascript
function hello(name){
  return 'Hello' + name + '!';
}
var msg = hello('World'); //함수실행
console.log(msg); // => 'Hello World!'
```
`hello('World')`가 함수를 실행하는 부분이다. `hello`표현식 뒤에 따라오는 `World`인자와 함께 함수 객체로 계산된 것이다.

⚠️ 즉시실행함수(IIFE)
```javascript
var message = (function(name){
    return 'Hello' + name + '!';
  })('World');
  console.log(message) //=> 'Hello World'!
```

즉시실행함수 역시 함수 실행의 종류 중 하나다.
```javascript
(function(name){
    return 'Hello' + name + '!';
  }) /*=> 함수 객체로 바뀔 표현식 */ ('World'); //=> 함수에 전달될 인자
```

# 2.1. 함수 실행에서의 this
함수 실행에서 `this`는 **전역객체**다.
**전역객체**는 실행 환경에 따라 결정 되며 웹 브라우저에서 `window` 객체가 전역객체가 된다.
```javascript
function sum(a,b){
console.log(this === window); // => true
this.myNumber = 20; // 전역객체에 'myNumber' 속성 추가
return a + b;
}
sum(15, 16); // => 31
window.myNumber; // => 20
```

sum(15, 16) 함수가 실행됨과 동시에 자바스크립트는 자동으로 `this`를 전역객체로 갖는다. 웹 브라우저 환경에서 `this`는 `window`이다. `this`가 함수 스코프~전역실행문맥~ 바깥에서 사용 되었을 경우 전역객체를 참조하게 된다.

# 2.2. 엄격모드 함수 실행에서의 this
엄격모드 함수 실행의 `this`는 **undefined**다.
엄격모드는 `코드 안정성` 그리고 `더 나은 오류검증 제공`을 위해 ECMA Script 5.1버전에서 처음 소개되었다. 엄격모드로 작성하는 방법은 **함수 내부 최상단**에 `use strick`라는 예약어를 적으면 된다.

```javascript
function multiply(a, b){
  'use strict';

  console.log(this === undefined); // => true
  return a * b;
}
multiply(2, 5); // => 10
```
엄격모드는 현재 스코프뿐만 아니라 내부에 정의된 모든 스코프에서도 적용된다.

{% highlight javascript linenos %}
{% raw %}
function execute(){
  'use strict';

  function concat(str1, str2){
    console.log(this === undefined); // => true
    return str1 + str2;
  }
  concat('Hello', 'World'); // => Hello World!
}
execute();
{% endraw %}
{% endhighlight %}

'use strict'는 최상단에 위치하고, 해당 스코프에 엄격모드를 실행해준다.
`4~7`라인에 `concat()`도 `use strict`를 상속받아서 엄격모드를 실행한다.
그리고, `concat('Hello', 'World!')` 실행은 `this`를 undefined로 만든다.

⚠️스코프마다 엄격모드, 비엄격모드 각 각 가능함.

```javascript
function nonStrictSum(a, b) {
  // 비엄격모드 : 전역객체 = window

  console.log(this === window); // => true
  return a + b;
}
function strictSum(a, b) {
  'use strict'; // 엄격모드 : 전역객체 = undefined

  console.log(this === undefined); // => true
  return a + b;
}
nonStrictSum(5, 6); // => 11
strictSum(8, 12); // => 20
```

# 2.3. 내부 함수에서 this를 사용할 때 실수하는 부분
함수를 호출할 때 흔히 하는 실수가 `외부함수의 this`와 `내부함수의 this`를 동일하게 생각하는 것이다. 사실, 내부함수의 문맥은 외부함수의 문맥에 의존되는게 아니라 오직 실행 환경에 좌우된다. 실수한 예제를 살펴보고 무엇이 잘못된건지 알아보자.
```javascript
var numbers = {
  numberA: 5,
  numberB: 10,
  sum: function(){
    console.log(this === numbers); // => true
    function calculate(){
      // this는 window (엄격모드였다면 undefined)
      console.log(this === numbers); // => 💥false
      return this.numberA + this.numberB;
    }
    return calculate();
  }
};
numbers.sum(); // NaN (엄격모드였다면 TypeError)
```
`numbers.sum()`은 객체 내의 **메소드**를 실행하는 것이므로 `sum메소드`내의 문맥ㅇ은 `var numbers`객체이다.  그리고, `calculate()`함수는 sum 내부에 정의되어 있다. 여기서 'calculate()함수 스코프 안에 있는 this도 numbers객체를 상속받았겠지?!'하고 <u>착각</u>하는 경우가 많다.
그러나, **`calculate()`함수는 메소드가 아니기 때문에 그렇기 때문에 전역변수가 `window`가 되는 것**이다(엄격모드였다면 undefined).
결과적으로 `calculate()`함수는 제대로 실행되지 않았기 때문에 15라는 값이 나오지 않았다.

## 🤷🏻‍ 엥? 헐! 그렇다면 어떻게 해야지 함수도 메소드와 동일한 context가 될 수 있을까?
해결책 중 하나는 바로 `.call`메소드를 사용하는 것이다.s
`calculate()`함수에 `.call`메소드를 사용하면 nmuberA와 numberB 속성에 접근할 수 있다.
```javascript
var numbers = {
  numberA: 5,
  numberB: 10,
  sum: function(){
    console.log(this === numbers); // => true
    function calculate(){
      // this는 window (엄격모드였다면 undefined)
      console.log(this === numbers); // => true
      return this.numberA + this.numberB;
    }
    🌟return calculate.call(this);🌟 // => 문맥을 수정하기 위해 .call()메소드를 적용
  }
};
numbers.sum(); // => 15
```
`calculate.call(this)`를 하게되면 this.numberA + this.numberB는 numbers.numberA + numbers.numberB와 동일하게 되서 결과값을 출력할 수 있다.

# 3. 메소드 실행
메소드는 객체의 속성으로 있는 함수이다.
예를 들어
```javascript
var myObject = {
  helloFunction: function() {
    return 'Hello World!';
  }
};
var message = myObject.helloFunction();
```
`.helloFunction()`메소드는 `myObject`의 메소드이다.
메소드에 접근하기 위해서는 `myObject.helloFunction`과 같은 속성 접근자를 이용하면 된다.
메소드 실행은 속성 접근자 형태의 표현식이 함수 객체로 계산되면서 실행된다. 이 표현식은 함수와 마찬가지로 {인자1,인자2,...}의 구조이다.
위의 예제를 해석하면 이렇게 된다 :
  > myObject라는 객체의 helloFunction이라는 메소드 실행

# 3.1. 메소드 실행에서의 this
`this`는 메소드 실행에서 메소드를 소유하고 있는 객체이다.
객체 내에 있는 메소드를 실행할 때, 여기서의 this = 객체 자신이다.
```javascript
var calc = {
  num: 0,
  increment: function() {
    console.log(this === calc); // => true
    this.num += 1; // => num + 1
    return this.num;
  }
};
calc.increment(); // => 1
calc.increment(); // => 2
```
`calc.increment()`메소드 호출은 `increment()`함수의 문맥(=context)를 calc 객체로 만들어준다. 그래서 this.num은 전역객체인 `calc`를 참조로 num의 속성을 증가시키는 것이 가능하도록 해준다. 자바스크립트 객체는 프로토타입에 있는 메소드를 상속받는다. 상속받은 메소드를 객체 내에서 실행한다면 메소드의 문맥은 객체 자신을 가리키게 된다.
```javascript
var myDog = Object.create({
  sayName: function() {
    console.log(this === myDog); // => true
    return this.name;
  }
});
myDog.name = 'Milo';
myDog.sayName(); // => Milo
```
Object.create()는 myDog라는 새로운 객체를 만들고, 프로토타입을 설정한다.
myDog객체는 sayName이라는 메소드를 상속받는다.
myDog.sayName()이 실행될 때, myDog가 실행 문맥이다.
```javascript
class Planet {
  constructor(name) {
    this.name = name;
  }
  getName() {
    console.log(this == earth); // => true
    return this.name;
  }
}
var earth = new Planet('Earth');
earth.getName(); // => Earth
```
ECMAScript 6의 `class`예약어에서 메소드 실행 문맥은 위와 마찬가지로 인스턴스 자신을 가리킨다.

# 3.2. 실수:객체로부터 메소드를 분리할 때

객체 내에 있는 메소드는 별도로 변수로 분리할 수 있다.
이 변수를 통해 메소드를 호출할 때 여기서의 `this`가 메소드가 정의되어있는 객체라고 생각할 수 있으나 사실 객체 밖에 있는 메소드를 호출할 경우 함수 실행을 한 결과와 같다.
함수실행을 할 경우 `this`는 전역객체인 window를 가르킨다. .bind() 바인딩 함수를 사용해서 문맥을 수정할 경우 메소드를 객체에 포함시킬 수 있다.

```javascript
function Animal(type, lefg){
this.type = type;
this.lefg = legs;
this.logInfo = function() {
    console.log(this === myCat);
    console.log('The ' + this.type + ' has' + this.legs + ' legs');
  }
}
var myCat = new Animal('Cat', 4);
setTimeout(myCat.logInfo, 1000);
)
```
에러다. 제대로 출력되려면 .bind()메소드를 사용해야 되는 것!

```javascript
setTimeout(myCat.logInfo.bind(myCat), 1000);
```
myCat.logInfo.bind(myCat)은 객체의 메소드가 logInfo라는 새로운 함수로 실행된다. 하지만 바인딩 메소드로 인해서 this가 window가 아니라 myCat을 가르키게 된다.
