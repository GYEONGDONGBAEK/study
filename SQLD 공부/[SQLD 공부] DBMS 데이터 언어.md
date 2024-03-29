# [SQLD] DBMS 데이터 언어

---

# **SQL(Structured Query Language)**

![SQL 개괄.png](%5BSQLD%5D%20DBMS%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%8B%E1%85%A5%E1%86%AB%E1%84%8B%E1%85%A5%208accc08fb5494dd7906ba99900e1371c/SQL_%25EA%25B0%259C%25EA%25B4%2584.png)

## **SQL 문법 종류**

데이터 정의 언어(DDL: Data Definition Language)

데이터 조작 언어(DML:Data Manipulation Language)

데이터 제어 언어(DCL:Date Control Language)

트랜잭션 제어 언어(TCL: Transaction Control Language)

### **DDL (Data Definition Language): 데이터 정의 언어**

### DDL이란?

<aside>
💡 테이블과 컬럼을 정의하는 명령어로 생성, 수정, 삭제 등의 데이터 전체 프레임을 결정하는 역할을 담당한다.

</aside>

### DDL 특징

<aside>
💡 DDL은 명령어를 입력하는 순간 작업이 즉시 반영(Auto Commit)되기 때문에 사용할 때 주의해야 한다.

</aside>

### DDL 종류

| 명령어 | 내용 |
| --- | --- |
| CREATE | 테이블을 생성하는 역할 |
| ALTER | 테이블의 구조를 수정하는 역할 |
| DROP | 테이블을 삭제하는 역할 |
| RENAME | 테이블을 이름을 변경하는 역할 |
| TRUNCATE | 테이블을 초기화하는 역할 |

### CREATE 규칙

- 객체를 의미하는 것이므로 단수형으로 이름을 짓는걸 권한다.
- 유일한 이름으로 명명해야 한다.
- 테이블 내의 컬럼명 또한 중복되지 않는 유일한 이름으로 명명해야 한다.
- 정의할 때 각 컬럼은 **`,`**으로 구분하며 테이블 생성문의 마지막은 **`;`**이다.
- 컬럼명은 데이터 표준화 관점에서 일관성 있게 사용해야 한다.
- 컬럼 뒤에 데이터 유형을 반드시 지정해야 한다.
- 테이블과 컬럼명은 반드시 문자로 시작한다.
- 대소문자 구분을 하지 않지만, 기본적으로 대문자로 만들어진다.

### ALTER: 컬럼 변경 문법

| 명령어 | 내용 |
| --- | --- |
| ADD COLUMN | 컬럼을 추가하는 역할 |
| DROP COLUMN | 컬럼을 삭제하는 역할 |
| MODIFY COLUMN | 컬럼을 수정하는 역할 |
| RENAME COLUMN | 컬럼 이름을 변경하는 역할 |
| DROP CONSTRAIN | 컬럼을 제약조건을 기반해서 삭제하는 역할 |

### **DML (Data Manipulation Language): 데이터 조작 언어**

### DML이란?

<aside>
💡 데이터베이스의 내부 데이터를 관리하기 위한 언어이다. 데이터를 조회, 추가, 변경, 삭제 등의 작업을 수행하기 위해 사용된다.

</aside>

### DML 특징

<aside>
💡 DDL과 달리 DML은 적는 즉시 반영(Auto Commit)이 되기 않는다. 다시 말해, DML에 의한 데이터 변동은 영구적인 변경이 아니기 때문에 ROLLBACK으로 다시 되돌릴 수 있다.

또한, DML은 Target 테이블을 메모리 버퍼 위에 올려두고 변경을 수행하기 때문에, 실시간으로 테이블에 반영되지 않는다. Commit 명령어를 통해 Transaction을 종료해야 해당 변경 사항이 테이블에 반영된다.

</aside>

### DML 종류

| 명령어 | 내용 |
| --- | --- |
| SELECT | 데이터베이스에서 데이터를 검색하는 역할 |
| INSERT | 테이블에 데이터를 추가하는 역할 |
| UPDATE | 테이블 내에 존재하는 데이터를 수정하는 역할 |
| DELETE | 테이블에서 데이터를 삭제하는 역할 |

### **DCL (Data Control Language): 데이터 제어 언어**

### DCL이란?

<aside>
💡 데이터를 관리 목적으로 보안, 무결성, 회복, 병행 제어 등을 정의하는데 사용한다. DCL을 사용하면 데이터베이스에 접근하여 읽거나 쓰는 것을 제한할 수 있는 권한을 부여하거나 박탈할 수 있고 트랜잭션을 명시하거나 조작할 수 있다.

</aside>

### DCL 특징

<aside>
💡 불법적인 사용자로부터 데이터를 보호하기 위한 데이터 보안의 역할을 수행하며, 데이터의 정확성을 위한 무결성을 유지하기도 한다. 마지막으로 시스템 장애에 대비한 회복과 병행수행을 제어한다.

</aside>

### DCL 종류

| 명령어 | 내용 |
| --- | --- |
| GRANT | 권한을 정의할때 사용하는 명령어 |
| REVOKE | 권한을 삭제할때 사용하는 명령어 |

### TCL (Transaction Control Language): 트랜잭션 제어 언어

### TCL이란?

<aside>
💡 DCL과 비슷한 맥락이지만 데이터를 제어하는 언어가 아닌 트랜잭션을 제어할때 사용한다. 논리적인 작업 단위를 묶어 DML에 의해 조작된 결과를 트랜잭션 별로 제어한다.

</aside>

### 트랜잭션의 Commit과 Rollback

### Commit

Commit은 모든 작업들을 정상 처리하겠다고 확정하는 명령어이다. 해당 처리 과정을 DB에 영구 저장하겠다는 의미로 Commit을 수행하면 하나의 트랜잭션 과정이 종료된다. Commit을 하기 전에는 다른 사용자가 트랜잭션 내용을 확인할 수 없다. 또한, 변경된 행은 잠금이 설정되어 있어서 다른 사용자가 변경할 수 없다.

### Rollback

Roll-back은 작업 중 문제가 발생되어 트랜잭션의 처리 과정에서 발생한 변경사항을 취소하는 명령어이다. 해당 명령을 트랜잭션에게 하달하면 트랜잭션은 Commit 되기 이전의 데이터오 돌아가 변경에 대하여 취소한다. 관련된 행에 대한 잠금이 풀리고 데이터 변경 사항이 복구되는 것이다.

### TCL 종류

| 명령어 | 내용 |
| --- | --- |
| COMMIT | 모든 작업을 정상적으로 처리하겠다는 명령어 |
| ROLLBACK | 모든 작업을 다시 돌려 놓겠다는 명령어 |
| SAVEPOINT | Commit 전에 특정 시점까지만 반영하거나 Rollback하겠다는 명령어 |