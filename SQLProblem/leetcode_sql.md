## Leetcode Problems

1. [1757. Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/?envType=study-plan-v2&envId=top-sql-50") (Easy)

```
SELECT
    product_id
FROM Products
WHERE
    low_fats = "Y" AND recyclable = "Y";
```

2. [584. Find Customer Referee](https://leetcode.com/problems/find-customer-referee/description/?envType=study-plan-v2&envId=top-sql-50) (Easy)

```bash
SELECT
    name
FROM Customer
WHERE referee_id != 2 OR referee_id IS NULL;
```

3. [595. Big Countries](https://leetcode.com/problems/big-countries/description/?envType=study-plan-v2&envId=top-sql-50) (Easy)

```
SELECT
    name, population, area
FROM World
WHERE
    area >= 3000000 OR population >= 25000000;
```

4. [1148. Article Views I](https://leetcode.com/problems/article-views-i/description/?envType=study-plan-v2&envId=top-sql-50) (Easy)

```
SELECT
   DISTINCT(author_id) as id
FROM Views
WHERE
   viewer_id = author_id
ORDER BY author_id asc;
```

5.  [1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/description/?envType=study-plan-v2&envId=top-sql-50) (Easy)

```
SELECT
    tweet_id
FROM
    Tweets
WHERE LENGTH(content) > 15;
```

6. [1378. Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/description/?envType=study-plan-v2&envId=top-sql-50) (Easy)

```
SELECT
    unique_id,
    name
FROM Employees
LEFT JOIN EmployeeUNI ON
    Employees.id = EmployeeUNI.id;
```

7. [1068. Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
    p.product_name,
    s.year,
    s.price
FROM Sales s
LEFT JOIN
    Product p
ON p.product_id = s.product_id;
```

8. [1581. Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
    DISTINCT(customer_id),
    count(Visits.visit_id) as count_no_trans
FROM Visits
LEFT JOIN Transactions ON Visits.visit_id = Transactions.visit_id
WHERE Transactions.transaction_id is NULL
GROUP BY customer_id;
```

9. [197. Rising Temperature](https://leetcode.com/problems/rising-temperature/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
    w1.id
FROM
    Weather w1 INNER JOIN Weather w2
ON w1.recordDate > w2.recordDate
WHERE
    DATEDIFF(w1.recordDate, w2.recordDate) = 1
AND w1.temperature > w2.temperature;
```

10. [1661. Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
  a.machine_id,
  ROUND(AVG(b.timestamp - a.timestamp), 3) as processing_time
FROM  Activity a
INNER JOIN Activity b
ON a.process_id = b.process_id
AND a.machine_id = b.machine_id
AND a.activity_type = "start"
AND b.activity_type = 'end'
GROUP BY machine_id;
```

11. [577. Employee Bonus](https://leetcode.com/problems/employee-bonus/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
  name, bonus
FROM Employee e
LEFT JOIN Bonus b
ON e.empId = b.empId
WHERE b.bonus < 1000
OR b.bonus IS NULL;
```

12. [1280. Students and Examinations](https://leetcode.com/problems/students-and-examinations/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
    st.student_id, st.student_name, sb.subject_name,
    count(ex.student_id) as attended_exams
FROM Students st
CROSS JOIN Subjects sb
LEFT JOIN Examinations ex ON
    st.student_id = ex.student_id
AND
    ex.subject_name = sb.subject_name
GROUP BY
    st.student_id, sb.subject_name
ORDER BY
    st.student_id, sb.subject_name;
```

13. [570. Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/description/?envType=study-plan-v2&envId=top-sql-50) - (Medium)

```
SELECT
    m.name
FROM Employee m
JOIN Employee e ON
m.id = e.managerID
GROUP BY e.managerID
HAVING count(e.managerID) >= 5;

```

14. [1934. Confirmation Rate](https://leetcode.com/problems/confirmation-rate/description/?envType=study-plan-v2&envId=top-sql-50) - (Medium)

```
SELECT
    s.user_id,
    ROUND(
        IFNULL(
            SUM(c.action = 'confirmed') / COUNT(c.action),
         0),
    2) AS confirmation_rate
FROM Signups s
LEFT JOIN Confirmations c
ON s.user_id = c.user_id
GROUP BY s.user_id;
```

15. [620. Not Boring Movies](https://leetcode.com/problems/not-boring-movies/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
    id, movie, description, rating
FROM Cinema
WHERE description NOT LIKE '%boring%'
AND (id%2) != 0
ORDER BY rating DESC;
```
