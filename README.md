## Лабораторна робота №4
1. Створюю базу даних і підключаюся до неї.
```mysql
create database Products;
use Products;
```

2. Створюю таблицю Customers.
```mysql
create table Customers(
    id int auto_increment primary key,
    age int,
    name varchar(32),
    surname varchar(32),
    phone varchar(16) unique
);
```

3. Створюю таблицю Orders.
```mysql
create table Orders(
    id int auto_increment primary key,
    date date,
    customer_id int,
    foreign key (customer_id) references Customers (id)
    on update cascade on delete cascade
);
```

4. Створюю таблицю Products.
```mysql
create table Products(
    id int auto_increment primary key,
    name varchar(50),
    manufacturer varchar(50),
    product_count int,
    price decimal
);
```

5. Додаю до таблиць Customers та Orders записи.
```mysql
insert into Customers(age, name, surname, phone)
values (21, 'Viriato', 'Sol', '(057)52-64-51'),
       (32, 'Suibhne', 'Charon', '(0512)46-15-56'),
       (38, 'Arthur', 'Afrodita', '(056)47-03-65'),
       (31, 'Sunita', 'Lech', '(062)63-60-55'),
       (33, 'Pollux', 'Cian', '(056)773-21-36'),
       (29, 'Glaukos', 'Vesper', '(048)26-17-06'),
       (42, 'Usha', 'Taranis', '(062)63-60-54'),
       (60, 'Brynhildr', 'Ashtart', '(044)518-59-66'),
       (43, 'Koios', 'Ishkur', '(0322)74-67-68'),
       (58, 'Murali', 'Pyrrhus', '(0692)47-38-44');

insert into Orders(date, customer_id)
values (date('2022-04-01'), 1),
       (date('2022-04-02'), 2),
       (date('2022-04-03'), 3),
       (date('2022-04-04'), 4),
       (date('2022-04-05'), 5),
       (date('2022-04-06'), 6),
       (date('2022-04-07'), 7),
       (date('2022-04-08'), 8),
       (date('2022-04-09'), 9),
       (date('2022-04-10'), 10);
```

6. Роблю повну вибірку з таблиць Customers та Orders.
```mysql
select * from Customers;
```
| id  | age | name      | surname  | phone          |
|-----|-----|-----------|----------|----------------|
| 1   | 21  | Viriato   | Sol      | (057)52-64-51  |
| 2   | 32  | Suibhne   | Charon   | (0512)46-15-56 |
| 3   | 38  | Arthur    | Afrodita | (056)47-03-65  |
| 4   | 31  | Sunita    | Lech     | (062)63-60-55  |
| 5   | 33  | Pollux    | Cian     | (056)773-21-36 |
| 6   | 29  | Glaukos   | Vesper   | (048)26-17-06  |
| 7   | 42  | Usha      | Taranis  | (062)63-60-54  |
| 8   | 60  | Brynhildr | Ashtart  | (044)518-59-66 |
| 9   | 43  | Koios     | Ishkur   | (0322)74-67-68 |
| 10  | 58  | Murali    | Pyrrhus  | (0692)47-38-44 |

```mysql
select * from Orders;
```
| id  | date       | customer_id |
|-----|------------|-------------|
| 1   | 2022-04-01 | 1           |
| 2   | 2022-04-02 | 2           |
| 3   | 2022-04-03 | 3           |
| 4   | 2022-04-04 | 4           |
| 5   | 2022-04-05 | 5           |
| 6   | 2022-04-06 | 6           |
| 7   | 2022-04-07 | 7           |
| 8   | 2022-04-08 | 8           |
| 9   | 2022-04-09 | 9           |
| 10  | 2022-04-10 | 10          |

7. Роблю вибірку всіх замовників чий вік знаходиться в
діапазоні від 20 до 30 років. Перед цим вношу зміни до таблиці, щоб в результаті вибірки було не менше трьох результатів.
```mysql
update Customers set age = age - 10;
select * from Customers where age between 20 and 30;
```
| id  | age | name    | surname  | phone          |
|-----|-----|---------|----------|----------------|
| 2   | 22  | Suibhne | Charon   | (0512)46-15-56 |
| 3   | 28  | Arthur  | Afrodita | (056)47-03-65  |
| 4   | 21  | Sunita  | Lech     | (062)63-60-55  |
| 5   | 23  | Pollux  | Cian     | (056)773-21-36 |

8. Роблю запит, який виведе на екран два стовпці. Перед цим додаю записи.
```mysql
insert into Products(name, manufacturer, product_count, price)
values ('Laptop',   'HP',       2,  16999.00),
       ('Laptop',   'Asus',     10, 26999.00),
       ('TV',       'Samsung',  4,  24999.00),
       ('TV',       'LG',       4,  28999.00),
       ('TV',       'Samsung',  4,  28999.00),
       ('Laptop',   'Asus',     6,  26999.00),
       ('TV',       'Samsung',  4,  18999.00),
       ('TV',       'Samsung',  4,  33999.00),
       ('TV',       'Samsung',  4,  43999.00),
       ('TV',       'Samsung',  4,  11999.00);
select name, product_count * price from Products;
```
| name   | product_count * price |
|--------|-----------------------|
| Laptop | 33998                 |
| Laptop | 269990                |
| TV     | 99996                 |
| TV     | 115996                |
| TV     | 115996                |
| Laptop | 161994                |
| TV     | 75996                 |
| TV     | 135996                |
| TV     | 175996                |
| TV     | 47996                 |

9. Роблю вибірку всіх товарів деякого виробника.
```mysql
select * from Products
where manufacturer = 'Samsung';
```
| id  | name | manufacturer | product_count | price |
|-----|------|--------------|---------------|-------|
| 3   | TV   | Samsung      |             4 | 24999 |
| 5   | TV   | Samsung      |             4 | 28999 |
| 7   | TV   | Samsung      |             4 | 18999 |
| 8   | TV   | Samsung      |             4 | 33999 |
| 9   | TV   | Samsung      |             4 | 43999 |
| 10  | TV   | Samsung      |             4 | 11999 |

10. Змінюю по одному запису у таблицях.
#### Customers
```mysql
update Customers set age = age + 1
where id = 1;
```
Було

| id  | age | name    | surname | phone         |
|-----|-----|---------|---------|---------------|
| 1   | 11  | Viriato | Sol     | (057)52-64-51 |
Стало

| id  | age | name    | surname | phone         |
|-----|-----|---------|---------|---------------|
| 1   | 12  | Viriato | Sol     | (057)52-64-51 |

#### Orders
```mysql
update Orders set date = date_add(date, interval 1 day)
where id = 1;
```
Було

| id  | date       | customer_id |
|-----|------------|-------------|
| 1   | 2022-04-01 | 1           |
Стало

| id  | date       | customer_id |
|-----|------------|-------------|
| 1   | 2022-04-02 | 1           |


#### Products
```mysql
update Products set product_count = product_count + 2
where id = 1;
```
Було

| id  | name   | manufacturer | product_count | price |
|-----|--------|--------------|---------------|-------|
| 1   | Laptop | HP           | 2             | 16999 |
Стало

| id  | name   | manufacturer | product_count | price |
|-----|--------|--------------|---------------|-------|
| 1   | Laptop | HP           | 4             | 16999 |

11. Видаляю по одному запису в таблицях.
#### Customers
```mysql
delete from Customers
order by age desc limit 1;
```
Було

| id  | age | name      | surname  | phone          |
|-----|-----|-----------|----------|----------------|
| 1   | 12  | Viriato   | Sol      | (057)52-64-51  |
| 2   | 22  | Suibhne   | Charon   | (0512)46-15-56 |
| 3   | 28  | Arthur    | Afrodita | (056)47-03-65  |
| 4   | 21  | Sunita    | Lech     | (062)63-60-55  |
| 5   | 23  | Pollux    | Cian     | (056)773-21-36 |
| 6   | 19  | Glaukos   | Vesper   | (048)26-17-06  |
| 7   | 32  | Usha      | Taranis  | (062)63-60-54  |
| 8   | 50  | Brynhildr | Ashtart  | (044)518-59-66 |
| 9   | 33  | Koios     | Ishkur   | (0322)74-67-68 |
| 10  | 48  | Murali    | Pyrrhus  | (0692)47-38-44 |
Стало


| id  | age | name      | surname  | phone          |
|-----|-----|-----------|----------|----------------|
| 1   | 12  | Viriato   | Sol      | (057)52-64-51  |
| 2   | 22  | Suibhne   | Charon   | (0512)46-15-56 |
| 3   | 28  | Arthur    | Afrodita | (056)47-03-65  |
| 4   | 21  | Sunita    | Lech     | (062)63-60-55  |
| 5   | 23  | Pollux    | Cian     | (056)773-21-36 |
| 6   | 19  | Glaukos   | Vesper   | (048)26-17-06  |
| 7   | 32  | Usha      | Taranis  | (062)63-60-54  |
| 9   | 33  | Koios     | Ishkur   | (0322)74-67-68 |
| 10  | 48  | Murali    | Pyrrhus  | (0692)47-38-44 |

#### Orders
```mysql
delete from Orders
order by date desc limit 1;
```
Було

| id  | date       | customer_id |
|-----|------------|-------------|
| 1   | 2022-04-02 | 1           |
| 2   | 2022-04-02 | 2           |
| 3   | 2022-04-03 | 3           |
| 4   | 2022-04-04 | 4           |
| 5   | 2022-04-05 | 5           |
| 6   | 2022-04-06 | 6           |
| 7   | 2022-04-07 | 7           |
| 9   | 2022-04-09 | 9           |
| 10  | 2022-04-10 | 10          |
Стало

| id  | date       | customer_id |
|-----|------------|-------------|
| 1   | 2022-04-02 | 1           |
| 2   | 2022-04-02 | 2           |
| 3   | 2022-04-03 | 3           |
| 4   | 2022-04-04 | 4           |
| 5   | 2022-04-05 | 5           |
| 6   | 2022-04-06 | 6           |
| 7   | 2022-04-07 | 7           |
| 9   | 2022-04-09 | 9           |

#### Products
```mysql
delete from Products
order by price * product_count limit 1;
```

Було

| id  | name   | manufacturer | product_count | price |
|-----|--------|--------------|---------------|-------|
| 1   | Laptop | HP           | 4             | 16999 |
| 2   | Laptop | Asus         | 10            | 26999 |
| 3   | TV     | Samsung      | 4             | 24999 |
| 4   | TV     | LG           | 4             | 28999 |
| 5   | TV     | Samsung      | 4             | 28999 |
| 6   | Laptop | Asus         | 6             | 26999 |
| 7   | TV     | Samsung      | 4             | 18999 |
| 8   | TV     | Samsung      | 4             | 33999 |
| 9   | TV     | Samsung      | 4             | 43999 |
| 10  | TV     | Samsung      | 4             | 11999 |

Стало

| id  | name   | manufacturer | product_count | price |
|-----|--------|--------------|---------------|-------|
| 1   | Laptop | HP           | 4             | 16999 |
| 2   | Laptop | Asus         | 10            | 26999 |
| 3   | TV     | Samsung      | 4             | 24999 |
| 4   | TV     | LG           | 4             | 28999 |
| 5   | TV     | Samsung      | 4             | 28999 |
| 6   | Laptop | Asus         | 6             | 26999 |
| 7   | TV     | Samsung      | 4             | 18999 |
| 8   | TV     | Samsung      | 4             | 33999 |
| 9   | TV     | Samsung      | 4             | 43999 |

12. Роблю унікальну вибірку виробників.
```mysql
select distinct manufacturer from Products;
```

| manufacturer |
|--------------|
| HP           |
| Asus         |
| Samsung      |
| LG           |
