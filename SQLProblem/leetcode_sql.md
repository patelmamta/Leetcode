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

16. [1251. Average Selling Price](https://leetcode.com/problems/average-selling-price/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
    p.product_id,
    ROUND(IFNULL(SUM(p.price * u.units)/SUM(u.units), 0), 2) as average_price
    FROM Prices p
    LEFT JOIN
    UnitsSold u
    ON u.purchase_date
    BETWEEN p.start_date AND p.end_date
    AND p.product_id = u.product_id
    GROUP BY product_id;
```

17. [1075. Project Employees I](https://leetcode.com/problems/project-employees-i/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
  project_id,
  ROUND(AVG(e.experience_years), 2) as average_years
FROM Project p
JOIN Employee e
ON e.employee_id = p.employee_id
GROUP BY p.project_id;
```

18. [1633. Percentage of Users Attended a Contest](https://leetcode.com/problems/percentage-of-users-attended-a-contest/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
WITH UserCount AS (
    SELECT COUNT(*) AS count FROM Users
)
SELECT
    r.contest_id,
    ROUND((COUNT(r.user_id)/ (SELECT count from UserCount)) * 100, 2) AS percentage
FROM Register r
GROUP BY r.contest_id
ORDER BY percentage DESC, r.contest_id ASC;
```

19. [1211. Queries Quality and Percentage](https://leetcode.com/problems/queries-quality-and-percentage/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
  DISTINCT(query_name) AS query_name,
  ROUND(SUM(rating/position)/count(query_name), 2) AS quality,
  ROUND((SUM(IF(rating < 3, 1, 0)) * 100) / count(query_name),2) AS poor_query_percentage
FROM Queries
GROUP BY query_name;
```

20. [1193. Monthly Transactions I](https://leetcode.com/problems/monthly-transactions-i/description/?envType=study-plan-v2&envId=top-sql-50) - (Medium)

```
SELECT
    DATE_FORMAT(trans_date, '%Y-%m') AS month,
    country,
    COUNT(id) AS trans_count,
    SUM(IF(state = 'approved', 1, 0)) AS approved_count,
    SUM(amount) AS trans_total_amount,
    SUM(IF(state = 'approved', amount, 0)) AS approved_total_amount
FROM Transactions
GROUP BY month, country;
```

21. [1174. Immediate Food Delivery II](https://leetcode.com/problems/immediate-food-delivery-ii/description/?envType=study-plan-v2&envId=top-sql-50) - (Medium)

```
WITH ImmediateOrders AS (
  SELECT
    customer_id,
    MIN(order_date) AS min_order
  FROM Delivery
  GROUP BY customer_id
)
SELECT
  ROUND(SUM(IF(i.min_order=d.customer_pref_delivery_date, 1, 0)) * 100.0 / COUNT(*), 2) AS immediate_percentage
FROM Delivery d
JOIN ImmediateOrders i ON d.order_date = i.min_order
AND  d.customer_id = i.customer_id;
```

22. [550. Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv/description/?envType=study-plan-v2&envId=top-sql-50) - (Medium)

```
WITH FirstLogin AS (
  SELECT
    MIN(event_date) as event_date,
    player_id
  FROM Activity
  GROUP BY player_id
)

SELECT
  ROUND(count(*) / (SELECT count(*) FROM FirstLogin), 2) AS fraction
FROM FirstLogin a
JOIN Activity b
ON a.player_id = b.player_id
AND DATEDIFF(b.event_date, a.event_date) = 1;
```

23. [2356. Number of Unique Subjects Taught by Each Teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
  teacher_id,
  COUNT(DISTINCT(subject_id)) AS cnt
FROM Teacher
GROUP BY teacher_id;
```

24. [1141. User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
  activity_date AS day,
  count(DISTINCT(user_id)) AS active_users
FROM
  Activity
WHERE
  activity_date BETWEEN '2019-06-28' AND '2019-07-27'
GROUP BY
  activity_date;
```

25. [1070. Product Sales Analysis III](https://leetcode.com/problems/product-sales-analysis-iii/description/?envType=study-plan-v2&envId=top-sql-50) - (Medium)

```
WITH FirstYear AS (
  SELECT
    product_id,
    MIN(year) AS first_year
  FROM Sales
  GROUP BY product_id
)

SELECT
  product_id,
  year AS first_year,
  quantity,
  price
FROM
  Sales
WHERE
  (product_id, year) IN (
SELECT
  product_id,
  first_year
FROM
  FirstYear
);
```

26. [596. Classes With at Least 5 Students](https://leetcode.com/problems/classes-with-at-least-5-students/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
  class
FROM
  Courses
GROUP BY class
HAVING count(student) >= 5;
```

27. [1729. Find Followers Count](https://leetcode.com/problems/find-followers-count/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
  user_id,
  count(follower_id) AS followers_count
FROM
  Followers
GROUP BY
  user_id
ORDER BY
  user_id;
```

28. [619. Biggest Single Number](https://leetcode.com/problems/biggest-single-number/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
WITH SingleNumbers AS (SELECT
  num
FROM
  MyNumbers
GROUP BY num
HAVING COUNT(num) = 1
)

SELECT
  MAX(num) AS num
FROM
  SingleNumbers;
```

29. [1045. Customers Who Bought All Products](https://leetcode.com/problems/customers-who-bought-all-products/description/?envType=study-plan-v2&envId=top-sql-50) - (Medium)

```
SELECT
  c.customer_id
FROM
  Customer c
GROUP BY customer_id
HAVING
  COUNT(DISTINCT(c.product_key)) = (SELECT COUNT(*) FROM Product);
```

30. [1731. The Number of Employees Which Report to Each Employee](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
    e.employee_id,
    e.name,
    COUNT(m.employee_id) as reports_count,
    ROUND(AVG(m.age), 0) as average_age
FROM
    Employees e
JOIN
    Employees m
ON
    e.employee_id = m.reports_to
GROUP BY m.reports_to
ORDER BY e.employee_id;
```

31. [1789. Primary Department for Each Employee](https://leetcode.com/problems/primary-department-for-each-employee/description/?envType=study-plan-v2&envId=top-sql-50) - (Easy)

```
SELECT
    employee_id,
    department_id
FROM
    Employee
WHERE
    primary_flag = 'Y'  OR (department_id, employee_id) IN (
        SELECT
            department_id,
            employee_id
        FROM Employee
        GROUP BY employee_id
        HAVING(count(department_id) = 1)
    );
```
