# Домашнее задание к занятию "`Индексы`" - `Мельников Семен`




### Задание 1

SELECT  SUM(a.DATA_LENGTH) as Размер_таблиц , SUM(a.INDEX_LENGTH) as Размер_индексов, CONCAT((SUM(a.INDEX_LENGTH) / SUM(a.DATA_LENGTH) *100))  AS '%'
FROM INFORMATION_SCHEMA.TABLES a
WHERE  a.TABLE_SCHEMA = 'sakila' ;

![image](https://user-images.githubusercontent.com/114281054/221504504-d0b1266d-7518-4a48-999d-f3609a8201b6.png)



---

### Задание 2

Не уверен,что правильно понял задание, буду отвечать исходя из того, что нужно выяснить почему запрос выполняется так долго и как можно получить аналогичный результат быстрее:


Часть запроса "distinct, over (partition by c.customer_id, f.title)" значительно замедляет выполнение запроса и нам это действие не трбуется в принципе,можно сделать группировку в конце запроса по name
Плюс не очень понятно зачем в список таблиц добалена film,она не нужна для решения задачи, вот так можно:

SELECT CONCAT(c.last_name, ' ', c.first_name) as name, sum(p.amount)
FROM payment p, rental r, customer c, inventory i
WHERE date(p.payment_date) = '2005-07-30' AND p.payment_date = r.rental_date AND r.customer_id = c.customer_id AND i.inventory_id = r.inventory_id
GROUP BY name

На выходе получаем тоже самое, но значительно быстрее
