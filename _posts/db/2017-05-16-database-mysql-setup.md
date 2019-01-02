---
layout: post
title: MAC에서 MySQL setup(install) 설치하기
description: "MySQL setup"
tags: [mysql]
category: db
sitemap:
  changefreq: daily
---

# 설치하기
1. [mysql](https://dev.mysql.com/downloads/mysql/)에 들어가서 Mac OS X 10.12 (x86, 64-bit), DMG Archive 버전으로 다운을 받는다. (2017-05-16)



2. 다운 받은 파일을 설치한다. 설치과정 중에서 임시로 발급해주는 비밀번호를 복사해놓는다. (모르고 복사해놓지 않았을 경우엔 [이글](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)참조)


3. 시스템환경설정->`MySQL`을 선택해서 실행한다


4. `MySQL`이 설치된 경로로 이동 : `cd /usr/local/mysql/bin`

5. `MySQL`실행 : `sudo ./mysql -p패스워드`


6. 접속완료!
![스크린샷 2017-05-16 오전 8.45.14](http://i.imgur.com/3qEGOBP.png)
