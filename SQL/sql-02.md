- INJECTION
  * 데이터베이스를 파괴할 수 있다.
  * 악의적인 사용자가 웹페이지 입력을 통해 SQL 명령문에 SQL 명령을 주입할 수 있는 기술이다. 삽입된 SQL명령은 SQL문을 변경하고 웹 응용 프로그램의 보안을 손상시킬 수 있다.
  * 1 = 1에 기반한 SQL 주입은 항상 참이다.
  * ''''=''''에 기반한 SQL삽입은 항상 참이다.
  _SQL 주입 공격으로부터 웹사이트를 보호하는 유일한 입증된 방법은 SQL 매개 변수를 사용하는 것이다. SQL 매개 변수는 실행 시간에 제어된 방식으로 SQL 쿼리에 추가되는 값이다._

예시)
```
txtUserId = getRequestString("UserId");
txtSQL = "SELECT * FROM Users WHERE UserId = @0";
db.Execute(txtSQL,txtUserId);
```
- SELECT TOP
  * 리턴할 레코드 수를 지정하는데 사용
  * 수천 개의 레코드가 있는 큰 테이블에서 매우 유용할 수 있다.
```
SELECT TOP number|percent column_name(s)
FROM table_name;
```
- LIKE
  * WHERE 절에서 열의 지정된 패턴을 검색하는데 사용\
```
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern;
```
- 와일드카드
  * 문자열의 다른 문자를 대체할 수 있다.
  * sql like 연산자와 함께 사용
  * 테이블 내의 데이터 검색
  * 와일드 카드
```
SELECT * FROM Customers
WHERE City LIKE 'ber%';

SELECT * FROM Customers
WHERE City LIKE '%es%';

SELECT * FROM Customers
WHERE City LIKE '_erlin';

SELECT * FROM Customers
WHERE City LIKE '[bsp]%';

SELECT * FROM Customers
WHERE City LIKE '[!bsp]%';
```
- IN
  * where 절에 여러 값을 지정할 수 있다.
```
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1,value2,...);
```
- BETWEEN
  * 범위 내의 값을 선택하는데 사용. 값은 숫자, 텍스트, 또는 날짜 일 수 있다.
```
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20;
```
- Aliases
  * 테이블이나 열 머리글의 이름을 임시로 바꾸는데 사용됨
```
SELECT column_name AS alias_name
FROM table_name;

SELECT column_name(s)
FROM table_name AS alias_name;
```
- Joins
  * 두 개 이상의 테이블에서 행을 결합하는데 사용
```
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers
ON Orders.CustomerID=Customers.CustomerID;
```
- INNER Join
  * 두 테이블의 열이 일치하는 한 두 테이블의 모든 행을 선택한다.
```
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name=table2.column_name;

SELECT column_name(s)
FROM table1
JOIN table2
ON table1.column_name=table2.column_name;
```
- LEFT JOIN
  * 왼쪽 테이블의 모든 행과 오른쪽 테이블의 일치하는 행을 반환한다. 결과가 일치하지 않으면 오른쪽에 NULL이다.
```
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name=table2.column_name;

SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID=Orders.CustomerID
ORDER BY Customers.CustomerName;
```
- RIGHT JOIN
  * 왼쪽 테이블에 일치하는 행과 함께 오른쪽 테이블의 모든 행을 리턴한다. 결과가 일치하지 않으면 왼쪽에 NULL이다.

- FULL JOIN
  * 왼쪽 테이블과 오른쪽 테이블의 모든 행을 리턴한다. LEFT 및 RIGHT 조인의 결과를 결합한다.
```
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name=table2.column_name;
