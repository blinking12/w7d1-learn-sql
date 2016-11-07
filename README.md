# w7d1-learn-sql

How many users are there?  
50
select count(*) from users;

What are the 5 most expensive items?
25          Small Cotton Gloves  Automotive, Shoes & Beauty  Multi-layered modular service-desk  9984      
83          Small Wooden Comput  Health                      Re-engineered fault-tolerant adapt  9859      
100         Awesome Granite Pan  Toys & Books                Upgradable 24/7 access              9790      
40          Sleek Wooden Hat     Music & Baby                Quality-focused heuristic info-med  9390      
60          Ergonomic Steel Car  Books & Outdoors            Enterprise-wide secondary firmware  9341      
select * from items order by price desc;


What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
76          Ergonomic Granite C  Books                       De-engineered bi-directional porta  1496
select price from items where category like '%Books%';
select price from items where category like 'Books';
There is no difference in the cheapest book.


Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
select user_id from addresses where street like '%6439%';
select first_name, last_name from users where id=40;
first_name  last_name
----------  ----------
Corrine     Little   

select count(user_id) from addresses where user_id=40;
count(user_id)
--------------
2         

Correct Virginie Mitchell's address to "New York, NY, 10108".
select id from users where first_name='Virginie';
id        
----------
39
select * from addresses where user_id=39;
id          user_id     street               city         state       zip       
----------  ----------  -------------------  -----------  ----------  ----------
41          39          12263 Jake Crossing  Roxanehaven  NY          34705     
42          39          83221 Mafalda Canyo  Bahringerla  WY          24028    

UPDATE addresses SET city = "New York", zip = 10108 where id=41;
sqlite> select * from addresses where id=41;
id          user_id     street               city        state       zip       
----------  ----------  -------------------  ----------  ----------  ----------
41          39          12263 Jake Crossing  New York    NY          10108     


How much would it cost to buy one of each tool?
select sum(price) from items where category like '%Tools%';
sum(price)
----------
46477


How many total items did we sell?
select sum(quantity) from orders;
2126



How much was spent on books?
elect sum(items.price*orders.quantity) from items inner join orders on items.id=orders.item_id where items.category like '%Book%';

1081352



Simulate buying an item by inserting a User for yourself and an Order for that User.
insert into users values (51, 'Troy', 'Denney', 'tvdenney@gmail.com');
insert into orders values (378, 51, 91, 1, datetime());
