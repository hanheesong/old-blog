---
layout: amp
title: "웹 저장소 API: 브라우저에 데이터 저장해보기 예제"
description: "웹 저장소 API: 브라우저에 데이터 저장하기"
tag: [API, jquery, json, javascript]
category: develope
sitemap:
  changefreq: daily
---

## 들어가기
HTML5 저장소라고 불리는 웹 저장소는 브라우저 내에 데이터를 저장하기 위한 공간임.
저장소는 크게 **로컬저장소** , **세션저장소**가 이쑴.

## 저장소 API에 액세스하기
HTML5 이전엔 브라우저에 정보 저장하기 위한 매커니즘으로 쿠키를 씀.
근데 쿠키는 많은 데이터 양 저장 안되고~ 동일한 도메인에 페이지 요청할 때마다 서버로 함께 전송되고~ 보안도 취약하고~ 그래서 안씀.

HTML5는 저장소 객체를 정의하고 있는데 저장소 객체는 `localStorage객체`와 `sessionStorage객체`가 있음.
둘다 똑같은 메소드를 쓰는데 다른점은 데이터를 저장하는 기간이랑 모든 탭들이 저장된 데이터를 공유할 수 있는가임.

로컬스토리지같은 경우는 창,탭 닫아도 데이터 보존 됨 그리고 열려 있는 모든 창,탭이 서로 데이터를 공유할 수 있는데 반면 세션스토리지는 안됨.

일반적으로 브라우저 저장소 객체는 도메인당 5MB공간을 줌.
데이터 저장소는 객체의 속성으로 저장되고 값은 문자열로 표현됨.
웹사이트는 저장소에 저장된 객체를 보호하려고 오리진 정책을 적용하고 있음.

## 저장소 API에 액세스하기
앞에 말한 로컬스토리지랑 세션스토리지는 `window객체`에 구현되서 메서드 앞에 뭘 붙이지 않아도됨.

저장소 객체에 데이터 저장이면 `setItem()`
저장소 객체에서 데이터를 쓸거면 `getItme()`

```javascript
//데이터 저장
localStorage.setItme('age', '25');
localStorage.setItme('name'. 'heesong');
//데이터 갖고와서 변수에 저장
var age = localStorage.getItme('age');
var name = localStorage.getItme('name');
//저장된 데이터 개수
var TotalItme = localStorage.length;
```

저장소 객체의 데이터 저장 및 조회는 동기방식으로 이뤄지기 때문에 데이터를 저장하거나 조회하는 동안엔 다른 모든 작업이 중단쓰..
그래서 사이트가 대량의 데이터를 빈번하게 저장, 액세스할 시 전체적으로 사이트가 느려짐.

저장소 객체는 주로 JSON형태의 데이터를 저장할 때 사용함.
- JSON -> 자바스크립트 객체로 변환하려면 parse()
- JSON -> 문자열로 변환하려면 stringfy()

```javascript
//객체표현식으로도 가능
localStorage.age = 12;
localStorage.name = 'heesong';
var age = localStorage.age;
var name = localStorage.name;
var TotalItme = localStorage.length;
```

| 메서드 | 설명 |
|--------|:--------|
| setItme(key, value)  | 새로운 키/값 쌍 생성       |
| getItem(key)  | 지정된 키에 해당하는 **값**을 가져옴    |
| removeItem(key)  | 지정된 키에 해당하는 **값**을 삭제 |
| clear()  | 모든 ㅋㅣ/값 쌍 삭제 |


| 속성 | 설명 |
|-----|:--------|
|length|저장된 키의 개수를  리턴|


## 해보기
클릭횟수를 로컬에 저장하고 가져와 보는 예제

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="description" content="">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title>Document</title>
        <link rel="stylesheet" href="css/style.css">
        <script>
        function clickCounter(){
            if(typeof(Storage) !== "undefinded") {
                if (localStorage.clickcount) {
                    localStorage.clickcount = Number(localStorage.clickcount)+1;
                } else {
                    localStorage.clickcount = 1;
                }
                document.getElementById("result").innerHTML = "총" + localStorage.clickcount +"번 클릭했음";
            }else {
                document.getElementById("result").innerHTML = "당신의 인터넷 브라우저는 웹 저장소를 제공하고 있지 못해요."
            }
        }
        </script>
    </head>
    <body>
        <p><button onclick="clickCounter()" type="button">Click Me!</button></p>
        <div id="result"></div>
    </body>
</html>
```

<iframe height='265' scrolling='no' title='WjWwXw' src='//codepen.io/heesong/embed/WjWwXw/?height=265&theme-id=0&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/heesong/pen/WjWwXw/'>WjWwXw</a> by hanheesong (<a href='https://codepen.io/heesong'>@heesong</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


## clear()이벤트 사용해보기
```html
<p><button onclick="clearText()" type="button">Clear</button></p>
```
```javascript
function clearText(){
            localStorage.clear();
            document.getElementById("result").innerHTML = "초기화됨";
        }
```

<iframe height='265' scrolling='no' title='WjWwXw' src='//codepen.io/heesong/embed/WjWwXw/?height=265&theme-id=0&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/heesong/pen/WjWwXw/'>WjWwXw</a> by hanheesong (<a href='https://codepen.io/heesong'>@heesong</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
