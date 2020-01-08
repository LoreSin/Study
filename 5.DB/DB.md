# Database
  대용량의 데이터 기지 (Data + Base = 데이터 기지)
  실시간 + 지속성 + 공유성 + 중복최소 + 안정성등을 갖추면 DBMS. 
  SQL 을 통해서 관리. (Structured Query Language : 구조적 질의 언어)


## SQL
  DDL / DML / DCL
  RDB 에서 사용되는 DB 를 사용하기 위한 언어

### DDL
  데이터 정의(Define) 언어
  
  - 스키마 또는 테이블등 데이터를 보관하는 구조를 관리하는 언어
  - CREATE, ALTER, DROP 등으로 시작하는 명령어들.
  - SCHEMA, TABLE, INDEX 등 `데이터구조를 정의`한다고 생각.

### DML
  데이터 조작(Manipulation) 언어
  
  - 테이블이나 인덱스등에 포함된 데이터를 직접 조작하는 언어.
  - SELECT, INSERT, UPDATE, DELETE 및 JOIN 등.
  - 흔히 웹에서 이야기하는 CRUD (Create, Read, Update, delete) 는 여기에 해당.
  
### DCL
  데이터 제어(Control) 언어

  - 데이터사용자의 사용권한을 제어.
  - GRANT, REVOKE 등의 유저권한에 따른 제어 // COMMIT, ROLLBACK 등 쿼리작업 반영여부를 제어.
  - 외부 커넥션 접근제어를 의미.

## NoSQL
  RDB 형식이 아닌 데이터를 처리하는 DB
  유형에 따라 Key-Value, Document, Column, Graph 형식이 존재.

-----


## MySQL
  많이 쓰이는 DBMS 중 하나
  워크벤치 (Workbench) 를 이용, 관리가 용이함. (각 언어마다 비슷한 툴 존재)
  Oracle 로 소유권이 넘어간 뒤, 주요 제작자가 나와서 만든 MariaDB 는 거의 완벽히 호환된다고 함.

## OracleDB
  Oracle 에서 제공하는 DB. 일부 SQL 문법이 다른 경우가 있음.
  성능은 약간 떨어지나, 안정성면이 높다고 함.

## MongoDB
  NoSQL 이며 Non-RDB 에서 사용되는 DB
  Document 타입 (Json 데이터) 의 동적 스키마 데이터를 취급

