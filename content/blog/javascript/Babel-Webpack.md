---
title: Babel&Webpack
date: 2020-12-31 11:16:38
category: "javascript"
draft: false
---

# Babel & Webpack

**ES6**

- IE11 지원율 11%

**모듈**

- 대부분의 프로젝트가 모듈을 사용하므로 모듈 로더 필요
- ES6 모듈은 모던 브라우저는 지원하지만 다음과 같은 단점이 있다.
  - IE 를 포함한 구형 브라우저 는 ESM 을 지원하지 않는다.
  - ESM을 사용해도 트랜스파일링과 번들링이 필요하다.
  - ESM이 아직 지원하지 않는 기능이 있다.

**Babel&Webpack**

- Bable
  - 트랜스파일러
- Webpack
  - 모듈 번들러

## Babel

### 설치

- npm 사용
- 버전 지정 시 패키지 이름 뒤에 @버전

**install**

```bash
$ cd Documents/dev/
$ mkdir esnext-project
$ cd esnext-project/


$ npm init -y
Wrote to C:\Users\atlas\Documents\dev\esnext-project\package.json:

{
  "name": "esnext-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}

$ npm i --save-dev @babel/core @babel/cli

```

**package.json**

```json
{
  "name": "esnext-project",
  "version": "1.0.0",
  "devDependencies": {
    "@babel/cli": "^7.12.10",
    "@babel/core": "^7.12.10"
  }
}
```

### Babel 프리셋 설치 & babel.config.json 설정 파일

**babel 프리셋**

- 함께 사용되어야할 babel 플러그 인들을 모아둔 것
- @babel/preset-env
  - 필요한 플러그인들을 프로젝트 지원 환경에 맞춰서 동적으로 결정

```bash
$ npm i --save-dev @babel/preset-env
```

```json
{
  "name": "esnext-project",
  "version": "1.0.0",
  "scripts": {
  },
  "devDependencies": {`1`
    "@babel/cli": "^7.12.10",
    "@babel/core": "^7.12.10",
    "@babel/preset-env": "^7.12.11"
  }
}

```
