---
layout: post
title: Sitemap.xml 형식 정의
description: "Let's take a look at sitemap.xml!"
tag: [develope, sitemap]
category: develope
sitemap:
  changefreq: daily
---

### Sitemap XML 형식
`Sitemap` 프로토콜 형식은 XML 태그로 구성된다.
`Sitemap`의 모든 데이터 값은 [엔티티 이스케이프](#escaping)되어야 하며 파일 자체는 UTF-8로 인코딩되어 있어야 한다.

Sitemap의 조건:
  * 여는 [`<urlset>`](#urlset) 태그로 시작해 닫는 `</urlset>`태그로 종료
  * `<urlset>` 태그 안에 네임스페이스(프로토콜 표준) 지정
  * 각  URL의 [`<url>`](#url) 항목을 상위 XML 태그로 포함
  * 각 `<url>` 상위 태그에 [`<loc>`](#loc) 하위 항목 포함

example:
{% highlight html linenos %}
{% raw %}<?xml version="1.0" encoding="UTF-8"?>
  <urlset xmlns="http://hanheesong.github.io/sitemap.xml">
  <url>
    <loc>http://www.example.com/</loc>
    <lastmod>2017-05-11</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.8</priority>
  </url>
</urlset>{% endraw %}
{% endhighlight %}

---

### XML 태그 정의

| 속성   | 설명  |
| :----- | :---- |
| `<urlset>`<a id="urlset"></a>  | 파일을 캡슐화하고 현재 프로토콜 표준을 참조  |
| `<url>`<a id="url"></a>  | 각 URL 항목의 상위 태그(나머지 태그는 이 태그의 하위 태그)  |
| `<loc>`<a id="loc"></a>  | 페이지의 URL  |
| `<lastmod>`|파일을 마지막으로 수정한 날짜|
| `<changefreq>`| 페이지가 변경되는 빈도 |
|  | always|
|  | daily|
|  | monthly|
|  | weekly|
|  | yearly|
|  | never|
| `<priority>`| 해당 사이트의 기타 URL에 대한 특정 URL의 상대적 우선순위

---

### 엔티티 이스케이프 <a id="escaping"></a>
`Sitemap` 파일은 UTF-8로 인코딩해야 한다. 일반적으로 파일을 저장할 때 인코딩을 지정할 수 있다.
모든 XML 파일과 마찬가지로 모든 데이터 값(URL 포함)은 아래 표에 나와 있는 문자에 대해 엔티티 이스케이프 코드를 사용해야 한다.

|문자|  |이스케이프 코드|
|:--|:--|:-----------|
|엠퍼샌드|&|`&amp;`|
|작은 따옴포|'|`&apos;`|
|큰 따옴포|"|`&quot;`|
|보다 큼|>|`&gt;`|
|보다 작음|<|`&lt;`|
