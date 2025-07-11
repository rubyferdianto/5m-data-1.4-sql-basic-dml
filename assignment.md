# Assignment

## Brief

Write the SQL DML statements for the following questions.

## Instructions

Paste the answer as SQL in the answer code section below each question.

### Question 1

Select the minimum and maximum price per sqm of all the flats.

```sql
SELECT MIN(price_per_sqm) min_price_per_sqm, MAX(price_per_sqm) max_price_per_sqm
FROM (
	SELECT ROUND(resale_price / floor_area_sqm, 2) price_per_sqm
	FROM main.resale_flat_prices_2017)
```

### Question 2

Select the average price per sqm for flats in each town.

```sql
	SELECT town, ROUND(AVG(resale_price / floor_area_sqm), 2) avg_price_per_sqm
	FROM main.resale_flat_prices_2017
	GROUP BY town
	ORDER BY 1
```

### Question 3

Categorize flats into price ranges and count how many flats fall into each category:

- Under $400,000: 'Budget'
- $400,000 to $700,000: 'Mid-Range'
- Above $700,000: 'Premium'
  Show the counts in descending order.

```sql
 WITH q1 AS 
	(SELECT resale_price,
	       CASE  
	       		WHEN resale_price < 400000 THEN 'Budget'
	       		WHEN resale_price >= 400000 AND resale_price < 700000 THEN 'Mid-Range'
	       		ELSE 'Premium'
	       	END category
	FROM main.resale_flat_prices_2017)
SELECT category, COUNT(1) number_of_category
FROM q1
GROUP BY category 
ORDER BY 2 DESC
```

### Question 4

Count the number of flats sold in each town during the first quarter of 2017 (January to March).

```sql
	SELECT town, month, COUNT(1) number_of_sold 
	FROM main.resale_flat_prices_2017
	WHERE month BETWEEN '2017-01' AND '2017-03'
	GROUP BY town, month
	ORDER BY 1, 2
```

## Submission

- Submit the URL of the GitHub Repository that contains your work to NTU black board.
- Should you reference the work of your classmate(s) or online resources, give them credit by adding either the name of your classmate or URL.
