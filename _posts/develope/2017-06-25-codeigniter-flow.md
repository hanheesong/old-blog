---
layout: amp
title: "코드이그나이터 주요 흐름"
description: "코드이그나이터 주요 흐름"
tag: [php, 코드이그나이터]
category: develope
sitemap:
  changefreq: daily
---
출처 : http://superad.tistory.com/329


### PHP 예약상수
`DIRECTORY_SEPARATOR` - 운영체제의 경로에 쓰이는 구분값을 반환
리눅스 => /
윈도우 => \

## /index.php

주요 경로 상수를 설정함

* 파일의 이름(?)
`define('SELF', pathinfo(__FILE__, PATHINFO_BASENAME));` - index.php
* 시스템 폴더
`define('BASEPATH', $system_path);` - ~경로\system\
* 루트폴더
`define('FCPATH', dirname(__FILE__).DIRECTORY_SEPARATOR);` - ~경로\
* Name of the "system" directory
`define('SYSDIR', basename(BASEPATH));` - system

`basename` - 경로 이름 구성 요소만 반환
```javascript
echo ".basename("/etc/sudoers.d", ".d")".PHP_EOL; //=> sudoers
echo ".basename("/etc/sudoers.d")".PHP_EOL; //=> sudoers.d
```
* application 폴더
`define('APPPATH', $application_folder.DIRECTORY_SEPARATOR);` - ~경로\application\

* view 폴더
`define('VIEWPATH', $view_folder.DIRECTORY_SEPARATOR);` - ~경로\application\view\

* 부트스트랩 파일 로드
`require_once BASEPATH.'core/CodeIgniter.php'; `

## /system/core/Codeigniter.php
* global functions 불러옴
`require(BASEPATH.'core/Common.php');`
* framework 상수 불러옴
`require(APPPATH.'config/constants.php');`
* base 컨트롤러 클래스 불러옴
`require BASEPATH.'core/Controller.php';`
* 브라우저에 최종 렌더링 된 출력을 보내기
`if ($EXT -> _call_hook('display_override') === FALSE){
  $OUT -> _display();
  }`
