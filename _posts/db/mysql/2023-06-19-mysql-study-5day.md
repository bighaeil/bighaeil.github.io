---
title: "MySQL 스터디 5일차 - optimizer"
categories:
    - db
    - mysql
    - index
last_modified_at: 2023-06-07T22:00:00
toc: true
---

데이터베이스 서버에서 두뇌와 같은 역활

요청 처리에 있어 더 최적화된 방법을 수립하도록 유도

# 쿼리 실행 절차

쿼리가 실행되는 과정

1. SQL 파싱(parsing), SQL 파서 모듈에서 처리하며 문법이 잘못되었는지 체크하고 SQL 파스 트리를 만든다. SQL 파스 트리는 쿼리를 의미 있는 단위로 쪼개서 트리로 만든 구조

2. 최적화 및 실행 계획 수립. SQL 파스 트리를 참조하여 내용 처리

- 불필요한 조건 제거 및 복잡한 연산의 단순화
- 여러 테이블의 조인이 있는 경우 어떤 순서로 테이블을 읽을지 결정
- 각 테이블에 사용된 조건과 인덱스 통계 정보를 이용해 사용할 인덱스를 결정
- 가져온 레코드들을 임시 테이블에 넣고 다시 한번 가공해야 하는지 결정

3. 실행 계획대로 스토리지 엔진에 레코드를 읽어 오도록 요청, 레코드를 조인하거나 정렬

# 종류

규칙 기반 최적화 방법과 비용 기반 최적화 방법이 있다

- 규칙 기반 최적화. 옵티마이저에 내장된 우선순위에 따라 실행 계획을 수립. DBMS에서 거의 사용되지 않음
- 비용 기반 최적화. 각 단위 작업의 비용(부하) 정보화 대상 테이블의 예측된 정보를 이용해 실행 계획 수립

# 기본 데이터 처리

## 스켄

옵티마이저는 다음과 같은 조건에서 풀 테이블 스캔을 선택한다

- 레코드 건수가 너무 작을 때
- 인덱스를 이용할 수 있는 조건이 없을 때
- 옵티마이저가 판단한 조건 일치 레코드 건수가 너무 많을 때

InnoDB 에서는 특정 테이블의 연속된 데이터 페이지를 읽을 때 백그라운드 스레드에서 리드 어헤드(Read ahead) 작업을 수행한다. 리드 어헤드는 필요할 것 같은 데이터를 디스크에서 미리 읽어 버퍼 풀에 두는 것

## 병렬 처리

8.0 부터 가능

하나의 쿼리를 여러 스레드에서 처리

## ORDER BY 처리

정렬을 처리하는 방법은 2가지가 있다

- 인덱스 이용. 이미 인덱스가 정렬돼 있어 읽기만 하면됨
- Filesort 이용. 레코드가 많지 않으면 유리

인덱스 정렬이 유리하지만 모든 정렬을 인덱스로 처리 할 수 없음

- 정렬 기준이 너무 많은 경우
- GROUP BY 또는 DISTINCT 같은 처리 결과를 정렬하는 경우
- UNION 같이 임시 테이블의 결과를 다시 정렬하는 경우
- 랜덤하게 결과 레코드를 가져오는 경우

MySQL 서버에서는 정렬 처리를 어떻게 수행하는지 실행 계획의 Extra 칼럼으로 확인할 수 있다

### 소트 버퍼

정렬을 수행하기 위해 별도의 메모리 공간

정렬해야 할 레코드 건수가 소트 버퍼보다 크다면?

이때 래코드를 여러 조각으로 나눠서 처리하고 이를 위해 디스크에 임시 저장한다

즉 디스크 쓰기와 읽기를 유발한다

그렇다고 소트 버퍼를 크게 설정해도, 실제 벤치마크 결과는 큰 차이를 보이지 않는다. 너무 큰 소트 버퍼는 큰 메모리 공간 할당 때문에 성능이 떨어질 수 있다.

### 정렬 알고리즘

- 싱글 패스 정렬 방식.
정렬 키와 레코드 전체를 가져와서 정렬.
SELECT 대상의 칼럼 전부를 가져와서 정렬을 수행.
많은 소트 버퍼 공간이 필요.
- 투 패스 정렬 방식.
정렬 키와 레코드의 로우 아이디(Row ID)만 가져와서 정렬.
정렬 대상 칼럼과 프라이머리 키 값만 소트 버퍼에 담아서 정렬.
두 번 읽어야 함.

일반적으로 싱글 패스 정렬 방식을 주로 사용한다. 하지만 다음과 같은 경우 투 패스 정렬 방식을 사용한다

- 레코드 크기가 max_length_for_sort_data 시스템 변수에 설정된 값보다 클 때
- BLOB이나 TEXT 타입의 칼럼이 SELECT 대상에 포함할 때

보통 SELECT 할 때 (*)를 많이 사용하는데 그러면 정렬 버퍼를 비효율적으로 사용한다. 그래서 SELECT 쿼리에 꼭 필요한 칼러만 조회하는 것을 권장.

### 정렬 처리 방법

옵티마이저는 정렬 처리를 위해 인덱스를 사용할 수 있는지 검토한다. 이용할 수 없다면 filesort로 처리를 한다.

쿼리에 ORDER BY를 사용하면 다음 3가지 중 하나로 처리한다

- 인덱스를 사용한 정렬. 실행 계획의 Extra 컬럼에 표시 없음. 값이 정렬돼 있기 때문에 순서대로 읽기.
- 조인에서 드라이빙 테이블만 정렬. "Using filesort" 표시. 첫 번째로 읽히는 테이블(드라이빙 테이블)의 칼럼만 ORDER BY 절에 작성된 경우.
- 조인에서 조인 결과를 임시 테이블로 저장 후 정렬. "Using temporary; Using filesort" 표시. 항상 조인 결과를 임시 테이블에 저장하고 다시 정렬함.

### 정렬 처리 성능 비교

WHERE 조건에서 인덱스를 잘 적용해도 ORDER BY나 GROUP BY에서 잘못 처리하면 쿼리가 느려진다.

먼저 쿼리가 처리되는 방법인 스트리망 처리와 버퍼링 처리를 확인하다

- 스트리밍 처리. 서버 쪽에 데이터가 얼마인지 관계없이 조건이 일치하는 레코드가 검색될 때마다 바로 클라이언트로 전송. LIMIT 조건을 추가하면 가져오는 레코드 건수가 줄어듬
- 버퍼링 방식. 모든 레코드를 가져온 후 차례대로 내보낸다. ORDER BY나 GROUP BY같은 처리는 결과를 스트리밍되는 것이 불가능하다. LIMIT 조건이 있어서 성능 향상에 별로 도움이 되지 않는다

어느 테이블이 먼저 드라이빙되어 조인되는지도 중요하지만 어떤 정렬 방식으로 처리되는지가 더 큰 성능 차이를 만든다.

### 정렬 관련 상태 변수

정렬에 관해 지금까지 몇 건의 레코드나 정렬 처리를 수행했는지, 소트 버퍼 간의 병합 작업은 몇 번있었는지 확인할 수 있다.

```sql
SHOW STATUS LIKE 'Sort%';
```

## GROUP BY 처리

GROUP BY에 사용된 조건은 인덱스를 사용해서 처리될 수 없다. HAVING 절을 튜닝하려고 인덱스를 생성하거나 다른 방법을 고민할 필요는 없다.

인덱스를 이용할 때는 인덱스 스캔 방법과 루스 인덱스 스캔 방법을 사용한다.

인덱스를 사용하지 못하는 쿼리는 임시 테이블을 사용한다.

### 임시 테이블을 사용

인덱스를 전혀 사용하지 못할 때

8.0 부터 묵시적인 정렬은 더 이상 실행되지 않음

8.0 부터 GROUP BY와 ORDER BY가 같이 사용되면 명시적으로 정렬 작업을 싱행

## DISTINCT 처리

특정 칼럼의 유니크한 값만 조회

SELECT DISTINCT 형태 쿼리 문을 사용하는 경우 GROUP BY와 내부적으로 같은 작업을 수행

COUNT(), MIN(), MAX() 같은 집합 함수와 DISTINCT 가 함께 사용하는 경우 `COUNT(DISTINCT s.a)`같은 처리를 하기 위해 임시 테이블을 사용한다.

`COUNT(DISTINCT ...)` 같이 복수 칼럼의 경우에 또 다른 임시 테이블을 필요로 한다.

## 내부 임시 테이블 활용

사용자가 생성한 임시 테이블(CREATE TEMPORAY TABLE)과는 달리 내부적인 임시 테이블은 쿼리의 처리가 완료되면 자동으로 삭제된다

8.0 이전에는 스토리지 엔진과 관계없이 임시 테이블이 메모리를 사용할 때 MEMORY 스토리지 엔진을 사용하다. 디스크에 저장될 때는 MyISAM 스토리지 엔진을 이용한다.

8.0 부터는 메모리는 TempTable이라는 스토리지 엔진을 사용하고, 디스크에 저장되는 임시 테이블은 InnoDB 스토리지 엔진을 사용한다.

MEMORY 스토리지 엔진은 가변 길이 타입을 지원하지 못한다.

MyISAM 스토리지 엔진은 트랜잭션을 지원하지 못한다.
