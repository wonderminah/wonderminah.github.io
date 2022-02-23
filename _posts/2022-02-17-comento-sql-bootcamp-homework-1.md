---
title: "코멘토 SQL 입문부터 활용까지 - 데이터 분석 보고서 작성과 대시보드 개발 - 1주차 과제"
date: 2022-02-17 01:59:00 +0900
toc: true
toc_icon: bars
toc_sticky: true
comments: true
tags: [comento-bootcamp, sql]
---

# 1번 문제

Country 별로 ContactName이 ‘A’로 시작하는 Customer의 숫자를 세는 쿼리를 작성하세요.

* 배울 점: COUNT(*)과 COUNT(1)

## 내 답안

```sql
SELECT
    Country
    , COUNT(*) as CustomersCountLikeA -- Customer의 숫자
FROM Customers
WHERE ContactName LIKE 'A%' -- ContactName이 'A'로 시작하는
GROUP BY Country -- Contry 별로
```

![image-20220217020112226](https://wonderminah.github.io/assets/img/image-20220217020112226.png)

## 예시 답안

```sql
SELECT
    Country
    , COUNT(1) cnt
FROM Customers
WHERE ContactName LIKE 'A%'
GROUP BY Country;
```

![image-20220217021517909](https://wonderminah.github.io/assets/img/image-20220217021517909.png)

## 차이점

* 내 답안: COUNT(*)을 사용
* 리드멘토님 예시 답안: COUNT(1)을 사용

**COUNT(*)과 COUNT(1)의 차이?**

* count(*): NULL 값에 상관없이 모든 행을 카운트한다.
* count(1): NULL 값이 들어간 행은 카운트하지 않는다.

이 쿼리 결과에서는 COUNT의 값이 NULL인 경우는 없기에, 카운트 결과 숫자의 차이는 없다.

# 2번 문제

Customer 별로 Order한 Product의 총 Quantity를 세는 쿼리를 작성하세요.

* 배울 점: JOIN, GROUP BY

## 내 답안

```sql
SELECT
    O.CustomerID
    , SUM(OD.Quantity) AS SumQuantity -- Order한 Product의 총 Quantity
FROM OrderDetails OD
LEFT JOIN Orders O ON OD.OrderID = O.OrderID
GROUP BY O.CustomerID -- Customer 별로
```

![image-20220217020820947](https://wonderminah.github.io/assets/img/image-20220217020820947.png)

## 예시 답안

```sql
SELECT
    a.CustomerID
    , SUM(b.Quantity)
FROM Orders a
LEFT JOIN OrderDetails b on a.OrderId = b.OrderId
GROUP BY a.CustomerID;
```

![image-20220217021635943](https://wonderminah.github.io/assets/img/image-20220217021635943.png)

## 차이점

* 내 답안: OrderDetails 테이블을 FROM절에 두고, Orders 테이블을 LEFT JOIN함
* 리드멘토님 예시 답안: Orders 테이블을 FROM절에 두고, OrderDetails 테이블을 LEFT JOIN함

**두 테이블을 JOIN할 경우 FROM절과 JOIN절의 위치에 따른 차이 / 각 절에 두어야 하는 테이블은?**

<strong style="color: red;">TODO</strong>

# 3번 문제

년월별, Employee별로 Product를 몇 개씩 판매했는지를 표시하는 쿼리를 작성하세요.

* 배울 점: DATE_FORMAT()

## 내 답안

```sql
SELECT
    DATE_FORMAT(O.OrderDate, '%Y-%m') AS 'YearMonth'
    , E.EmployeeID
    , COUNT(DISTINCT OD.ProductID) AS 'DistinctCountOfProducts'
FROM Orders O
LEFT JOIN OrderDetails OD ON O.OrderID = OD.OrderID
LEFT JOIN Employees E ON O.EmployeeID = E.EmployeeID
GROUP BY YearMonth, EmployeeID
ORDER BY YearMonth ASC, EmployeeID ASC
```

![image-20220217021935851](https://wonderminah.github.io/assets/img/image-20220217021935851.png)

## 예시 답안

```sql
SELECT
    SUBSTR(a.OrderDate,1,7) ym
    , a.EmployeeID
    , SUM(b.Quantity) sumOfQuantity
FROM Orders a
LEFT JOIN OrderDetails b ON a.OrderID = b.OrderID
```

![image-20220217022116907](https://wonderminah.github.io/assets/img/image-20220217022116907.png)

## 차이점

* 'Product를 몇 개씩 판매했는지'에 대한 해석
  * 나의 경우 Product의 종류 수로 해석하여 COUNT(DISCOUNT ProductID)를 사용
  * 리드멘토님의 경우 Product의 총 수량으로 해석하여 SUM(Quantity)를 사용

위 차이점에 대해서는, 해석 상의 문제이니 의도대로 집계한 것이라면 문제가 없다고 하셨다.

* EmployeeID를 SELECT하는 기준 테이블에 대해
  * 나의 경우 SELECT Employees.EmployeeID
  * 리드멘토님의 경우 Orders.EmployeeID

이에 대해서는 별다른 피드백은 없으셨으나, Orders 테이블에도 EmployeeID가 있었으므로,   
굳이 별도로 LEFT JOIN Employees 을 할 필요는 없었다고 생각된다.
