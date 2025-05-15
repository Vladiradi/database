https://github.com/annykh/GT210125-m-be/blob/main/shop.sql 
https://github.com/annykh/GT210125-m-be/blob/main/%D0%A2%D0%B5%D1%85_%D0%BE%D0%BF%D0%B8%D1%81%D0%B0%D0%BD%D0%B8%D0%B5_shop.txt


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

-- 6. Вывести имена клиентов, у которых нет заказов.
```
select distinct c.CNAME
from SELLERS s
join ORDERS o on s.SELL_ID = o.SELL_ID
join CUSTOMERS c on o.CUST_ID = c.CUST_ID
```

-- 7. Вывести пары продавцов, работающих в одном городе
```
select s1.SNAME as seller01, s2.SNAME as seller02, s1.CITY
from SELLERS s1
join SELLERS s2
on s1.CITY = s2.CITY and s1.SELL_ID < s2.SELL_ID;
```
-- 8. Вывести имена начальников и их подчиненных, если у начальника комиссия выше, чем у подчиненного.
select boss.SNAME as boss, emp.SNAME as employee
from SELLERS emp
join SELLERS boss on emp.BOSS_ID = boss.SELL_ID
where boss.COMM > emp.COMM;
