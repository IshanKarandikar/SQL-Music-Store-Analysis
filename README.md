# 🎵 Music Store SQL Analysis

## Project Overview
This project analyzes a digital music store database using **PostgreSQL** to answer real business questions across sales, customer behavior, and music trends. The analysis covers 11 business questions across two difficulty levels using SQL concepts including JOINs, CTEs, Window Functions, Subqueries, and Aggregate Functions.

---

## Database Schema

![Schema]("C:\Users\cr7is\OneDrive\Pictures\Screenshots\Screenshot 2026-03-03 170223.png")

---

## Tools Used
- **PostgreSQL 18** — Database and query execution
- **pgAdmin 4** — Query editor and visualization
- **GitHub** — Version control and project hosting

---

## Business Questions Solved

### 🟡 Easy Level

**Q1: Who is the senior most employee based on job title?**

![Q1](images/LE_Q1.png)

> **Answer:** Madan Mohan is the Senior Most Employee.

---

**Q2: Which countries have the most invoices?**

![Q2](images/LE_Q2.png)

> **Answer:** USA has the most invoices with 131.

---

**Q3: What are the top 3 values of total invoice?**

![Q3](images/LE_Q3.png)

> **Answer:** Top invoice value is 23.75 from France.

---

**Q4: Which city has the best customers?**

![Q4](images/LE_Q4.png)

> **Answer:** Prague has the best customers with total invoice value of 273.24.

---

**Q5: Who is the best customer based on total spending?**

![Q5](images/L5_Q5.png)

> **Answer:** R Madhav is the best customer from Prague with total value of 144.54.

---

### 🔴 Medium Level

**Q1: Find email, first name, last name of all Rock band listeners arranged alphabetically.**

![MQ1](images/LM_Q1.png)

> **Answer:** 59 Rock listeners found, sorted alphabetically.

---

**Q2: Which artists have written the most Rock music? Return top 10.**

![MQ2](images/LM_Q2.png)

> **Answer:** Led Zeppelin leads with 114 Rock tracks, followed by U2 with 112.

---

**Q3: Return names of tracks whose length is above average.**

![MQ3](images/LM_Q3.png)

> **Answer:** 494 tracks are above average duration. Longest is "Occupation / Precipice" at 5,286,953 ms.

---

**Q4: Who are the top 3 highest spending customers in each country?**

![MQ4](images/LM_Q4.png)

> **Answer:** 39 rows returned showing top 3 spenders per country.

---

**Q5: Find the most popular music genre for each country.**

![MQ5](images/LM_Q5.png)

> **Answer:** Rock is the most popular genre in most countries.

---

**Q6: Find the customer that has spent the most money in each country.**

![MQ6](images/LM_Q6.png)

> **Answer:** 24 countries covered. Luis Gonçalves leads Brazil with 108.89.

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
[LinkedIn](https://linkedin.com/in/ishankarandikar)

---
*Project inspired by Rishabh Mishra's Music Store SQL Analysis*
