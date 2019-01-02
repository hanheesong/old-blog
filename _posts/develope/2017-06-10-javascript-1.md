---
layout: amp
title: "jQuery 선택 효과"
description: "jqeury selectable() 함수 정리"
tag: [jquery, javascript]
category: develope
sitemap:
  changefreq: daily
---

```javascript
var fadetime = 500, delaytime = 200;
function selectable(){
  $('.f-btns li').on('mouseover', function(){
    var $me = $(this); //$(this) = $('.f-btns li')
    $me.find('.hover').stop(true, true).show('fade', fadetime);
  }).on('mouseout', function(){
    var $me = $(this);
    if ($me.hasClass('choosed')) return; //만약에 $('.f-btns li')가 choosed 되어 있으면 아래 코드 실행안하고 스코프 종료.
    $me.find('.hover').stop(true, true).hide('fade', fadetime);
  }).on('click', function(){
    var $me = $(this);
    $('.f-btns li .hover').not($me.find('.hover')).stop(true, true).hide('fade', fadetime, function(){
      $(this).closest('li').removeClass('choosed');//나빼고 선택된 애들 다 초기화
    });
    $('form').find('input[name="toothtype"]').remove();
    $('form').append('<input type="hidden" name="toothtype" value="' + $(this).attr('toothtype') + '" />');
  });
}
```

`selectable()` 함수는 `$(window).load()` 창이 로드 될 때 `onloadselectableeffect()`함수가 실행이 되고 실행이 될 때 동안은 select를 못하게 하기 위한 효과 방지 함수로 사용 됨.

onladselectableeffect()함수는 이러하다.
```javascript
function onloadselectableeffect(){
  $('.f-btns li').each(function(i){
    var $me = $(this);
    setTimeout(function(){
      $me.find('.hover').stop(true, true).show('fade', fadetime, function(){
        $me.find('.hover').stop(true, true).hide('fade', fadetime);
      });
    }, i*delaytime);
  });
  selectable();
  setTimeout(function(){
    $('.f-btns li')[0].click();
  }, $('.f-btns li').length*delaytime+fadetime);
}
```
`onloadselectableeffect()`함수가 실행되면 `.f-btns li`에 해당하는 엘리먼트가 하나씩 순서대로 매개변수 `i`와 `delaytime`의 시간 간격으로 오버된다.
그리고 `onloadselectableeffect()` 함수가 종료되면 `selectable()` 함수가 실행되면서 선택이 가능해진다. setTimeout함수는 먼저 `.f-btns li`의 첫번째 엘리먼트를 선택하도록하는 함수.
그 후에 `.f-btns li`의 li 갯수만큼 `delaytime`효과와 `fadetime`을 각자 계산해준다.

각 함수를 만든다음에
```javascript
$(window).load(function(){
  onloadselectableeffect();
});
```
를 호출하면 츄루룩 실행댐
