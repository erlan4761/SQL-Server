# SQL-Server
SQL Server database


-----------------------------------------------------------------------------------------TABLE CLIENTS
drop table CLIENTS;
create table CLIENTS (
	CLIENTS_ID int NOT NULL IDENTITY(1,1) primary key,
	NAME nchar(1000),
	PLACE_OF_BIRTH nchar(1000),
	DATE_OF_BIRTH date,
	ADDRESS nchar(1000),
	PASSPORT nchar(1000),
	CLIENTS_PK int);


insert into clients (NAME, PLACE_OF_BIRTH, DATE_OF_BIRTH, ADDRESS, PASSPORT)
	values (
		'Сидоров Иван Петрович',
		'Россия, Московская облать, г. Пушкин',
		 CONVERT(DATETIME,'01.01.2001'),
		'Россия, Московская облать, г. Пушкин, ул. Грибоедова, д. 5',
		'2222 555555, выдан ОВД г. Пушкин, 10.01.2015');

insert into clients (NAME, PLACE_OF_BIRTH, DATE_OF_BIRTH, ADDRESS, PASSPORT)
	values (
		'Иванов Петр Сидорович',
		'Россия, Московская облать, г. Клин',
		 CONVERT(DATETIME,'01.01.2001'),
		'Россия, Московская облать, г. Клин, ул. Мясникова, д. 3',
		'4444 666666, выдан ОВД г. Клин, 10.01.2015');

insert into clients (NAME, PLACE_OF_BIRTH, DATE_OF_BIRTH, ADDRESS, PASSPORT)
	values (
		'Петров Сиодр Иванович',
		'Россия, Московская облать, г. Балашиха',
		CONVERT(DATETIME,'01.01.2001'),
		'Россия, Московская облать, г. Балашиха, ул. Пушкина, д. 7',
		'4444 666666, выдан ОВД г. Клин , 10.01.2015');

select * from CLIENTS
-----------------------------------------------------------------------------------------TABLE PRODUCTS
drop table PRODUCTS;
create table PRODUCTS (
	PRODUCT_ID int NOT NULL IDENTITY(1,1) primary key,
	PRODUCT_TYPE_ID int,
	NAME nchar(100),
	CLIENT_REF int,
	OPEN_DATE date,
	CLOSE_DATA date);

insert into products (PRODUCT_TYPE_ID, name, CLIENT_REF, OPEN_DATE,CLOSE_DATA)
	values (1,'Кредитный договор с Сидоровым И.П.',1,CONVERT(DATETIME,'01.06.2015'),null);

insert into products (PRODUCT_TYPE_ID, name, CLIENT_REF, OPEN_DATE,CLOSE_DATA)
	values (2,'Депозитный договор с Сидоровым И.П.',2,CONVERT(DATETIME,'01.08.2017'),null);

insert into products (PRODUCT_TYPE_ID, name, CLIENT_REF, OPEN_DATE,CLOSE_DATA) 
	values (3,'Карточный договор с Сидоровым И.П.',3,CONVERT(DATETIME,'01.08.2017') ,null);

select * from PRODUCTS
-----------------------------------------------------------------------------------------TABLE PRODUCTYPE
drop table PRODUCTYPE;
create table PRODUCTYPE (
	ID int NOT NULL IDENTITY(1,1) primary key,
	NAME nchar(100),
	BEGIN_DATE date,
	END_DATE date,
	TARIF_REF int,);
	
insert into productype (name, begin_date, end_date, TARIF_REF)
	values ('КРЕДИТ', CONVERT(DATETIME,'01.01.2018'),null,1);

insert into productype (name, begin_date, end_date, TARIF_REF)
	values ('ДЕПОЗИТ',CONVERT(DATETIME,'01.01.2018'),null,2);

insert into productype (name, begin_date, end_date, TARIF_REF)
	values ('КАРТА',CONVERT(DATETIME,'01.01.2018'),null,3);

select * from PRODUCTYPE
-----------------------------------------------------------------------------------------TABLE TARIFS
drop table TARIFS;
create table TARIFS (
	ID int NOT NULL IDENTITY(1,1) primary key,
	NAME nchar(100),
	COST int,);

insert into tarifs (name, cost)
	values ('Тариф за выдачу кредита', 10);

insert into tarifs (name, cost)
	values ('Тариф за открытие счета', 10);

insert into tarifs (name, cost)
	values ('Тариф за обслуживание карты', 10);

select * from TARIFS;
-----------------------------------------------------------------------------------------TABLE ACCOUNTS
drop table ACCOUNTS;
create table ACCOUNTS (
	ID int NOT NULL IDENTITY(1,1) primary key,
	NAME nchar(100),
	SALDO int,
	CLIENT_REF int,
	OPEN_DATE date,
	CLOSE_DATE date,
	PRODUCT_REF int,
	ACC_NUM nchar(25));
	
insert into accounts (name, saldo, client_ref, open_date, close_date, product_ref, acc_num)
	values ('Кредитный счет для Сидорова И.П.',-2000, 1, CONVERT(DATETIME,'01.08.2017'), null, 1,'45502810401020000022');

insert into accounts (name, saldo, client_ref, open_date, close_date, product_ref, acc_num)
	values ('Депозитный счет для Сидорова И.П.', 6000, 2, CONVERT(DATETIME,'01.08.2017'), null, 2,'42301810400000000001');

insert into accounts (name, saldo, client_ref, open_date, close_date, product_ref, acc_num)
	values ('Карточный счет для Сидорова И.П.', 8000, 3, CONVERT(DATETIME,'01.08.2017'), null, 3,'40817810700000000001');

select * from ACCOUNTS
-----------------------------------------------------------------------------------------TABLE RECORDS
drop table RECORDS;
create table RECORDS (
	ID int NOT NULL IDENTITY(1,1) primary key,
	DT int,
	SUM int,
	ACC_REF int,
	OPEN_DATE date);

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (1, 5000, 1, CONVERT(DATETIME,'01.06.2015'));

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (0, 1000, 1, CONVERT(DATETIME,'01.07.2015'));

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (0, 2000, 1, CONVERT(DATETIME,'01.08.2015'));

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (0, 3000, 1, CONVERT(DATETIME,'01.09.2015'));

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (1, 5000, 1, CONVERT(DATETIME,'01.10.2015'));

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (0, 3000, 1, CONVERT(DATETIME,'01.10.2015'));
	

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (0, 10000, 2, CONVERT(DATETIME,'01.08.2017'));

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (1, 1000, 2, CONVERT(DATETIME,'05.08.2017'));

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (1, 2000, 2, CONVERT(DATETIME,'21.09.2017'));

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (1, 5000, 2, CONVERT(DATETIME,'24.10.2017'));

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (0, 6000, 2, CONVERT(DATETIME,'26.11.2017'));


insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (0, 120000, 3, CONVERT(DATETIME,'08.09.2017'));

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (1, 1000, 3, CONVERT(DATETIME,'05.10.2017'));

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (1, 2000, 3, CONVERT(DATETIME,'21.10.2017'));

insert into records (DT, SUM, ACC_REF, OPEN_DATE)
	values (1, 5000, 3, CONVERT(DATETIME,'24.10.2017'));

select * from RECORDS
