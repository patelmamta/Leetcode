
##  Leetcode Problems

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

 5. [1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/description/?envType=study-plan-v2&envId=top-sql-50) (Easy)


```
SELECT
    tweet_id
FROM
    Tweets
WHERE LENGTH(content) > 15;
```