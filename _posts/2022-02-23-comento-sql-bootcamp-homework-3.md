---
title: "코멘토 SQL 입문부터 활용까지 - 데이터 분석 보고서 작성과 대시보드 개발 - 3주차 과제"
date: 2022-02-23 17:00:00 +0900
toc: true
toc_icon: bars
toc_sticky: true
comments: true
tags: [comento-bootcamp, sql]
---

# 과제 주제

**Northwind 데이터 분석 보고서 작성**

Northwind 데이터에 대한 가설을 3개 정하고, 그 가설에 대한 핵심 지표 및 보조 지표를 설정한 뒤, 그 지표를 분석해 가설에 대한 분석 보고서를 PowerPoint나 Word로 작성해 주세요. 각 가설은 서로 연결되는 하나의 흐름을 가져야 합니다.

**'가설 수립 > 가설을 검증하기 위한 지표 선정 > 지표 측정 및 분석 > 분석 결과 및 결론(인사이트)'** 의 순서를 꼭 지켜주세요.

# 과제 수행 내용

수행 전에 데이터베이스에서 모르는 것

* standard cost
* list cost
* reorder level
* target level

## 가설 수립

구매 직무의 고객이 주문량이 많을 것이다. (c.job_title)

```sql
select
    c.job_title
    , count(*)
from orders o 
left join customers c on o.customer_id = c.id
group by c.job_title
```

최소 주문금액이 높을수록 재구매율이 낮을 것이다. p.minimum_reorder_quantity가 낮을수록 재구매율이 높다.

```sql
```

배송기간이 빠른 업체일수록 판매량이 높을 것이다.

```sql
```

## 1

### 가설 수립

2분기 맥주의 주문량(혹은 총 판매금액)은 1분기 대비 증가하였을 것이다.

### 가설을 검증하기 위한 지표 선정

분기별 맥주 판매량

### 지표 측정 및 분석

```sql
select 
    quarter(o.order_date) as quarter -- 분기
    , count(*) as order_count -- 주문량
from orders o 
left join order_details od on od.order_id = o.id
left join products p on p.id = od.product_id
where p.id = 34 -- 맥주
group by quarter -- 분기별로 집계
```

![image-20220223220025679](/Users/minah.kim/Library/Application Support/typora-user-images/image-20220223220025679.png)

### 분석 결과 및 결론(인사이트)

* 분석 결과: 2분기의 맥주 판매량은 1분기 대비 100% 증가
* 결론(인사이트): 2분기의 맥주 판매량 증가에 대비하여, 2분기 도달 전 맥주의 재고를 사전에 확보할 수 있도록 한다.



* 상품별
  * 최소 주문금액
* 지불방법별
  * cash
  * credit card
  * check
* 직원별
* 고객별
  * 구매 직무 고객의 총 구매금액이 그렇지 않은 고객의 총 구매금액 보다 높을 것이다.
* 공급업체별
  * 평균 배송기간이 짧은 업체의 



* sales_report
  * 제품 카테고리(category)에 따른 판매율
  * 나라/지역(country, region)에 따른 판매율
  * 고객 특성(customer)에 따른 구매율
  * 세일즈 직원(employee)에 따른 판매율
  * 제품(products)에 따른 판매율
    * 가설: 
    * (?) reorder_level이랑 products.target_level은 뭐지?

## 가설을 검증하기 위한 지표 선정

## 지표 측정 및 분석

## 분석 결과 및 결론(인사이트)