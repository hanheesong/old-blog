---
layout: post
title: "[맥]Homebrew로 Node.js 설치하기(재설치)"
description: "Nodejs-Mac(OSX)에 nodejs를 설치하는 최고의 방법"
tag: [ 설치, Node.js, Homebrew, 맥 ]
category: develope
sitemap:
  changefreq: daily
---

### 💬
nodejs를 nodejs.org사이트에서 다운로드해 설치했더니 파일 시스템 접근할 때 권한 에러가 작렬한다..그래서 삭제하고 brew로 깔아 보려고 한다. (Homebrew최고임👍)

## nodejs 제거
- node와 npm을 시스템에서 제거함. (sudo권한 필요)
```bash
$ cd /usr/local; sudo rm -r bin/node bin/npm include/node /lib/node_modules
```
- brew로 node삭제
```bash
brew uninstall node
```

## node 설치
 ⚠️ 설치 할 떄 Xcode를 앱스토어에서 다운받아서 한 번 실행하면 시스템 권한을 가질 수 있게 셋팅 됨
- homebrew 설치 (homebrew 없을 때)
```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

- node 설치. 아직 npm 설치는 ❌
```bash
brew install node --without-npm
```

- 자신 계정 폴더에서 `.bash_profile`파일 생성하고 내용추가.
node 버전은 다 다르니 현재 버전 알아보고 수정하면 됨.
```bash
export PATH="/usr/local/Cellar/node/7.10.0/bin:$PATH"
```

- 다음과 같이 실행해서 node파일의 경로를 system에 등록해 어디서나 node명령을 수행할 수 있도록 설정.
```bash
. .bash_profile
```
- 마지막으로 `npm`설치.
```bash
curl -L https://www.npmjs.com/install.sh | sh
```

![스크린샷 2017-05-24 오전 8.07.16](http://i.imgur.com/GHNTrwQ.png)

끝.

테스트 해볼겸 그런트를 깔아봤음.
![스크린샷 2017-05-24 오전 8.07.43](http://i.imgur.com/r7jaN0E.png)

오예~🎉
