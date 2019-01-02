---
layout: amp
title: "지킬 build error"
description: "지킬 포스팅 오류"
tag: [jekyll, error]
category: error
sitemap:
  changefreq: daily
---

지킬 블로그 포스팅이 안돼서 살펴봤더니 openssl이 문제였음.

## 오류해결과정
1. brew로 onenssl 재설치
```bash
brew reinstall openssl
```

2. 링크시키기
```bash
brew link openssl --force
```

3. ffi 재설치
```bash
gem uninstall ffi
gem install ffi --platform=ruby
```

GemFime에 `gem "json"` 라인 추가.
