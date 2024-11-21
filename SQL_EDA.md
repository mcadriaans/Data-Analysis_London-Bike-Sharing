# London bike sharing EDA 🚲

## Create table 
```sql
CREATE TABLE bike_sharing (
    timestamp TIMESTAMP,
    cnt INTEGER,
    t1 FLOAT,
    t2 FLOAT,
    wind_speed FLOAT,
    weather_code VARCHAR(30),
    is_holiday VARCHAR(5),
    is_weekend VARCHAR(5),
    season VARCHAR(25),
	humidity_percent FLOAT
);
```

### Verify table exists in PostgreSQL
```sql
SELECT * 
FROM bike_sharing
LIMIT 5;
```
![image](https://github.com/user-attachments/assets/5a300dfb-0714-424a-9e5b-871bcbfc1e52)

## Business Questions
### 1. What is the start and end date and duration of bike rental tracking in our data?
```sql
SELECT
 MIN(timestamp :: DATE) AS starting_date,
 MAX(timestamp :: DATE) AS end_date,
 (MAX(timestamp :: DATE) - MIN(timestamp :: DATE)) AS days_tracked
FROM bike_sharing;
```
![image](https://github.com/user-attachments/assets/bca1b66d-b791-4d46-a5ee-c708872aadf1)


### 2. What is the total amount of bike rentals during the 730 days?
```sql
SELECT
 SUM(cnt) AS total_bike_rentals
FROM bike_sharing;
```
![image](https://github.com/user-attachments/assets/edc78058-681b-45fb-88d2-2770dd12c6f7)


#### 2.1 What is the total amount of bike rentals per year?
```sql
SELECT
 EXTRACT(Year FROM timestamp) AS bs_year,
 SUM(cnt) AS bike_rentals_per_year
FROM bike_sharing
GROUP BY 1
ORDER BY 1;
```
![image](https://github.com/user-attachments/assets/32efa997-a734-4a62-bee2-ca7c67d253fa)


### 3. What are the top 5 days with the highest number of bike rentals?
```sql
SELECT
 timestamp :: DATE,
 TO_CHAR(timestamp :: DATE, 'Day') AS weekday,
 SUM(cnt) AS daily_bike_rentals
FROM bike_sharing
GROUP BY 1,2
ORDER BY 3 DESC
LIMIT 5;
```
![image](https://github.com/user-attachments/assets/41e599c5-22a1-479d-8339-a4e1e58f2ce5)

### 4. What was the most popular season for bike rentals in each year?
```sql
SELECT
 bs_year,
 season,
 bike_rentals_per_year
FROM(
 SELECT
  EXTRACT(Year FROM timestamp) AS bs_year,
  season,
  SUM(cnt) AS bike_rentals_per_year,
  RANK()OVER(
    PARTITION BY EXTRACT(Year FROM timestamp)
    ORDER BY SUM(cnt) DESC
  ) AS rnk
  FROM bike_sharing
  GROUP BY 1, 2
)
WHERE rnk = 1;
```
![image](https://github.com/user-attachments/assets/6b0377e7-6406-4eeb-98dd-dcf759fde30d)
### 5. Show the minimum, average and maximum actual daily temperatures.
```sql
SELECT
	timestamp::DATE AS bs_date,
	MIN(t1) AS min_daily_temp,
	ROUND(AVG(t1):: NUMERIC, 1) AS avg_daily_temp,
	MAX(t1) AS max_daily_temp
FROM bike_sharing
GROUP BY 1
ORDER BY 1;
```
![image](https://github.com/user-attachments/assets/e446d67a-86f2-4105-b206-326dc31b4797)

### 6. Find the 7-day moving average for total bike rentals
```sql
WITH daily_rentals AS(
SELECT
 timestamp :: DATE AS bs_date,
 SUM(cnt) AS total_bike_rentals
FROM bike_sharing
GROUP BY 1
ORDER BY 1
)
SELECT
 bs_date,
 total_bike_rentals,
 CASE WHEN ROW_NUMBER()OVER(ORDER BY bs_date) < 7 THEN NULL
 ELSE ROUND(AVG(total_bike_rentals) OVER(
  ORDER BY bs_date
  ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
  ), 2) END AS seven_day_moving_avg
FROM daily_rentals
ORDER BY 1;
```
![image](https://github.com/user-attachments/assets/2b3e5221-2d03-4bc5-93ec-16dfdc884671)
