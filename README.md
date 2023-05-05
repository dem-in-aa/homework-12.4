# Домашнее задание к занятию «SQL. Часть 2» Андрей Дёмин

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

```sql
select  concat(s.last_name, ' ', s.first_name) AS staff_name, c.city, COUNT(customer.customer_id)
from staff s
join  address a on  a.address_id   = s.address_id 
join  city c    on  a.city_id      = c.city_id  
join  store     on  store.store_id = s.store_id
join  customer  on  store.store_id = customer.store_id
group by  staff_id 
having  count(customer.customer_id) > 300; 
```

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

```sql
select  count(length)
from film
where  length > (select AVG(length) from film);
```

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

```sql
SELECT  DATE_FORMAT(payment_date, '%M %Y') as 'month of maximum payments',
SUM(amount) as 'sum',
COUNT(rental_id) as 'number of payments'
FROM payment  
GROUP BY DATE_FORMAT(payment_date, '%M %Y')
ORDER BY SUM(amount) DESC
limit 1;
```


### Задание 4*

Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».

### Задание 5*

Найдите фильмы, которые ни разу не брали в аренду.
