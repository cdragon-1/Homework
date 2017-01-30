- UNION
  * 두 개 이상의 select 문의 결과 집합을 결합하는데 사용
  * union 내의 각 select 문은 동일한 수의 열을 가져야 한다. 열은 유사한 데이터 유형을 가져야 한다. 또한 각 select의 열은 동일한 순서여야 한다.
```
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;

SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;
```
- SELECT INTO
  * 한 테이블의 정보를 다른 테이블로 복사할 수 있다.
  * 한 테이블의 데이터를 복사하여 새 테이블에 삽입한다.
```
SELECT *
INTO newtable [IN externaldb]
FROM table1;

SELECT column_name(s)
INTO newtable [IN externaldb]
FROM table1;
```
- INSERT INTO SELECT
  * 한 테이블의 데이터를 복사하여 기존 테이블에 삽입한다.
  * 목표 테이블의 기존 행에는 영향을 주지 않는다.
```
INSERT INTO table2
SELECT * FROM table1;

INSERT INTO table2
(column_name(s))
SELECT column_name(s)
FROM table1;
```
-CREATE DB
  * 데이터베이스를 만든다.
```
CREATE DATABASE dbname;
```
- CREATE TABLE
  * 데이터베이스에 테이블을 작성하는데 사용.
  * 테이블은 행과 열로 구성된다.
  * 각 테이블에는 이름이 있어야 한다.
```
CREATE TABLE table_name
(
column_name1 data_type(size),
column_name2 data_type(size),
column_name3 data_type(size),
....
);
```
  * column_name 매개 변수는 테이블의 컬럼 이름을 지정한다.

  * data_type 매개 변수는 열에서 보유 할 수있는 데이터 유형 (예 : varchar, 정수, 십진수, 날짜 등)을 지정한다.

  * size 매개 변수는 테이블의 열의 최대 길이를 지정한다.

- CONSTRAINTS
  * 테이블의 데이터에 대한 규칙을 지정하는데 사용됨
  * 제한 조건과 데이터 조치 사이에 위반이 있으면, 제한 조건에 의해 조치가 중단됨
  * CREATE TABLE. 내에서 테이블이 작성되거나 테이블이 작성된 후에 (ALTER TABLE.에서) 제한 조건을 지정할 수 있다.
```
CREATE TABLE table_name
(
column_name1 data_type(size) constraint_name,
column_name2 data_type(size) constraint_name,
column_name3 data_type(size) constraint_name,
....
);
```
  * Kinds of constraints
> NOT NULL - 열이 NULL 값을 저장할 수 없음을 나타냅니다
UNIQUE - 열의 각 행은 고유 한 값을 가져야한다는 보장
PRIMARY KEY -에 NULL과 UNIQUE NOT의 조합. 열 (또는 두 개 이상의 열 조합)이 테이블의 특정 레코드를보다 쉽고 빠르게 찾는 데 도움이되는 고유 한 ID를 갖도록 보장합니다.
FOREIGN KEY는 - 다른 테이블의 값과 일치하는 하나의 테이블에서 데이터의 참조 무결성을 보장합니다
CHECK는 - 컬럼의 값이 특정 조건을 충족 보장
DEFAULT는 - 열에 대한 디폴트 값을 지정합니다

- NOT NULL
  * 열이 NULL 값을 허용하지 않도록 한다.
  * 필드가 항상 값을 포함하도록 한다. 즉, 새 레코드를 삽입하거나 필드에 값을 추가하지 않고 레코드를 업데이트 할 수 있다.
```
CREATE TABLE PersonsNotNull
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255)
)
```
- UNIQUE
  * 데이터베이스 테이블의 각 레코드를 고유하게 식별한다.
  * unique 및 primary key 제약 조건은 둘 다 열 또는 열 집합의 고유성을 보장한다.
  * primary key 제약 조건에는 자동으로 unique 제약 조건이 정의되어 있다.
  * 테이블 당 unique 제약 조건을 많이 가질 수 있지만 테이블 당 하나의 primary key 제약 조건만 가질 수 있다.
```
CREATE TABLE Persons
(
P_Id int NOT NULL UNIQUE,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255)
)
```
- PRIMARY KEY
  * 데이터베이스 테이블의 각 레코드를 고유하게 식별한다.
  * 기본 키에는 unique 값이 있어야 한다.
  * 기본 키 열은 null 값을 포함할 수 없다.
  * 대부분의 테이블에는 기본 키가 있어야하며 각 테이블에는 기본 키가 하나만 있을 수 있다.
```
CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
PRIMARY KEY (P_Id)
)
```
- FOREIGN KEY
  * 한 테이블의 외부 키는 다른 테이블의 primary key를 가리킨다.
  * 테이블 간의 연결을 파괴하는 작업을 방지하는 데 사용된다.
  * 잘못된 데이터가 가리키는 테이블에 포함 된 값 중 하나 여야하므로 잘못된 데이터가 외부 키 열에 삽입되는 것을 방지한다.
```
CREATE TABLE Orders
(
O_Id int NOT NULL PRIMARY KEY,
OrderNo int NOT NULL,
P_Id int FOREIGN KEY REFERENCES Persons(P_Id)
)
```
- CHECK
  * 열에 배치할 수 있는 값 범위를 제한하는데 사용
  * 단일 열에 check 제한 조건을 정의하면 열에 대해 특정 값만 허용된다.
  * 테이블에 check 제한 조건을 정의하면 다른 행에 있는 값을 기반으로 행의 값을 제한 할 수 있다.
```
CREATE TABLE Persons
(
P_Id int NOT NULL CHECK (P_Id>0),
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255)
)
```
- DEFAULT
  * 열에 기본값을 삽입하는데 사용된다.
  * 다른 값을 지정하지 않으면 기본값이 모든 새 레코드에 추가된다.
```
CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255) DEFAULT 'Sandnes'
)
```
- CREATE INDEX
  * 테이블에 인덱스를 작성
  * 인덱스를 사용하면 데이터베이스 응용 프로그램에서 데이터를 빠르게 찾을 수 있다.(검색, 쿼리 속도를 높임)
_인덱스 테이블과 함께 업데이트 하는 것에는 더 많은 시간이 걸린다. 따라서 자주 검색 할 열 (및 테이블)에 대해서만 인덱스를 만들어야 한다._
```
CREATE INDEX index_name
ON table_name (column_name)

CREATE INDEX PIndex
ON Persons (LastName)
```
- DROP
  * 인덱스, 테이블 및 데이터베이스는 drop문을 사용하여 쉽게 삭제 / 제거 할 수 있다.
```
DROP INDEX index_name ON table_name
DROP TABLE table_name
DROP DATABASE database_name
테이블 내부의 데이터만 삭제는
TRUNCATE TABLE table_name
```
- ALTER
  * 기존 테이블의 열을 추가, 삭제 또는 수정
```
ALTER TABLE table_name
ADD column_name datatype

ALTER TABLE table_name
DROP COLUMN column_name
```
- AUTO INCREMENT
  * 자동 증가하는 새 레코드가 테이블에 삽입될 때 고유 번호가 생성되도록 함
```
CREATE TABLE Persons
(
ID int NOT NULL AUTO_INCREMENT,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
PRIMARY KEY (ID)
)
```
- VIEWS
  * sql문의 결과 세티를 기반으로 하는 가상 테이블
  * 실제 테이블과 마찬가지로 행과 열이 포함된다.
  * sql함수, where 및 join문을 뷰에 추가하고 데이터가 하나의 단일 테이블에서 오는 것처럼 데이터를 표시할 수 있다.
```
CREATE VIEW view_name AS
SELECT column_name(s)
FROM table_name
WHERE condition

CREATE VIEW [Current Product List] AS
SELECT ProductID,ProductName
FROM Products
WHERE Discontinued=No
```
- DATES
  * 날짜 작업시 가장 어려운 부분은 삽입하려는 날짜의 형식이 데이터베이스의 날짜 열 형식과 일치하는지 확인하는 것이다.
  * Mysql 날짜 함수
  >_Function Description_
  NOW()	Returns the current date and time
  >CURDATE()	Returns the current date
  CURTIME()	Returns the current time
  DATE()	Extracts the date part of a date or date/time expression
  EXTRACT()	Returns a single part of a date/time
  DATE_ADD()	Adds a specified time interval to a date
  DATE_SUB()	Subtracts a specified time interval from a date
  DATEDIFF()	Returns the number of days between two dates
  DATE_FORMAT()	Displays date/time data in different formats

```
SELECT * FROM Orders WHERE OrderDate='2008-11-11'
```
- NULL VALUES
  * 알 수 없는 데이터가 누락되었음을 나태낸다.
  * 기본적으로 테이블 열은 null값을 포함할 수 있다.
```
SELECT LastName,FirstName,Address FROM Persons
WHERE Address IS NULL

SELECT LastName,FirstName,Address FROM Persons
WHERE Address IS NOT NULL
```
- DATA TYPES
  * 열에 포함될 수 있는 값의 종류
  * 데이터베이스 테이블의 각 열에는 이름과 데이터 유형이 있어야 한다.
  * SQL 개발자는 SQL 테이블을 작성할 때 각 테이블 열에 저장된 데이터 유형을 결정해야 한다. 데이터 유형은 각 컬럼 내부에서 예상되는 데이터 유형을 이해하기위한 SQL의 지침 및 레이블이며 SQL이 저장된 데이터와 상호 작용하는 방법을 식별한다.
  * sql의 일반 데이터 형식
  >Data type	Description
  CHARACTER(n)	Character string. Fixed-length n
  VARCHAR(n) or
  CHARACTER VARYING(n)	Character string. Variable length. Maximum length n
  BINARY(n)	Binary string. Fixed-length n
  BOOLEAN	Stores TRUE or FALSE values
  VARBINARY(n) or
  BINARY VARYING(n)	Binary string. Variable length. Maximum length n
  INTEGER(p)	Integer numerical (no decimal). Precision p
  SMALLINT	Integer numerical (no decimal). Precision 5
  INTEGER	Integer numerical (no decimal). Precision 10
  BIGINT	Integer numerical (no decimal). Precision 19
  DECIMAL(p,s)	Exact numerical, precision p, scale s. Example: decimal(5,2) is a number that has 3 digits before the decimal and 2 digits after the decimal
  NUMERIC(p,s)	Exact numerical, precision p, scale s. (Same as DECIMAL)
  FLOAT(p)	Approximate numerical, mantissa precision p. A floating number in base 10 exponential notation. The size argument for this type consists of a single number specifying the minimum precision
  REAL	Approximate numerical, mantissa precision 7
  FLOAT	Approximate numerical, mantissa precision 16
  DOUBLE PRECISION	Approximate numerical, mantissa precision 16
  DATE	Stores year, month, and day values
  TIME	Stores hour, minute, and second values
  TIMESTAMP	Stores year, month, day, hour, minute, and second values
  INTERVAL	Composed of a number of integer fields, representing a period of time, depending on the type of interval
  ARRAY	A set-length and ordered collection of elements
  MULTISET	A variable-length and unordered collection of elements
  XML	Stores XML data

- SQL COMMENTS
  * 주석을 사용하여 SQL문의 섹션을 설명할 수 있다.
```
--Select all:
SELECT * FROM Customers;

/*Select all the columns
of all the records
in the Customers table:*/
SELECT * FROM Customers;

SELECT CustomerName, /*City,*/ Country FROM Customers;
