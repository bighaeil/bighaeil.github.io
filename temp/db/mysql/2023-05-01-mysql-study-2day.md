---
title: "MySQL 스터디 2일차 - transaction"
categories:
    - db
    - mysql
    - transaction
last_modified_at: 2023-05-01T17:00:00
toc: true
---

지난 시간에 이어 Real MySQL 5챕터를 읽고 정리한다

# 트랜잭션과 잠금

트랜잭션을 지원하는 InnoDB의 처리 방식을 알아보자

- MyISAM이나 MEMORY 스토리지 엔진은 트랜잭션을 지원하지 않는다

# 트랜잭션

작업의 `완정성`을 보장해 주는 기술

논리 적인 작업 자체가 100% 적용되거나 아무것도 적용되지 않는 것을 보장해 주는 것

```sql

insert into ...; /* 정상 작동 */
insert into ...; /* 정상 작동 */
insert into ...; /* 어떤 이유로 ERROR가 발생 */

```

만약 위 코드가 같은 트랜잭션 상에서 실행한다면 어떤 이유에서든 오류가 발생하였기 때문에 앞서 했던 2번의 insert는 무시하고 전체를 원 상태로 만든다

## 주의사항

프로그램 코드에서 트랜잭션의 범위를 최소화해야 한다
잘못된 설계는 서버 부하로 이어질 수 있다

# 잠금

동시성을 제어하기 위한 기능

한 시점에 하나의 커넥션만 변경할 수 있게 해주는 역활

MySQL에서 사용하는 잠근은 크게 2가지로 나눌 수 있다

- 스토리지 엔진 레벨 : 스토리지 엔진간 상호 영향을 미치지 않는다
- MySQL 엔진 레벨 : 스토리지 엔진을 제외한 나머지로 모든 스토리지 엔진에 영향을 미친다

MYSQL 엔진 레벨 잠금에 대해 알아보자

## 글로벌 락

범위는 MySQL 전체로 잠금 중 가장 범위가 크다. 

8.0부터 조금 더 가벼운 글로벌 락으로 백업 락을 제공한다

## 테이블 락

개별 테이블 단위로 설정되는 잠금

## 네임드 락

단순히 사용자가 지정한 임의의 문자열에 대해 잠금을 설정한다
많은 레코드에 대해서 복작한 요건으로 레코드를 변경하는 트랜잭션에 유용하게 사용할 수 있다

```
1) 한꺼번에 많은 레코드 변경하는 쿼리 
2) 동일 데이터 참조하는 프로그램끼리 분류해서 네임드 락
```

8.0부터 중첩해서 사용할 수 있다. 모두 헤제하는 기능도 추가

## 메타데이터 락

테이블이나 뷰 등 데이터베이스 객체의 이름이나 구조를 변경하는 경우에 획득하는 장금

# InnoDB 스토리지 엔진 잠금

스토리지 엔진 내부에서 레코드 기반의 잠금 기능을 제공하고 잠금 정보가 상담히 작은 공간으로 관리 한다

잠금의 종류로는 다음과 같다

## 레코드 락

레코드 자체만 잠그는 락으로 InnoDB 스토리지 엔진에서는 레코드뿐 아니라 `인덱스의 레코드`도 잠근다

## 갭 락

레코드와 바로 인적한 레코드 사이의 `간격만`을 잠그는 락이다

레코드 사이에 새로운 레코드가 생성(insert)되는 것을 제어한다

## 넥스트 키 락

레코드 락과 갭락을 합쳐 놓은 형태의 락이다

## 자동 증가 락

AUTO_INCREMENT 칼럼 속성 사용할 때 사용

insert 또는 update 같이 새로운 레코드를 저장하는 쿼리에서만 사용

# 인덱스와 잠금

InnoDB의 잠금은 레코드를 잠그는 것이 아니라 인덱스를 장그는 방식으로 처리한다

```sql

update ... where a = 'A' and b = 'B'; /* 결과적으로 1건만 update */

```

변경해야 할 레코드를 찾기 위해 검색한 인덱스의 레코드는 모두 락을 건다

그래서 인덱스 잠금 방식을 모르고 설계하면 성능저하가 올 수 있다

만약 위 조건 a, b에 인덱스 설계가 없다면 테이블의 모든 레코드를 조회해야 한다 즉 모든 레코드는 잠금이 된다

## 레코드 수준의 잠금 확인 및 해제

5.1부터 레코드 잠금과 잠금 대기에 대한 조회가 가능하다

# 격리 수준 (isolation level)

여러 트랜잭션 간의 작업 내용을 어떻게 공유하고 차단할 것인지를 결정하는 레벨

격리 수준은 크게 4가지로 나눈다

## READ UNCOMMITTED

commit이나 rollback 여부에 상관없이 변경 내용이 다른 트랜잭션에서 보인다

### 더티 리드 (Dirty read)

어떤 트랜잭션에서 처리한 작업이 완료되지 않았는데도 다른 트랜잭션에서 볼 수 있는 현상

## READ COMMITTED

어떤 트랜잭션에서 변경했어도 commit이 완료된 데이터만 다른 트랜잭션에서 조회할 수 있는 격리 수준이다

오라클 DBMS에서 기본 격리 수준이다

더티 리드같은 현상은 발생하지 않는다

### NON-REPEATABLE READ 부정합 문제

READ COMMITTED 격리 수준에서도 부정합 문제가 발생한다

```sql
1) 트랜잭션 A 시작
2) select ...; /* A */
3) 다른 트랜잭션 B 시작
4) update set ...; /* A를 B로 변경 */
5) 다른 트랜잭션 B 종료
2) select ...; /* B */
) 트랜잭션 A 종료
```

트랜잭션 A 내에서 똑같은  select 쿼리를 실행했는데 항상 같은 결과를 가져올 수 없는 경우가 있다.

## REPEATABLE READ

MVCC 기능으로 rollback될 가능성에 대비해 변경되기전 레코드를 언두 공간에 백업해주도 실제 레코드 값을 변경한다. REPEATABLE READ 격리 수준은 이를 이용하여 트랜잭션 내에서 동일한 경과를 보여줄 수 있게 보장한다.

NON-REPEATABLE READ 부정합이 발생하지 않는다

InnoDB 스토리지 엔진에서 기본 격리 수준이다

모든 InnoDB의 트랜잭션은 고유한 `트랙잭션 번호`(순차적으로 증가하는 값)를 가진다. 그리고 언두 영역에 트랜잭션의 번호가 포함돼 있다.

```sql
0) /* 데이터: A, 트랜잭션 번호: 6 */
1) 트랜잭션 A 시작 트랜잭션 번호가 10
2) 트랜잭션 A select ...; /* A */
3) 다른 트랜잭션 B 시작 트랜잭션 번호가 12
4) 다른 트랜잭션 B update ...; /* 데이터 A를 B로 변경, 트랜잭션 번호 6을 12로 변경 */
5) 변경 전 데이터를 언두 로그로 복사 /* 데이터: B, 트랜잭션 번호: 6 */
6) 다른 트랜잭션 B 종료
7) 트랜잭션 A select ...; /* 데이블 조회시 트랜잭션 번호가 12 이므로 언두 로그로 조회 트랜잭션 번호가 작은 6번의 데이터 A를 조회 */
```

단점으로 장시간 트랜잭션이 종료되지 않으면 언두 영역의 백업된 데이터가 무한히 커질 수 있다. 즉 성능이 떨어진다

### PHANTIOM READ 부정합 문제

다른 트랜잭션에서 수쟁한 변경 작업에 의해 레코드가 보였다 안 보였다 하는 현상

위 같은 상황에서 트랜잭션이 `SELECT ... FOR UPDATE`를 수행할 때 만약 다른 트랜잭션 B가 insert가 수행한다면 `SELECT ... FOR UPDATE`는 조회되는 레코드는 현제 레코드의 값을 가져오기 때문에 언두 레코드에는 잠금을 걸 수 없다

`SELECT ... FOR UPDATE` 또는 `SELECT ... LOCK IN SHARE MODE`에서 조회되는 레코드는 언두 영역이 아닌 현재 레코드 값을 가져온다

## SERIALIZABLE

한 트랜잭션에서 읽고 쓰는 레코드를 다른 트랜잭션에서는 절대 접근할 수 없다

가장 엄격한 격리 수준

동시 처리 성능이 떨어진다
