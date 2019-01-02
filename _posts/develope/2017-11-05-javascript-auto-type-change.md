---
layout: amp
title: "[javascript] 자동타입변환"
description: ""
tag: [javascript]
category: develope
sitemap:
  changefreq: daily
---

문자열과 숫자를 불리언 값으로 변환하는 규칙
`0`, `NaN`, `빈 문자열`은 __false__로 간주!
다른 값은 모두 다 __true__를 반환!

```javascript
false == 0 // true
false === 0 // false
"5" == 5 // true
"" == 0 // true
```
