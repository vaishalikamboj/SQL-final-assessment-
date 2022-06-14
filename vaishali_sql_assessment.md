# SQL-final-assessment-

create database truyum;
use truyum;
-- 1. a) Frame insert scripts to add data into menu_item table. 
create table menu_item(
item_id int auto_increment primary key,
item_name varchar(40) not null,
price float not null,
is_it_active varchar(3) not null,
date_of_launch date not null,
category varchar(20),
free_delivery varchar(3));
-- 1. b) Frame SQL query to get all menu items 
select *from menu_item;

insert into menu_item (item_name, price, is_it_active, date_of_launch, category, free_delivery) values ('sandwich', 99, 'yes', '2016-09-01', 'main course', 'yes'), ('burger', 129, 'yes', '2015-03-09', 'main course', 'no'), ('pizza', 149, 'yes', '2017-01-08', 'main course', 'yes'), ('frenchfries', 49, 'no', '2017-03-05', 'starters', 'yes'), ('chocolate brownie', 79, 'yes', '2018-04-09', 'dessert', 'yes');

-- 2. a) Frame SQL query to get all menu items which after launch date is active. 
select *from menu_item where is_it_active ='yes';

-- 3. a) Frame SQL query to get a menu items based on menu item id
select *from menu_item where item_id in ('1', '3');

-- 3. b) frame update SQL menu_items table to update all the columns values based on Menu Item Id
update menu_item set item_name ='cornchips', price = 20, category = 'starters' where item_id = '4';

-- 4. a) frame insert scripts for adding data into user and cart tables.In user table create two users. Once user will not have any entries in cart, while the other will have at least 3 items in the cart.
create table users(
id int primary key auto_increment,
name varchar(90) not null);

create table cart (
cart_id int primary key auto_increment,
menu_item_id int,
user_id int,
foreign key (user_id) references menu_item(item_id),
foreign key (user_id) references users(id)); 

select *from users;
select *from cart;
insert into users values (1, 'Duranjaya');
insert into users values (2, 'Amolika');

insert into cart values (1,2,1), (2,3,1), (3,5,1);
select a.item_name from menu_item as a join cart as b on a.item_id = b.menu_item_id where b.user_id = 1;

select sum(a.price) from menu_item as a join cart as b on a.item_id = b.menu_item_id where b.user_id = 1;

delete from cart where user_id = 1 and menu_item_id = 3;
