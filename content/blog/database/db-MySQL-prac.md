---
title: db MySQL prac
date: 2020-12-31 11:22:39
category: "database"
draft: false
---

# MySQL 연습

## quiz 1

![mysql_quiz_01-1](C:\Users\Jung\Desktop\frontend\Database\quiz\pdf2png\mysql_quiz_01\mysql_quiz_01-1.png)

![mysql_quiz_01-2](C:\Users\Jung\Desktop\frontend\Database\quiz\pdf2png\mysql_quiz_01\mysql_quiz_01-2.png)

![mysql_quiz_01-3](C:\Users\Jung\Desktop\frontend\Database\quiz\pdf2png\mysql_quiz_01\mysql_quiz_01-3.png)

```mysql
# quiz1
#1
use sakila;
select country.country,COUNT(customer.customer_id)
from city,country, address,customer
WHERE city.country_id = country.country_id AND city.city_id= address.city_id AND address.address_id = customer.customer_id
AND country.country = "India"
GROUP BY country.country;


#2
SELECT name, population
FROM world.city
WHERE population > 1000000 AND countryCode ="KOR";

#3
SELECT name, countrycode, population
FROM world.city
WHERE population between 8000000 AND 10000000;

#4
use world;
SELECT code, Name,indepYear, continent, population
FROM country
WHERE indepYear between 1941 and 1949
ORDER BY indepYear asc;

#5
SELECT countrycode, language, percentage
FROM countrylanguage
WHERE language in ("Korean", "English", "Spanish") AND percentage >= 95
ORDER BY percentage DESC;

#6
SELECT code, name, continent, governmentForm, population
FROM country
WHERE code like "A%" AND governmentForm like "%Republic%";

#7
SELECT first_name, COUNT(first_name) as count
FROM sakila.actor
GROUP BY first_name
HAVING first_name ="DAN";

#8
SELECT film_id title, description
FROM sakila.film_text
WHERE TITLE like "%ICE%" and description like "%Drama%";

#9
SELECT title, description,category, length, price
FROM sakila.film_list
WHERE price between 1 and 4 AND length >= 180 AND category not in ("Sci-Fi","Animation");

```

## quiz 2
