# Assignment

## Brief

Write the SQL statements for the following questions.

## Instructions

Paste the answer as SQL in the answer code section below each question.

### Question 1

Using the `claim` and `car` tables, write a SQL query to return a table containing `id, claim_date, travel_time, claim_amt` from `claim`, and `car_type, car_use` from `car`. Use an appropriate join based on the `car_id`.

Answer:

```sql
SELECT
    claim.id,
    claim.claim_date,
    claim.travel_time,
    claim.claim_amt,
    car.car_type,
    car.car_use
FROM
    claim
    LEFT JOIN car on claim.car_id = car.id;

```

### Question 2

Write a SQL query to compute the running total of the `travel_time` column for each `car_id` in the `claim` table. The resulting table should contain `id, car_id, travel_time, running_total`.

Answer:

```sql
SELECT
    id,
    car_id,claim_date,
    travel_time,
    SUM(travel_time) OVER (
        PARTITION BY
            car_id
        ORDER BY
            claim_date 
    ) AS running_total
FROM
    claim
```

### Question 3

Using a Common Table Expression (CTE), write a SQL query to return a table containing `id, resale_value, car_use` from `car`, where the car resale value is less than the average resale value for the car use.

Answer:

```sql
  
  with avg_resale_val_car_use as (
  select car_use, avg(resale_value) avg_resale_val
  from main.car 
  group by car_use
 )
 select c1.id, c1.resale_value, c1.car_use
 from car c1
 inner join avg_resale_val_car_use c2
 on c1.car_use = c2.car_use
 where c1.resale_value < c2.avg_resale_val;
```

## Submission

- Submit the URL of the GitHub Repository that contains your work to NTU black board.
- Should you reference the work of your classmate(s) or online resources, give them credit by adding either the name of your classmate or URL.
