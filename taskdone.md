https://github.com/annykh/GT210125-m-be/blob/main/shop.sql 
https://github.com/annykh/GT210125-m-be/blob/main/%D0%A2%D0%B5%D1%85_%D0%BE%D0%BF%D0%B8%D1%81%D0%B0%D0%BD%D0%B8%D0%B5_shop.txt

-- 3. Вывести всех продавцов, чьи комиссии между 0.10 и 0.15 (включительно).
-- 4. Вывести имена продавцов, у которых нет заказов.
-- 5. Вывести имена всех продавцов, которые продают товары клиентам из Тулы.
-- 6. Вывести имена клиентов, у которых нет заказов.
-- 7. Вывести пары продавцов, работающих в одном городе. -- 8. Вывести имена начальников и их подчиненных, если у начальника комиссия выше, чем у подчиненного.



-- 1. Вывести всех продавцов, чьи имена начинаются на букву 'Л'.  
```
select SNAME from SELLERS 
where SNAME like 'Л%';
```
-- 2. Вывести всех клиентов из города Тула с рейтингом больше 100. 
```
select CNAME, CITY, RATING
from CUSTOMERS
where CITY = 'Тула' and RATING > 100;
```

-- 3. Вывести всех продавцов, чьи комиссии между 0.10 и 0.15 (включительно)
```
select SNAME, COMM
from SELLERS
where COMM between 0.10 and 0.15;
```

-- 4. Вывести имена продавцов, у которых нет заказов.  
```
select s.SNAME
from SELLERS s
left join ORDERS o on s.SELL_ID = o.SELL_ID
where o.ORDER_ID is null;
```

-- 5. Вывести имена всех продавцов, которые продают товары клиентам из Тулы.  
```
select distinct s.SNAME
from SELLERS s
join ORDERS o on s.SELL_ID = o.SELL_ID
join CUSTOMERS c on o.CUST_ID = c.CUST_ID
where c.CITY = 'Тула';
```
