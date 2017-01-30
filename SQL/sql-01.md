#### SQL : Structured Query Language
: SQL은 데이터베이스에 접근하고 처리하기 위한 표준 언어이다.

- SQL로 할 수 있는 것은?
  * 데이터베이스에 대해 쿼리를 실행할 수 있습니다.
  * 데이터베이스에서 데이터를 검색 할 수 있습니다.
  * 데이터베이스에 레코드를 삽입 할 수 있습니다.
  * 데이터베이스의 레코드를 업데이트 할 수 있습니다.
  * 데이터베이스에서 레코드를 삭제할 수 있습니다.
  * 새로운 데이터베이스를 생성 할 수 있습니다.
  * 데이터베이스에 새로운 테이블을 생성 할 수 있습니다.
  * 데이터베이스에 저장 프로 시저를 생성 할 수 있습니다.
  * 데이터베이스에 뷰를 생성 할 수 있습니다.
  * 테이블, 프로 시저 및 뷰에 대한 사용 권한을 설정할 수 있습니다.

##### SQL 구문
- SQL 키워드는 대소 문자를 구분하지 않는다.
- 세미콜론 : 세미콜론은 데이터베이스 시스템에서 각 SQL문을 분리하여 서버에 대한 동일한 호출에서 둘 이상의 SQL문을 실행할 수 있도록 하는 표준 방법이다.

- SQL 명령
  * SELECT - 데이터베이스에서 데이터를 추출
  * UPDATE - 데이터베이스에 데이터를 업데이트
  * DELETE - 데이터베이스에서 데이터를 삭제
  * INSERT INTO는 - 데이타베이스에 새로운 데이터를 삽입
  * CREATE DATABASE - 새 데이터베이스를 만듭니다
  * ALTER DATABASE - 데이터베이스를 수정
  * CREATE TABLE - 새로운 테이블을 생성
  * ALTER TABLE - 테이블을 수정
  * DROP TABLE - 테이블을 삭제합니다
  * CREATE INDEX - 인덱스 (검색 키)를 생성
  * DROP INDEX - 인덱스를 삭제

- SELECT
  * 데이터베이스에서 데이터를 선택하기 위해 사용된다.
  * 결과는 결과 테이블에 저장되고, 결과세트라고 불린다.

- SELECT DISTINCT Statement
  * distinct values를 돌려주기 위해서만 사용된다.
  * 테이블에서, column은 많은 이중의 값들을 포함할지도 모른다; 그래서 때때로 distinct values를 만들기를 원할수도 있다.(설명이 어렵게 되있음...)

- WHERE Clause
  * 레코드를 필터링하는데 사용됨
  * 지정된 기준을 충족하는 레코드만 추출하는데 사용됨

- AND / OR
  * AND 및 OR 연산자는 둘 이상의 조건에 따라 레코드를 필터링하는데 사용됨
  * AND 연산자는 첫 번째 조건과 두 번째 조건이 모두 참인 경우 레코드를 표시함
  * OR 연산자는 첫 번째 조건 또는 두 번째 조건이 참이면 레코드를 표시함

- ORER BY
  * 결과 집합을 정렬하는 데 사용
  * 기본적으로 레코드를 오름차순으로 정렬. 내림차순으로 레코드를 정렬하려면 DESC 키워드를 사용할 수 있다.

- INSERT INTO
  * 테이블에 새 레코드를 삽입하는데 사용
```
INSERT INTO table_name
VALUES (value1,value2,value3,...);
or
INSERT INTO table_name (column1,column2,column3,...)
VALUES (value1,value2,value3,...);
```
  * 지정된 열에만 데이터 삽입
```
INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');
```

- UPDATE
  * 테이블의 기존 레코드를 업데이트
```
UPDATE table_name
SET column1=value1,column2=value2,...
WHERE some_column=some_value;
```
_WHERE 절은 갱신해야하는 레코드를 지정한다. WHERE 절을 생략하면 모든 레코드가 업데이트 된다!_

- DELETE
  * 테이블의 레코드를 삭제
```
DELETE FROM table_name
WHERE some_column=some_value;
```
  * 모든 데이터 삭제
```
DELETE FROM table_name;

or

DELETE * FROM table_name;
```
