---
title: "javascript - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-08T20:00:00
---

# javascript

web browser 가 javascript 를 사용하는 대표적인 언어 - 브라우저의 웹페이지를 동적으로 만드는게 사용하는 언어로 개발되었음

스크립트 언어 - 해당 언어를 해석할 수 있는 엔진이 존재

인터프리터 언어 - 한줄씩 읽으면서 바로바로 해석

서버사이드 역할을 하는 node js 가 존재 - 최초 목적과 다르게 서버를 만들 수 있음

모바일(React Native, Native Script) 등 많은 분야에서 사용하고 있다.

# runtime

스크립트 실행환경은 각종 웹프라우저(크롬, 파이어폭스), nodejs, electron 등

여러가지 환경이 있다. 이런 다양한 환경에서 공통으로 동작하기 위해한 노력으로

ECMA 에서 표준을 만들고 있다.

> ~~5를 기준으로 공부하되 ECMA 6의 경우 명시를 하겠다.~~  
> 필요에 따라 명시하자

# 개발 준비

브라우저 환경의 경우 원하는 브라우저를 설치하면 됨

IDE 는 가장 많이 사용하는 무료인 [VSCode](https://code.visualstudio.com/) 를 사용한다.

(개인적으로 webStrom 을 좋아하지만 유료)

설치하지 않아도 자바스크립트 결과를 제공하는 사이트가 존재한다.

[CodeSendbox](https://codesandbox.io/) 에서 `Create Sendbox` 를 클릭하고 `Vanilla` 를 선택한다.

> `Vanilla` 는 다른 라이브러리가 없는 일반 Javascript만 쓰겠다는 의미

# 참고

서버사이드 자바스크립트를 원하면 [node.js](https://nodejs.org/ko/) 설치를 하는데 최신버전 보다는 안정적인 버전을 설치한다.

