Table: Weather

+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| recordDate    | date    |
| temperature   | int     |
+---------------+---------+
id is the column with unique values for this table.
There are no different rows with the same recordDate.
This table contains information about the temperature on a certain day.
 

Write a solution to find all dates' Id with higher temperatures compared to its previous dates (yesterday).

Return the result table in any order.

The result format is in the following example.

 

Example 1:

Input: 
Weather table:
+----+------------+-------------+
| id | recordDate | temperature |
+----+------------+-------------+
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |
+----+------------+-------------+
Output: 
+----+
| id |
+----+
| 2  |
| 4  |
+----+
Explanation: 
In 2015-01-02, the temperature was higher than the previous day (10 -> 25).
In 2015-01-04, the temperature was higher than the previous day (20 -> 30).


# Solution
Select ids where the temperature on that date is higher than the temperature from the previous day.

> Select 'id' from 'Weather' table.
> Perform a self-join on the 'Weather' table to match each row with the row from the previous day.
> Filter the returned result for rows where the temperature of the current day is greater than the temperature from the previous day.
> Return the 'id' column from the 'Weather' table meeting these conditions.

SELECT id
FROM Weather AS t1
JOIN Weather AS t2
ON t2.recordDate = DATE_SUB(t1.recordDate, INTERVAL 1 DAY)
WHERE t1.temperature > t2.temperature;
