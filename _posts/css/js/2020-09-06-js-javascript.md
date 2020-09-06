---
title: "javascript - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-06T20:00:00
---

# javascript

스크립트 언어 - 해당 언어를 해석할 수 있는 엔진이 존재

인터프리터 언어 - 한줄씩 읽으면서 바로바로 해석

web browser 가 javascript 를 사용하는 대표적인 언어
* 웹 사이트를 동적으로 만들어줌

서버사이드 역할을 하는 node js 가 존재 - 최초 목적과 다르게 서버를 만들 수 있음

모바일 등 많은 분야에서 사용하고 있다.

# runtime

스크립트 실행환경은 각종 웹프라우저(크롬, 파이어폭스), nodejs, electron 등

여러가지 환경이 있다. 이런 다양한 환경에서 공통으로 동작하기 위해한 노력으로

ECMA 에서 표준을 만들고 있다.

일단은  ECMA 5를 기준으로 공부해보자.

# 개발 준비

브라우저 환경의 경우 원하는 브라우저를 설치하면 됨

[node.js](https://nodejs.org/ko/) 설치를 하는데 최신버전 보다는 안정적인 버전을 설치한다.

IDE 는 가장 많이 사용하는 무료인 [VSCode](https://code.visualstudio.com/) 를 사용한다.

(개인적으로 webStrom 을 좋아하지만 유료)

