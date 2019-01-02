---
layout: amp
title: "jQuery : tab"
description: "jQuery tab 탭 텝"
tag: [jquery, javascript, tab]
category: develope
sitemap:
  changefreq: daily
---

### flow
a엘리먼트의 onclick 을 이용해 gotab(idx)를 넘김
gotab함수는 idx로 해당하는 탭의 콘튼츠를 찾아 보여줌.

### 필요변수 : idx, go
- idx의 타입은 숫자여야함.
  idx = Number(idx);
- go는 탭 콘텐츠에서 id값이 tab-1, tab-2, tab-3의 규칙을 갖고 있도록 만들어줘야함.
  var $go = $tabcontainer.find('[id^="tab-' + idx +'"]');

```html
<div class="cont-top">

  <div class="tab-header f-btns">
    <ul class="tab-list">
      <li class="tab-item tab1"><a href="javascript:void(0)" onclick="gotab('1')"><img src="tab1_off.png" alt="탭 선택 전"><div class="hover"><img src="tab1_on.png" alt="탭 선택 후"></div></a></li>
      <li class="tab-item tab2"><a href="javascript:void(0)" onclick="gotab('2')"><img src="tab2_off.png" alt="탭 선택 전"><div class="hover"><img src="tab1_on.png" alt="탭 선택 후"></div></a></li>
      <li class="tab-item tab3"><a href="javascript:void(0)" onclick="gotab('3')"><img src="tab3_off.png" alt="탭 선택 전"><div class="hover"><img src="tab1_on.png" alt="탭 선택 후"></div></a></li>
    </ul>
  </div>

</div>


<div class="cont-middle">

  <div id="tabs-container">

    <div id="tab-1" class="tab-cont">
      <img src="tab1.jpg" alt="첫번째 탭">
    </div>

    <div id="tab-2" class="tab-cont">
      <img src="tab2.jpg" alt="두번째 탭">
    </div>

    <div id="tab-3" class="tab-cont">
      <img src="tab3.jpg" alt="세번째 탭">
    </div>

  </div>

</div>
```
`.tab-list li`안에 `a` 태그 `onclick` 속성을 사용해 `gotab()`를 호출하고 매개변수로 idx를 넘김.


```javascript
var $tabctrls       = $('.f-btns li'),
    $tabcontainer   = $('#tabs-container'),
    $tabitems       = $('.tab-cont');

function gotab(idx) {
  idx = Number(idx);  // idx 값을 숫자 타입으로 바꿔서 idx에 저장
  if ( isNan(idx) || idx<=0 ) idx = 0;  // idx 값을 0으로 세팅
  idx++;   

  var $go          = $tabcontainer.find('[id^=tab-]' + idx + '"]');

  if (idx !== -1) { //4
    $tabitems.hide();
    $go.show();
  }
}
```
## isNan()
`isNan()` 어떤 값이 숫자가 아닌지 여부를 나타내서 부울 값을 반환
NaN (숫자 아님) 이면 true, 숫자면 false를 반환 !

```javascript
isNan(100) //false
isNan('dd') //true
```
