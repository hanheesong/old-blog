---
layout: amp
title: "variable handling 함수"
description: "정리"
tag: [php, 실무공부]
category: develope
sitemap:
  changefreq: daily
---
# Variable hanling 함수 목록


### isset()
```java
$a = array ('test'=>null, 'hello'=>1);
if (isset($a['test'])) {
  echo "a의 배열 test는 1이라는 값이 있다.";
} else {
  echo "a의 배열 test는 1이라는 값이 없다.";
}
```

### is_array( $var )
주어진 변수가 배열인지 아닌지

```java
$yes = array('this', 'is', 'an array');

echo is_array($yes) ? 'Array' : 'not an Array';
```

* is_float()
* is_int()
* is_string()
* is_object()

등등..
