---
layout: post
title: "input 요소 radio name 속성"
description: "input radio 요소 사용시 주의점"
tag: [html]
category: develope
sitemap:
  changefreq: daily
---
 
{% highlight html linenos %}
{% raw %}
<label for="radio-1"><input type="radio" name="agreement" id="radio-1"/>예</label>
<label for="radio-2"><input type="radio" name="agreement" id="radio-2"/>아니오</label>
{% endraw %}
{% endhighlight %}

라디오 타입은 같은 name 속성 값을 가진 요소를 기준으로 선택한다.
위의 예시에서 '예'를 클릭했을 때 '아니오'가 해제 되는 것은 둘이 같은 name 속성 값인 agreement를 사용하고 있기 때문
