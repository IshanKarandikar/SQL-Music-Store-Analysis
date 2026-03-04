# 🎵 Music Store SQL Analysis

## Project Overview
This project analyzes a digital music store database using **PostgreSQL** to answer real business questions across sales, customer behavior, and music trends. The analysis covers 11 business questions across two difficulty levels using SQL concepts including JOINs, CTEs, Window Functions, Subqueries, and Aggregate Functions.

---

## Database Schema

![Schema](images/Screenshot%202026-03-03%20170223.png)

---

## Tools Used
- **PostgreSQL 18** — Database and query execution
- **pgAdmin 4** — Query editor and visualization
- **GitHub** — Version control and project hosting

---

## Business Questions Solved

### 🔴 Medium Level

**Q1: Find email, first name, last name of all Rock band listeners arranged alphabetically.**

![MQ1](images/LM%20Q1.png)

```sql
SELECT DISTINCT c.email, c.first_name, c.last_name
FROM customer c
JOIN invoice i ON c.customer_id = i.customer_id
JOIN invoice_line l ON i.invoice_id = l.invoice_id
WHERE l.track_id IN (
  SELECT track_id FROM track t
  JOIN genre g ON t.genre_id = g.genre_id
  WHERE g.name = 'Rock'
)
ORDER BY c.first_name;
```

> **Answer:** 59 Rock listeners found, sorted alphabetically.

---

**Q2: Which artists have written the most Rock music? Return top 10.**

![MQ2](images/LM%20Q2.png)

```sql
SELECT artist.artist_id, artist.name,
COUNT(artist.artist_id) AS number_of_songs
FROM track
JOIN album ON album.album_id = track.album_id
JOIN artist ON artist.artist_id = album.artist_id
JOIN genre ON genre.genre_id = track.genre_id
WHERE genre.name = 'Rock'
GROUP BY artist.artist_id
ORDER BY number_of_songs DESC
LIMIT 10;
```

> **Answer:** Led Zeppelin leads with 114 Rock tracks, followed by U2 with 112.

---

**Q3: Return names of tracks whose length is above average.**

![MQ3](images/LM%20Q3.png)

```sql
WITH avg_length AS (
  SELECT AVG(milliseconds) AS avg_duration
  FROM track
)
SELECT name, milliseconds
FROM avg_length, track
WHERE avg_duration < milliseconds
ORDER BY milliseconds DESC;
```

> **Answer:** 494 tracks above average duration. Longest is "Occupation / Precipice" at 5,286,953 ms.

---

**Q4: Who are the top 3 highest spending customers in each country?**

![MQ4](images/LM%20Q4.png)

```sql
WITH ranked AS (
  SELECT billing_country, customer_id,
  SUM(total) AS total_amount,
  RANK() OVER (PARTITION BY billing_country ORDER BY SUM(total) DESC) AS rnk
  FROM invoice
  GROUP BY billing_country, customer_id
)
SELECT customer_id, billing_country, rnk, total_amount
FROM ranked
WHERE rnk <= 3;
```

> **Answer:** 39 rows returned showing top 3 spenders per country.

---

**Q5: Find the most popular music genre for each country.**

![MQ5](images/LM%20Q5.png)

```sql
WITH popular_genre AS (
  SELECT COUNT(il.quantity) AS purchases,
  c.country, g.name,
  ROW_NUMBER() OVER (PARTITION BY c.country
  ORDER BY COUNT(il.quantity) DESC) AS rnk
  FROM invoice_line il
  JOIN invoice i ON i.invoice_id = il.invoice_id
  JOIN customer c ON c.customer_id = i.customer_id
  JOIN track t ON t.track_id = il.track_id
  JOIN genre g ON g.genre_id = t.genre_id
  GROUP BY c.country, g.name
)
SELECT * FROM popular_genre WHERE rnk <= 1;
```

> **Answer:** Rock is the most popular genre in most countries.

---

**Q6: Find the customer that has spent the most money in each country.**

![MQ6](images/LM%20Q6.png)

```sql
WITH customer_spend AS (
  SELECT c.customer_id, c.first_name, c.last_name,
  c.country, SUM(i.total) AS total_spent,
  RANK() OVER (PARTITION BY c.country
  ORDER BY SUM(i.total) DESC) AS rnk
  FROM customer c
  JOIN invoice i ON c.customer_id = i.customer_id
  GROUP BY c.customer_id, c.first_name, c.last_name, c.country
)
SELECT first_name, last_name, country, total_spent
FROM customer_spend
WHERE rnk = 1
ORDER BY country;
```

> **Answer:** 24 countries covered. Luis Gonçalves leads Brazil with 108.89.

---

### 🟡 Easy Level

**Q1: Who is the senior most employee based on job title?**

![Q1](images/LE%20Q1.png)

> **Answer:** Madan Mohan is the Senior Most Employee.

---

**Q2: Which countries have the most invoices?**

![Q2](images/LE%20Q2.png)

> **Answer:** USA has the most invoices with 131.

---

**Q3: What are the top 3 values of total invoice?**

![Q3](images/LE%20Q3.png)

> **Answer:** Top invoice value is 23.75 from France.

---

**Q4: Which city has the best customers?**

![Q4](images/LE%20Q4.png)

> **Answer:** Prague has the best customers with total invoice value of 273.24.

---

**Q5: Who is the best customer based on total spending?**

![Q5](images/L5%20Q5.png)

> **Answer:** R Madhav is the best customer from Prague with total value of 144.54.

---

## Key SQL Concepts Used

| Concept | Questions |
|---|---|
| SELECT, WHERE, ORDER BY, LIMIT | All questions |
| Aggregate Functions (SUM, COUNT, AVG) | LE Q2, Q4, Q5, LM Q2, Q3, Q4 |
| GROUP BY | LE Q2, Q4, Q5, LM Q2, Q4, Q5, Q6 |
| INNER JOIN / JOIN | LE Q5, LM Q1, Q2, Q4, Q5, Q6 |
| Subquery | LM Q1 |
| CTE (WITH clause) | LM Q3, Q4, Q5, Q6 |
| Window Functions RANK() / ROW_NUMBER() | LM Q4, Q5, Q6 |
| DISTINCT | LM Q1 |

---

## Key Business Insights

- 🏙️ **Prague** generates the highest revenue — best city for a music festival
- 🇺🇸 **USA** dominates with 131 invoices — largest customer base
- 🎸 **Rock** is the most popular genre across majority of countries
- 🎵 **Led Zeppelin** has the most Rock tracks (114) in the store
- 👑 **R Madhav** is the single best customer with $144.54 total spending
- 🌍 Top spenders identified per country for targeted marketing campaigns

---

## Author
**Ishan Karandikar**
MBA Business Analytics — University Canada West, Vancouver BC
