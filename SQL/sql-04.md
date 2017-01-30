#### SQL Function

- SQL은 데이터에 대한 계산을 수행하는 많은 내장 함수를 가지고 있다.

- SQL 집계 함수
  * AVG () - 평균값을 반환합니다.
  * COUNT () - 행 수를 반환합니다.
  * FIRST () - 첫 번째 값을 반환합니다.
  * LAST () - 마지막 값을 반환합니다.
  * MAX () - 가장 큰 값을 반환합니다.
  * MIN () - 가장 작은 값을 반환합니다.
  * SUM () - 합계를 반환합니다.

- SQL 스칼라 함수
: 입력 값을 기반으로 단일 값을 리턴합니다.
  * UCASE () - 필드를 대문자로 변환합니다.
  * LCASE () - 필드를 소문자로 변환합니다.
  * MID () - 텍스트 필드에서 문자 추출
  * LEN () - 텍스트 필드의 길이를 반환합니다.
  * ROUND () - 숫자 필드를 지정된 소수 자릿수로 반올림합니다.
  * NOW () - 현재 시스템 날짜와 시간을 반환합니다.
  * FORMAT () - 필드가 표시되는 방식을 지정합니다.

- AVG() 함수
: 숫자 열의 평균값을 반환한다.
```
SELECT AVG(column_name) FROM table_name
```
- COUNT()
: 지정된 기준과 일치하는 행 수를 반환한다.
```
SELECT COUNT(column_name) FROM table_name;

SELECT COUNT(*) FROM table_name;
테이블의 레코드 수를 반환

SELECT COUNT(DISTINCT column_name) FROM table_name;
지정된 열의 고유 값 수를 반환
```
- FIRST()
: 선택한 열의 첫 번째 값을 반환
```
SELECT FIRST(column_name) FROM table_name;

SELECT TOP 1 column_name FROM table_name
ORDER BY column_name ASC;

SELECT FIRST(CustomerName) AS FirstCustomer FROM Customers;
직접 해보기»
```
- LAST()
: 선택한 열의 마지막 값을 반환한다.
```
SELECT LAST(column_name) FROM table_name;

SELECT TOP 1 column_name FROM table_name
ORDER BY column_name DESC;

SELECT LAST(CustomerName) AS LastCustomer FROM Customers;
직접 해보기»
```
- MAX()
: 선택된 열의 가장 큰 값을 반환한다.
```
SELECT MAX(column_name) FROM table_name;
```
- MIN()
: 선택된 열의 가장 작은 값을 반환한다.
```
SELECT MIN(column_name) FROM table_name;
```
- SUM()
: 숫자 열의 총 합계를 반환한다.
```
SELECT SUM(column_name) FROM table_name;
```
- GROUP BY
: 집계 함수와 함께 사용되어 결과 집합을 하나 이상의 열로 그룹화한다.
```
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name;
```
- HAVING
: where 키워드를 집계 함수와 함께 사용할 수 없으므로 Having절이 sql에 추가되었다.
```
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
HAVING aggregate_function(column_name) operator value;
```
- UCASE()
: 필드 값을 대문자로 변환한다.
```
SELECT UCASE(column_name) FROM table_name;
```
- LCASE()
: 필드 값을 소문자로 변환
```
SELECT LCASE(column_name) FROM table_name;
```
- MID()
: 텍스트 필드에서 문자를 추출하는데 사용
```
SELECT MID(column_name,start,length) AS some_name FROM table_name;
```
- LEN ()
: 텍스트 필드에 값의 길이를 반환한다.
```
SELECT LEN(column_name) FROM table_name;
```
- ROUND()
: 숫자 필드를 지정된 소수 자리로 반올림하는데 사용
```
SELECT ROUND(column_name,decimals) FROM table_name;

SELECT ProductName, ROUND(Price,0) AS RoundedPrice
FROM Products;
```
- NOW()
: 현재 시스템 날짜와 시간을 반환
```
SELECT NOW() FROM table_name;
```
- FORMAT()
: 필드 표시 방법을 형식화 한다
```
SELECT FORMAT(column_name,format) FROM table_name;

SELECT ProductName, Price, FORMAT(Now(),'YYYY-MM-DD') AS PerDate
FROM Products;
```
