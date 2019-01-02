---
layout: amp
title: "코드이그나이터 MVC 패턴"
description: "코드이그나이터 MVC 패턴"
tag: [코드이그나이터, MVC]
category: develope
sitemap:
  changefreq: daily
---

만약에 유저가 요청한 URL주소가 `http://oo2.org/topic/get/1`일 때,
`코드이그나이터`는 application/controller/topic.php을 로드한다.
topic -> 컨트롤러 클래스
get -> 컨트롤러 클래스의 메소드
1 -> 컨트롤러 클래스 메소드의 파라미터 값

```java
class Topic extends CI_controller{
  function get($id) {
    $this->load->model('topic_model'); //1
    $topic = $this->topic_model->get($id); //2
    $this->load->view('topic', array('topic'=>$topic)); //3
  }
}
```

## 코드이그나이터 MVC 구조 파악
1. 모델 로드하기 : `$this->load->model('topic_model')`하게 되면 `코드이그나이터`는 인자에 해당하는 값인 application/models/topic_model.php를 찾아서 로드합니다.
```java
//topic_model.php
class Topic_model extends CI_Model{
  function get($topic_id){
    return $value;
  }
}
```
2. 로드한 모델 사용하기 : `$topic = $this->topic_model->get($id)`는 topic_model의 클래스의 get메소드를 호출하겠다라는 뜻이 됩니다.
그리고 맨 마지막에 `$value`값이 return되면서 `$topic`변수에 저장이 되겠죠.

3. 뷰 호출하기 : $this->load->view('topic', array('topic'=>$topic));
```html
<html>
  <head><?=$topic['title']?></head>
</html>
```
`$topic`은 로드한 모델인 get()메소드의 `$value` 배열 값이 들어있으므로 `$value`에 title이라는 값이 배열에 저장되어 있으면 해당 되는 정보를 출력하겠죠.
