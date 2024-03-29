---
title: "MySQL 스터디 1일차 - architecture"
categories:
    - db
    - mysql
    - architecture
last_modified_at: 2023-04-18T10:15:00
toc: true
---

Real MySQL 4쳅터를 읽고 공부한 것을 정리해보자.

MySQL 서버의 아키텍처에 대하여 구성과 특징을 안다.

# MySQL 엔진 아키텍처

MySQL 서버는 크게 MySQL 엔진과 스토리지 엔진으로 구분할 수 있다.

특징을 알아보자.

## MySQL 엔진

아래와 같은 구성으로 되어있다.

- 커넥션 핸들러
- SQL 인터페이스
- SQL 파서
- SQL 옵티마이저
- 캐시 & 버퍼

## 스토리지 엔진

특징은 아래와 같다.

실제 데이터를 디스크에 저장하거나 읽어오는 부분을 담당한다.

여러 개를 동시에 사용할 수 있다.

InnoDB 스토리지 엔진과 MyISAM 스토리지 엔진 등이 있겠으나 InnoDB 스토리지 엔진만 알아 보자.

## MySQL 스레딩 구조

MySQL 서버는 스레드 기반으로 작동하며 크게 포그라운드 스레드와 백그라운드 스레드로 구분한다.

백그라운드는 무시하고

> thread/sql/one_connection

위 스레드만 실제 사용자 요청을 처리하는 포그라운드 스레드다. 그래서 포그라운드 스레드를 클라이언트 스레드 사용자 스레드 라고 한다.

## 메모리

MySQL에서 사용하는 메모리 공간은 크게 `글로벌 메모리 영역`과 `로컬 메모리 영역`으로 구분할 수 있다.

### 글로벌 메모리 영역

일반적으로 클라이언트 스레드 수와 무관하게 하나의 메모리 공간만 할당된다.

생성된 메모리 영역은 모든 스레드가 공유한다.

대표적인 글로벌 메모리 영역은 다음과 같다.

- 테이블 캐시
- InnoDB 버퍼 풀
- InnoDB 어댑티브 해시 인덱스
- InnoDB 리두 로그 버퍼

### 로컬 메모리 영역

세션 메모리 영역이라고도 한다.

클라이언트 스레드가 사용하는 메모리 영역이다.

절대 공유하여 사용하지 않는다.

대표적인 로컬 메모리 영역은 다음과 같다.

- 정렬 버퍼
- 조인 버퍼
- 바이너리 로그 캐시
- 네트워크 버퍼

## 플러그인

MySQL 플러그인 모델을 사용한다.

그래서 필요한 기능을 플러그인 형태로 개발하여 갈아 낄 수 있다.

## 컴포넌트

MySQL 8.0 부터 기존의 플러그인 아키텍처를 대처하기 위해 컴포넌트 아키텍처가 지원된다.

플러그인의 단점

- 플러그인끼리 통신할 수 없음
- 직접 호출하기 때문에 안전하지 않음
- 초기화가 어려움

## 쿼리 실행 구조

### 쿼리 파서

쿼리 문장을 토큰으로 분리해 트리 형태의 구조로 만든다. 기본 문법 오류를 발견한다.

### 전처리기

구조적인 문제점이 있는지 확인한다. 개체를 매핑해 해당 객체의 존재 여부와 접근 권한 등을 확인한다.

### 옵티마이저

저렴한 비용으로 가장 빠르게 처리할지를 결정한다.

### 실행 엔진

각 핸들러에게 요청하여 수행 시킨다.

### 핸들러(스토리지 엔진)

요청에 따라 데이터를 디스크로 저장하거나 읽어 들인다.

## 복제(replication)

## 쿼리 캐시

~~동일한 SQL 요청을 캐싱~~(8.0에서 제거됨)

## 스레드 풀

~~스레드 개수를 줄여서 동시 처리되는 요청이 많아도 서버의 자원 소모를 줄인다.~~(커뮤니티에디션 지원 X)

## 트랜잭션 메타데이터

5.7 버전까지는 파일로 관리했다. 파일 기반이라 트랜잭션을 지원하지 않는다.

8.0 부터 InnoDB 테이블에 저장 및 관리한다. 그래서 서버가 비정상적으로 종료되어도 스키마 변경이 완전 성공 또는 완전 실패로 처리된다.

## InnoDB 스토리지 엔진 아키텍처

가장 많이 사용되는 스토리지 엔진이다.

레코드 기반의 잠금을 제공하여 높은 동시성 처리와 안전성과 성능을 제공한다.

InnoDB 스토리지 엔진의 구조

- 버퍼 풀
  - 언두 페이지
  - 체인지 버퍼
  - 데이터 페이지 버퍼
  - 어댑티브 해시 인덱스
- 로그 버퍼

### 키에 의한 클러스터링

프라이머리 키 값의 순서대로 디스크에 저장

### 외래 키 지원

### MVCC(Multi Version Concurrency Control)

레코드 레벨의 트랜잭션에서 잠금을 사용하지 않는 일관된 읽기를 제공하는 기능이다

언두 로그를 이용하여 이를 구현하고 멀티 버전으로 하나의 레코드에 대해 여러 개의 버전이 동시에 관리 될 수 있다

### 잠금 없는 일관된 읽기 

MVCC(Multi Version Concurrency Control) 기술을 이용

변견되지 전의 데이털르 읽기 위해 언두 로그를 사용한다

### 자동 데드락 감지

교착 상태를 체크하기 위해 잠금 대기 목록을 그래프 형태로 관리한다

교착 상태에 빠진 트랙잰션들을 찾아서 그중 하나를 강제로 종료하는데 그 대상은 언두 로그 레코드를 가장 적게 가진 트랜잭션이 일반적으로 롤백 대상이 된다.

### 자동화된 장애 복구

서버가 시작될 때 완료되지 못한 트랜잭션이나 디스크에 일부만 기록된 데이터 페이지 등에 대한 복구 작업이 자동으로 진행된다

설정값은 1부터 6까지 가능하다

### 버퍼 풀

데이터 파일이나 인덱스 정보를 메모리에 캐시해 두는 공간으로 쓰기 작업을 지연시켜 일괄 작업으로 처리할 수 있도록 해준다

#### 버퍼 풀 크기

#### 버퍼 풀 구조

LRU(Least Recently Used) 리스트 구조에 Old 서브리스트와 New 서브리스트 영역이 존재

#### 버퍼 풀과 리두 로그

버퍼 풀의 쓰기 버퍼링 기능까지 향상시키려면 리두 로그와의 관계를 이애해야함

데이터를 변경하는 작업을 하면 버퍼 풀의 더티 페이지(Dirty Page)와 리두 로그가 증가하고 데이터가 모두 디스크로 동기화될 때 같이 동기화 된다

#### 버퍼 풀 플러시

급작스럽게 디스크 기록이 폭증할 수 있다

8.0 부터 2개의 더티 페이지 플러시 기능이 부드럽게 처리한다

- 플러시 리스트 플러시 : 주기적으로 플러시 함수 호출
- LRU 리스트 플러시 : 사용 빈도가 낮은 데이터 페이지들을 제거

### 버퍼 풀 상태 백업 및 복구

5.6 부터 버퍼 풀 덤프 및 적재 기능이 도입

### 버퍼 풀 적재 내용 확인

5.6 부터 테이블을 조회할 수 있었는데 상당히 큰 부하를 일으켰다
8.0 부터는 인덱스별로 데이터 페이지가 얼마나 적재되어 있는지 확인할 수 있다

### Double Write Buffer

더티 페이지가 디스크 파일로 플러시할 때 일부만 기록되는 현상같은 오작동이 발생할 수 있다 이런 문제를 막기 위해 Double-Write 기법을 이용한다
시스템의 더블 버퍼에 기록해 놓는다 그리고 디스크 쓰기를 수행할 때 문제가 발생하면 더블 버퍼의 데이터를 파일에 복사한다 즉 실패할 때만 사용하는 버퍼이다

### 언두 로그

데이터가 변경되지 전에 이전 버전의 데이터를 별도로 저장한다

- 트랜잭션 보장 : 트랜잭션이 롤백되면 변경 전 데이터로 복구
- 격리 수준 보장 : 데이터 변경중에 다른 커넥션이 이 데이터를 조회하면 트랜잭션 격리 수준에 맞게 변경중인 레코드를 읽지 않고 언두 로그에 백업해둔 데이터를 읽어서 반환

#### 언두 로그 레코드 모니터링

5.5 버전까지 한 번 늘어난 언두 로그는 줄일 수가 없었는데 8.0 부터 언두 로그 공간을 줄이는 것도 가능해졌다
그래서 언두 로그 레코드가 얼마나 되는지 모니터랑 하는 것이 좋다

#### 언두 테이블스페이스

언두 로그가 저장되는 공간

5.6 이전에는 언두 로그가 시스템 테이블스페이스에 저장됐다
5.6 부터 시스템 변수가 도입 별도의 언두 로그 파일을 사용한다
8.0 부터 항상 외부의 별도 로그 파일에 기록되도록 바뀌였다

### 체인지 버퍼

만약 데이터를 업데이트 할 때 디스크로 직접 읽어와서 업데이트 한다면 이를 즉시 실행하지 않고 임시 공간에 저장하고 수행하는데 이때 사용하는 임시 공간을 의미 한다

### 리두 로그 및 로그 버퍼

데이터베이스 서버는 데이터 변경 내용을 로그로 먼저 기록한다
리두 로그는 서버가 비정상적으로 종료됐을 때 기록하지 못한 데이터를 잃지 않게 해주는 안전장치

### 리두 로그 아카이빙

8.0 부터 리두 로그 아카이빙 기능 추가
데이터 변경이 너무 많아서 리두 로그가 덮어쓰인다고 하더라도 백업이 실패하지 않게 해준다

#### 리두 로그 활성화 및 비활성화

8.0 부터 수동으로 활성화 비활성화 할 수 있게 되었다

### 어댑티브 해시 인덱스

스토리지 엔진이 사용자가 자주 요청하는 데이터에 대해 자동으로 생성하는 인덱스

데이터를 디스크에 읽어오는 경우가 많은 경우 도움이 되지 않는다 또한 메모리 공간을 사용하기 때문에 큰 메모리 공간이 쓰일 수 있다
삭제에도 영향을 미친다

## MySQL 로그 파일

서버 상태를 진단

### 에러 로그 파일

### 제너럴 쿼리 로그 파일

서버에서 실행되는 쿼리의 기록

### 슬로우 쿼리 로그

성능 저하 검사 및 정기적인 점검





