-- https://github.com/annykh/GT210125-m-be/blob/main/shop.sql
-- https://github.com/annykh/GT210125-m-be/blob/main/%D0%A2%D0%B5%D1%85_%D0%BE%D0%BF%D0%B8%D1%81%D0%B0%D0%BD%D0%B8%D0%B5_shop.txt

-- 1. Вывести всех продавцов, чьи имена начинаются на букву 'Л'.  
-- 2. Вывести всех клиентов из города Тула с рейтингом больше 100.  
-- 3. Вывести всех продавцов, чьи комиссии между 0.10 и 0.15 (включительно).  
-- 4. Вывести имена продавцов, у которых нет заказов.  
-- 5. Вывести имена всех продавцов, которые продают товары клиентам из Тулы.  
-- 6. Вывести имена клиентов, у которых нет заказов.  
-- 7. Вывести пары продавцов, работающих в одном городе.
-- 8. Вывести имена начальников и их подчиненных, если у начальника комиссия выше, чем у подчиненного.


CREATE DATABASE shop;

USE shop;

CREATE TABLE SELLERS(
       SELL_ID    INTEGER, 
       SNAME   VARCHAR(20), 
       CITY    VARCHAR(20), 
       COMM    NUMERIC(2, 2),
             BOSS_ID  INTEGER
);
                                            
CREATE TABLE CUSTOMERS(
       CUST_ID    INTEGER, 
       CNAME   VARCHAR(20), 
       CITY    VARCHAR(20), 
       RATING  INTEGER
);

CREATE TABLE ORDERS(
       ORDER_ID  INTEGER, 
       AMT     NUMERIC(7,2), 
       ODATE   DATE, 
       CUST_ID    INTEGER,
       SELL_ID    INTEGER 
);

INSERT INTO SELLERS VALUES(201,'Олег','Москва',0.12,202);
INSERT INTO SELLERS VALUES(202,'Лев','Сочи',0.13,204);
INSERT INTO SELLERS VALUES(203,'Арсений','Владимир',0.10,204);
INSERT INTO SELLERS VALUES(204,'Екатерина','Москва',0.11,205);
INSERT INTO SELLERS VALUES(205,'Леонид ','Казань',0.15,NULL);


INSERT INTO CUSTOMERS VALUES(301,'Андрей','Москва',100);
INSERT INTO CUSTOMERS VALUES(302,'Михаил','Тула',200);
INSERT INTO CUSTOMERS VALUES(303,'Иван','Сочи',200);
INSERT INTO CUSTOMERS VALUES(304,'Дмитрий','Ярославль',300);
INSERT INTO CUSTOMERS VALUES(305,'Руслан','Москва',100);
INSERT INTO CUSTOMERS VALUES(306,'Артём','Тула',100);
INSERT INTO CUSTOMERS VALUES(307,'Юлия','Сочи',300);


INSERT INTO ORDERS VALUES(101,18.69,'2022-03-10',308,207);
INSERT INTO ORDERS VALUES(102,5900.1,'2022-03-10',307,204);
INSERT INTO ORDERS VALUES(103,767.19,'2022-03-10',301,201);
INSERT INTO ORDERS VALUES(104,5160.45,'2022-03-10',303,202);
INSERT INTO ORDERS VALUES(105,1098.16,'2022-03-10',308,207);
INSERT INTO ORDERS VALUES(106,75.75,'2022-04-10',304,202); 
INSERT INTO ORDERS VALUES(107,4723,'2022-05-10',306,201);
INSERT INTO ORDERS VALUES(108,1713.23,'2022-04-10',302,203);
INSERT INTO ORDERS VALUES(109,1309.95,'2022-06-10',304,203);
INSERT INTO ORDERS VALUES(110,9891.88,'2022-06-10',306,201);


Техническое описание базы данных "shop"

База данных "shop" содержит 3 таблицы:

SELLERS (Продавцы)

Поля:    
    SELL_ID (PRIMARY KEY) – уникальный идентификатор продавца.
    SNAME – имя продавца.
    CITY – город, в котором находится продавец.
    COMM – комиссия продавца в виде дробного числа (процент от продаж).
    BOSS_ID – идентификатор начальника данного продавца (ссылка на SELL_ID).

Описание:
    Таблица содержит информацию о продавцах, их месте работы и процентной ставке комиссии. Поле BOSS_ID указывает на начальника продавца, что позволяет строить иерархию сотрудников.

CUSTOMERS (Клиенты)

Поля:
    CUST_ID (PRIMARY KEY) – уникальный идентификатор клиента.
    CNAME – имя клиента.
    CITY – город проживания клиента.
    RATING – рейтинг клиента (число, характеризующее активность или значимость клиента).

Описание:
  Таблица содержит информацию о клиентах, которые совершают заказы в магазине.

ORDERS (Заказы)

Поля:
    ORDER_ID (PRIMARY KEY) – уникальный идентификатор заказа.
    AMT – сумма заказа.
    ODATE – дата оформления заказа.
    CUST_ID (FOREIGN KEY → CUSTOMERS) – идентификатор клиента, который оформил заказ.
    SELL_ID (FOREIGN KEY → SELLERS) – идентификатор продавца, который оформил заказ.

Описание:
  Таблица содержит информацию о заказах, оформленных клиентами. Каждому заказу соответствует конкретный клиент и продавец, оформивший заказ.

Связи между таблицами:

ORDERS → CUSTOMERS через CUST_ID (один клиент может сделать несколько заказов).
ORDERS → SELLERS через SELL_ID (каждый заказ оформляется конкретным продавцом).
SELLERS (иерархическая связь) через BOSS_ID, который ссылается на SELL_ID (продавец может иметь начальника).





