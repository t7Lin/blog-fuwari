---
title: JOIN ON
published: 2025-06-30
description: SQL Learning Note_5
tags: 
  - SQL
category: Notes
draft: false
---

https://sqlzoo.net/wiki/The_JOIN_operation
## 🧩 核心概念

**JOIN ON** 是 SQL 中连接多个表的操作，基于两个表之间的**关联字段**建立关系：

```sql
SELECT 列...
FROM 表A
JOIN 表B ON 表A.关联列 = 表B.关联列
```

## 🔍 四大连接类型

| 连接类型           | 描述               | 示例                    | 结果特点           |
| -------------- | ---------------- | --------------------- | -------------- |
| **INNER JOIN** | 返回匹配的记录          | `JOIN...ON A.id=B.id` | 仅两表匹配的行        |
| **LEFT JOIN**  | 返回左表所有记录+匹配的右表记录 | `LEFT JOIN...ON...`   | 左表完整，右表可能为NULL |
| **RIGHT JOIN** | 返回右表所有记录+匹配的左表记录 | `RIGHT JOIN...ON...`  | 右表完整，左表可能为NULL |
| **FULL JOIN**  | 返回两个表所有记录        | `FULL JOIN...ON...`   | 两表完整，不匹配部分为NUL |
## 💡 最佳实践指南

### 1. 标准连接语法
```sql
SELECT orders.id, customers.name
FROM orders
INNER JOIN customers ON orders.customer_id = customers.id
```

### 2. 多表连接
```sql
SELECT o.order_date, c.name, p.product_name
FROM orders o
JOIN customers c ON o.customer_id = c.id
JOIN products p ON o.product_id = p.id
```

**经典例题：**
展示电影类型“Alien”的演员清单。
https://chat.deepseek.com/a/chat/s/56193c33-56e1-464c-9134-ad60c1f846e4

```sql
SELECT actor.name  -- 目标表：actor，我们想要演员名字
FROM movie   -- 过滤表：通过movie表过滤电影
JOIN casting ON movie.id = casting.movieid  -- 连接表：casting连接movie
JOIN actor ON actor.id = casting.actorid  -- 连接表：casting连接actor
WHERE title = 'Alien'  -- 过滤条件在movie表上
```
### 3. 复杂连接条件
```sql
SELECT *
FROM employees e
JOIN departments d ON e.dept_id = d.id AND d.location = 'NY'
```