---
layout: amp
title: "AMP 적용하기 - 구글의 검색엔진 최적화 사이트 개발하기"
description: "jekyll 블로그에 AMP 프로젝트 설치하고 적용하기"
tags: [AMP]
category: develope
sitemap:
  changefreq: daily
---

AMP는 Accelerated Mobile Pages의 약자로 일반적인 HTML 웹 사이트입니다.

`AMP` 구축해본 결과 `AMP` 설치없이 간단하게 자바스크립트를 포함한 라이브러리를 추가하는것만으로 네이티브한 app를 구축할 수 있게 해주는 매력있는 플랫폼이며 유연하고 간단하기 때문에 퍼블리셔와 개발자 모두가 참여할 수 있습니다.
단, 마크업시 몇 가지 중요한 규칙이 있습니다.
(예를 들면, `<img>`는 `<amp-img`로 표기해야하는 것)

이제 구글의 AMP를 이용하여 검색엔진 최적화 사이트를 만들어 보겠습니다.

# AMP 설치하기

⚡️[juusaw](http://)님의 github 파일 참고⚡️

1. _layout폴더에는 [`amp.html`](https://github.com/juusaw/amp-jekyll/blob/master/amp.html)을 만들고, 루트 디렉토리에서 _plugins 폴더를 생성해서 그 폴더 안에 [`amp_generate.rb`](https://github.com/juusaw/amp-jekyll/blob/master/lib/jekyll/amp_generate.rb)와 [`amp_filter.rb`](https://github.com/juusaw/amp-jekyll/blob/master/lib/jekyll/amp_filter.rb)를 넣습니다.

2. `Gemfile` 파일에 추가한 후 터미널을 열어서 `bundler install`을 실행합니다.
```
gem "fastimage"
gem "amp-jekyll"
```
그 다음 _config.yml 파일에 아래 내용을 추가합니다.
```
ampdir: /_site/amp
gems:
  - amp-jekyll
```

3. 자신이 가지고 있는 `head`와 관련있는 html 문서에다가 추가합니다. ([]=>{})
```html
[% if page.path contains '_posts' %]
	<link rel="amphtml" href="[[ page.id | prepend: '/YOURDIR' | prepend: site.baseurl | prepend: site.url ]]">
[% endif %]
```

4. 터미널을 열고 `gem install amp-jekyll`을 입력해 설치하면 `AMP` 기본적인 세팅이 끝납니다.

# AMP HTML 필수 마크업

  (이건 위의 자료로 받은 amp.html을 활용하면 됩니다.)

  - Doctype `<!doctype html>`로 시작해야 합니다.
  - `<html>`태그에 `amp`와 `lang='ko'`속성을 추가합니다.
  - `<script async src="https://cdn.ampproject.org/v0.js"></script>`를 `<head>`태그 안에 삽입합니다.
  - `<meta name="viewport" content="width=device-width,minimum-scale=1"`도 마찬가지로 `<head>`태그 안에 삽입합니다.
  - AMP에서 제공하는 `script`이외 다른`script`를 사용할 수 없습니다.

  ==필수 마크 업 요소가 많으니 자세한 사항은 [이곳](https://www.ampproject.org/docs/tutorials/create/basic_markup)을 참조해주세요.==

# 미리보기 및 유효성 검사

  빌드 단계나 사전 처리 필요없이 다른 정적 HTML 사이트를 미리 보는 것처럼 AMP 페이지를 미리 볼 수 있습니다.

  1. 브라우저에서 페이지를 엽니다.
  2. URL에 `#development=1`을 추가합니다.
  (예:`http//localhost:8000/released.amp.html#development=1`)
  3. 크롬 개발자모드 콘솔을 열고 유효성 검사 오류를 확인합니다.

# 결과
![스크린샷 2017-05-18 오전 5.17.29](http://i.imgur.com/gQ8PXoG.png)
