---
layout: single
title: "[Node] NVM으로 Node.js 버전관리"
categories: "Development-Tools"
tag: ["react", "npm", "nvm"]
typora-root-url: ../
description: nvm 개념 설명, 설치법, 적용예제
---

## 1. nvm으로 node.js 버전관리

> nvm이란??
> {: .notice--info}

<code>nvm</code>은 <code>node version manger</code>의 약자로, <code>node.js</code> 의 버전관리 도구이다. 협업을 하게되면 프로젝트별로 <code>node.js</code>버전을 관리할수있게 도와준다.

<code>node.js</code>는 프론트엔드 개발환경에서는 너무 많이 쓰이고 있고, 백엔드에서도 <code>node.js</code> + <code>express</code> 조합으로 많이 볼수있다. 회사에서 프론트엔드를 리액트로 하고 있는데 배포환경이 <code>node.js</code> <code>v16.14</code> 로 되있어서 해당 프로젝트를 <code>nvm</code>을 써서 버전을 맞춰줬다.

### 1️⃣ nvm 설치

다운로드는 해당 깃헙 레퍼지토리에서 가능하다.

나의경우에는 <code>v1.1.12</code> 가 최신버전이어서 설치해주었다.

**[https://github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases){:target="\_blank"}**

<img src="/images/2024-01-26-frontend-01/스크린샷 2024-01-27 083009.png" alt="스크린샷 2024-01-27 083009" style="zoom: 33%;" />

### 2️⃣ node.js 릴리즈노트

<code>node.js</code> 릴리즈노트를 확인하고 싶으면 공식홈페이지에서 확인할 수 있다.

**[https://nodejs.org/en/about/previous-releases](https://nodejs.org/en/about/previous-releases){:target="\_blank"}<img src="/images/2024-01-26-frontend-01/스크린샷 2024-01-27 083546.png" alt="스크린샷 2024-01-27 083546" style="zoom:67%;" />**

### 3️⃣ node.js 버전 설치 & 스위칭

나의경우엔 회사에서 사용하는 <code>v16.14.0</code> 으로 설치해주었다.

버전을 관리할 프로젝트 경로에서 아래와 같이 실행해준다.

```
nvm install <버전명>
nvm use <버전명>
nvm list
```

![스크린샷 2024-01-27 084223](/images/2024-01-26-frontend-01/스크린샷 2024-01-27 084223.png)

---

## 호환성 맞지 않는 라이브러리가 설치될시 🥲..

예외상황이 생기길 바라지 않았지만 이번에도 예외상황이 생겼다..

<code>react-hook-form</code> 라이브러리를 설치했는데 <code>v7.49.3</code> 가 설치되었다. 젠킨스툴로 배포하는도중에 다음과같은 에러가 발생하였다. <code>v7.49.3</code> 은 <code>node.js</code> <code>v18.0.0</code> 이상부터 호환하는 라이브러리라는 메시지였다.

<code>v16.14</code> 환경에서 라이브러를 설치하였는데 왜 <code>v18.0.0</code> 이상부터 호환되는 라이브러리가 설치됬는지는 모르겠지만 .. 어찌저찌 방법을 찾아내었다.

<code>react-hook-form</code>을 사용하기위해선 <code>node.js v16.14</code>, <code>react v18</code> 두개의 호환성을 맞춰줘야 됬다.

해당명령어를 통해 <code>v7.0.0</code> 부터 하나씩 올려가면서 <code>react</code>와 <code>node.js</code>의 버전을 체크해주었다.

WindowPowerShell 창을 열어준다.

```
(Invoke-RestMethod -Uri 'https://registry.npmjs.org/react-hook-form/7.0.0') | Select-Object -ExpandProperty _nodeVersion

(Invoke-RestMethod -Uri 'https://registry.npmjs.org/react-hook-form/7.0.0') | Select-Object -ExpandProperty peerDependenciesrty peerDependencies
```

<code>react-hook-form v7.29.0</code>에서 <code>react</code>, <code>node.js</code> 버전이 충족하는것을 확인했다.

![스크린샷 2024-01-27 085347](/images/2024-01-26-frontend-01/스크린샷 2024-01-27 085347.png)

다시 라이브러리를 설치해주었다.

```
npm uninstall react-hook-form
npm i react-hook-form@7.29.0
```

페이지에서 쓰고있던 기능이 정상 동작하는것을 확인하고, 배포하였더니 배포도 정상적으로 되는것을 확인할 수 있었다!
