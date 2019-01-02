---
layout: amp
title: "체크 형식 자바스크립트"
description: "체크 형식 자바스크립트"
tag: [javascript]
category: develope
sitemap:
  changefreq: daily
---
```javascript
var f = [];
f.init = function(){
  f.btn();
}
f.btn = function(){
  var btn_item = $('.f-btns li');

  btn_item.on('mouseover',function(){
    var me = $(this);
    if ( me.hasClass('checked') ) {// btn_item이 이미 checked라는 클래스가 있다면 그냥 끝내기
      return;
    } else {
      me.addClass('hover');
    }
  }).on('mouseout',function(){
    var me = $(this);
    me.removeClass('hover');
    if ( me.hasClass('checked') ) { //checked라는 클래스가 있으면 그냥 냅둬
      return;
    }
  }).on('click', function(){
    var  me         = $(this)
        ,user_data  = me.closest('.f-btns').find('[toothtype]')
        ,form       = $('form')
        ,toothtype  = []
        ;
    me.toggleClass('checked');
    form.find('input[name="toothtype"]').remove();
    user_data.each(function(){
      if ( !$(this).attr('toothtype') ) {//속성이 toothtype이 아니라면 끝내기
        return;
      }
      if ( $(this).hasClass('checked') ) {
        toothtype.push($(this).attr('toothtype'));
      }
    });
    toothtype = toothtype.join(';');
    form.append('<input type="hidden" name="toothtype" value="'+toothtype+'"/>')
  });
}
```
# 분석
### mousenter vs mouseover
`mouseenter` 이벤트는 바인딩 된 요소에 마우스 포인터가 진입해야만 발생하고,
 __자식 요소__에는 이벤트 적용 XXX
 `mouseenter`는 좀 엄격한 느낌

 체크 리스트에서 체크 된 효과를 주기 위해서는 자식요소에 영향을 계속 끼치게 해주는 `mouseover`를 사용하는게 효과적일 것 같다.
