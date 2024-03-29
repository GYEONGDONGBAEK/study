# [DB] 트랜잭션(Transaction)

---

## **트랜잭션(transaction)**

**트랜잭션이란 데이터베이스의 상태를 변화시키기 위해 수행하는 작업의 논리적 단위다.** 데이터 베이스의 상태를 변화시킨다는 말은 SELECT, INSERT, UPDATE, DELETE 등과 같은 조작어를 사용하는 행동을 의미한다.

이런 트랜잭션은 상황에 따라 여러 개가 만들어 질 수 있고, 그 각각의 트랜잭션들은 상황에 따라 Commit(저장) 되거나 Rollback(철회) 될 수 있다.

- **커밋(Commit)**: 모든 부분작업이 정상적으로 완료하면 이 변경사항을 한꺼번에 DB에 반영한다.
- **롤백(Rollback)**: 부분 작업이 실패하면 트랜잭션 실행 전으로 되돌린다.

### **트랜잭션의 사용 이유**

1. A 은행에서 출금하여 B은행으로 송금하려고 한다.
2. 송금 중, 알 수 없는 오류가 발생하여 A은행 계좌에서 돈은 빠져나갔지만 B은행의 계좌에 입금되지 않았다.
3. 이와 같은 상황을 막기 위해 거래가 성공적으로 모두 끝나야 이를 완전한 거래로 승인하고, 거래 도중 뭔가 오류가 발생했을 때는 이 거래를 처음부터 없었던 거래로 완전히 되돌린다.

이렇게 거래의 안전성을 확보하는 방법으로 트랜잭션을 사용한다. 데이터베이스에서는 테이블로부터 데이터를 읽어 온 후 다른 테이블에 데이터를 입력하거나 갱신, 삭제하는데 처리 도중 오류가 발생하면 Rollback 되고, 모든 처리 과정이 성공적으로 수행되었을 경우에 최종적으로 Commit 된다.

### 트랜잭션의 의미

- 트랜잭션은 데이터베이스 시스템에서 병행 제어 및 회복 작업 시 처리되는 작업의 논리적 단위이다.
- 사용자가 시스템에 대한 서비스 요구 시 시스템이 응답하기 위한 상태 변환 과정의 작업단위이다.
- 하나의 트랜잭션은 Commit 되거나 Rollback 된다.

---

## 트랜잭션의 특징(ACID)

## 원자성(Atomicity)

- 트랜잭션의 작업이 부분적으로 실행되거나 중단되지 않는 것을 보장한다.
- 즉, 트랜잭션이 DB에 모두 반영되거나 혹은 전혀 반영되지 않아야 합니다.(All or Nothing)

## **일관성(Constency)**

- **트랜잭션의 작업 처리 결과는 항상 일관성이 있어야 한다.**
- 예를 들어, 작성 테이블의 본문 내용의 글자 제한이 255글자이고, 트랜잭션이 일어나면 글자 제한 조건을 만족해야만 트랜잭션이 수행되고 위반한다면 거부해야 한다.
- 즉, 트랜잭션 수행 전, 후에 데이터 모델의 모든 제약 조건(기본키, 외래 키, 도메인, 도메인 제약조건 등)을 만족해야 한다.

## **격리성, 고립성(Isolation)**

- **트랜잭션 수행 시 다른 트랜잭션의 작업이 끼어들지 못하도록 보장해야 한다.**
- 즉, 둘 이상의 트랜잭션이 동시에 병행(parallelism) 실행되고 있을 때, 어떤 트랜잭션도 다른 트랜잭션 연상에 끼어들 수 없습니다.

## **지속성, 영속성(Durability)**

- **성공적으로 수행된 트랜잭션은 영원히 반영되어야 한다.**
- 즉, 트랜잭션이 성공적으로 종료되어 Commit 연산을 실행했다면 해당 데이터는 데이터베이스에 영원히 반영이 되어야 합니다.

---

## 트랜잭션의 상태

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/2eff32c8-0f11-425a-ab8b-a8d00be79745">

- **활동(Active) :** 트랜잭션이 실행중인 상태
- **실패(Failed) :** 트랜잭션 실행에 오류가 발생하여 중단된 상태
- **철회(Aborted) :** 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태
- **부분 완료(Partially Committed) :** 트랜잭션의 마지막 연산까지 실행했지만, Commit 연산이 실행되기 직전의 상태
- **완료(Committed) :** 트랜잭션이 성공적으로 종료되어 Commit 연산을 실행한 후의 상태