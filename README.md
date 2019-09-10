# java-sql

A student that completes this project shows that they can:
* Query data from a single table
* Query data from multiple tables
* Create a new datadaase using PostgreSQL

# Introduction

Working with SQL

# Instructions

ReImport the Northwind database into PostgreSQL using pgAdmin. This is the same data we used during the guided project.

clone https://github.com/pthom/northwind_psql.git

## pgAdmin

* Right Click Databases
  * Create
    * type in northwind2

* Tools -> Query Tool
  * Open file northwind.sql (from cloned repo)
  * Execute

* Look under
  * northwind2 -> Schemas -> public -> tables

* Clear query windows

Answer the following data queries. Keep track of the SQL you write by pasting it into this document under its appropriate header below. You will be submitting that through the regular fork, change, pull process.


### find all customers that live in London. Returns 6 records.
> This can be done with SELECT and WHERE clauses

Code:

SELECT *
FROM customers
WHERE city ='London'

Answer:

"AROUT"	"Around the Horn"	"Thomas Hardy"	"Sales Representative"	"120 Hanover Sq."	"London"		"WA1 1DP"	"UK"	"(171) 555-7788"	"(171) 555-6750"
"BSBEV"	"B's Beverages"	"Victoria Ashworth"	"Sales Representative"	"Fauntleroy Circus"	"London"		"EC2 5NT"	"UK"	"(171) 555-1212"	
"CONSH"	"Consolidated Holdings"	"Elizabeth Brown"	"Sales Representative"	"Berkeley Gardens 12  Brewery"	"London"		"WX1 6LT"	"UK"	"(171) 555-2282"	"(171) 555-9199"
"EASTC"	"Eastern Connection"	"Ann Devon"	"Sales Agent"	"35 King George"	"London"		"WX3 6FW"	"UK"	"(171) 555-0297"	"(171) 555-3373"
"NORTS"	"North/South"	"Simon Crowther"	"Sales Associate"	"South House 300 Queensbridge"	"London"		"SW7 1RZ"	"UK"	"(171) 555-7733"	"(171) 555-2530"
"SEVES"	"Seven Seas Imports"	"Hari Kumar"	"Sales Manager"	"90 Wadhurst Rd."	"London"		"OX15 4NB"	"UK"	"(171) 555-1717"	"(171) 555-5646"


### find all customers with postal code 1010. Returns 3 customers.
> This can be done with SELECT and WHERE clauses

Code:

SELECT * 
FROM customers
WHERE postal_code = '1010'

Answer:

"CACTU"	"Cactus Comidas para llevar"	"Patricio Simpson"	"Sales Agent"	"Cerrito 333"	"Buenos Aires"		"1010"	"Argentina"	"(1) 135-5555"	"(1) 135-4892"
"OCEAN"	"Océano Atlántico Ltda."	"Yvonne Moncada"	"Sales Agent"	"Ing. Gustavo Moncada 8585 Piso 20-A"	"Buenos Aires"		"1010"	"Argentina"	"(1) 135-5333"	"(1) 135-5535"
"RANCH"	"Rancho grande"	"Sergio Gutiérrez"	"Sales Representative"	"Av. del Libertador 900"	"Buenos Aires"		"1010"	"Argentina"	"(1) 123-5555"	"(1) 123-5556"


### find the phone number for the supplier with the id 11. Should be (010) 9984510.
> This can be done with SELECT and WHERE clauses

Code:

SELECT phone
FROM suppliers
WHERE supplier_id = 11

Answer:

"(010) 9984510"


### list orders descending by the order date. The order with date 1998-05-06 should be at the top.
> This can be done with SELECT, WHERE, and ORDER BY clauses

Code:

SELECT order_date
FROM orders
ORDER BY order_date DESC

Answer:

"1998-05-06"
"1998-05-06"
"1998-05-06"
"1998-05-06"
"1998-05-05"
"1998-05-05"
"1998-05-05"
"1998-05-05"


### find all suppliers who have names longer than 20 characters. You can use `length(company_name)` to get the length of the name. Returns 11 records.
> This can be done with SELECT and WHERE clauses

Code:

SELECT company_name
FROM suppliers
WHERE length(company_name) > 20
  

Answer:

"New Orleans Cajun Delights"
"Grandma Kelly's Homestead"
"Cooperativa de Quesos 'Las Cabras'"
"Specialty Biscuits, Ltd."
"Refrescos Americanas LTDA"
"Heli Süßwaren GmbH & Co. KG"
"Plutzer Lebensmittelgroßmärkte AG"
"Nord-Ost-Fisch Handelsgesellschaft mbH"
"Formaggi Fortini s.r.l."
"Aux joyeux ecclésiastiques"
"New England Seafood Cannery"



### find all customers that include the word 'MARKET' in the contact title. Should return 19 records.
> This can be done with SELECT and a WHERE clause using the LIKE keyword

> Don't forget the wildcard '%' symbols at the beginning and end of your substring to denote it can appear anywhere in the string in question

> Remember to convert your contact title to all upper case for case insenstive comparing so upper(contact_title)

Code:

SELECT contact_title
FROM customers
WHERE UPPER(contact_title) like '%MARKET%'

Answer:

"Marketing Manager"
"Marketing Manager"
"Marketing Assistant"
"Marketing Manager"
"Marketing Manager"
"Marketing Manager"
"Marketing Manager"
"Marketing Manager"
"Marketing Assistant"
"Marketing Manager"
"Marketing Manager"
"Marketing Assistant"
"Marketing Assistant"
"Marketing Assistant"
"Marketing Manager"
"Marketing Manager"
"Marketing Assistant"
"Marketing Manager"
"Owner/Marketing Assistant"


### add a customer record for   
* customer id is 'SHIRE'
* company name is 'The Shire'
* contact name is 'Bilbo Baggins'
* the address is '1 Hobbit-Hole'
* ths city is 'Bag End'
* the postal code is '111'
* the country is 'Middle Earth'
> This can be done with the INSERT INTO clause

Code:
INSERT INTO customers(customer_id, company_name, contact_name, address, city, postal_code, country)  
VALUES ('SHIRE', 'The Shire', 'Bilbo Baggins', '1 Hobbit-Hole', 'Bag End', '111', 'Middle Earth') 

Answer:
"SHIRE"	"The Shire"	"Bilbo Baggins"		"1 Hobbit-Hole"	"Bag End"		"111"	"Middle Earth"		


### update _Bilbo Baggins_ record so that the postal code changes to _"11122"_.
> This can be done with UPDATE and WHERE clauses

Code:
UPDATE customers
SET postal_code = '11122'
WHERE customer_id = 'SHIRE'

Answer:
"SHIRE"	"The Shire"	"Bilbo Baggins"		"1 Hobbit-Hole"	"Bag End"		"11122"	"Middle Earth"

### list orders grouped by customer showing the number of orders per customer. _Rattlesnake Canyon Grocery_ should have 18 orders.
> This can be done with SELECT, COUNT, JOIN and GROUP BY clauses. Your count should focus on a field in the Orders table, not the Customer table

> There is more information about the COUNT clause on [W3 Schools](https://www.w3schools.com/sql/sql_count_avg_sum.asp)

Code:

SELECT COUNT(DISTINCT o.Order_id) AS TotalOrders, c.Company_Name, c.Contact_Name, c.customer_id
FROM orders o JOIN customers c 
on (o.Customer_iD = c.Customer_iD)
GROUP BY c.customer_ID

Answer:

"18"	"Rattlesnake Canyon Grocery"	"Paula Wilson"	"RATTC"
"6"	"Alfreds Futterkiste"	"Maria Anders"	"ALFKI"
"4"	"Ana Trujillo Emparedados y helados"	"Ana Trujillo"	"ANATR"
"7"	"Antonio Moreno Taquería"	"Antonio Moreno"	"ANTON"
"13"	"Around the Horn"	"Thomas Hardy"	"AROUT"
"18"	"Berglunds snabbköp"	"Christina Berglund"	"BERGS"
"7"	"Blauer See Delikatessen"	"Hanna Moos"	"BLAUS"
"11"	"Blondesddsl père et fils"	"Frédérique Citeaux"	"BLONP"
"3"	"Bólido Comidas preparadas"	"Martín Sommer"	"BOLID"
"17"	"Bon app'"	"Laurence Lebihan"	"BONAP"
"14"	"Bottom-Dollar Markets"	"Elizabeth Lincoln"	"BOTTM"
"10"	"B's Beverages"	"Victoria Ashworth"	"BSBEV"
"6"	"Cactus Comidas para llevar"	"Patricio Simpson"	"CACTU"

### list customers names and the number of orders per customer. Sort the list by number of orders in descending order. _Save-a-lot Markets should be at the top with 31 orders followed by _Ernst Handle_ with 30 orders. Last should be _Centro comercial Moctezuma_ with 1 order.
> This can be done by adding an ORDER BY clause to the previous answer

Code:

SELECT COUNT(DISTINCT o.Order_id) AS TotalOrders, c.Company_Name, c.Contact_Name, c.customer_id
FROM orders o JOIN customers c 
on (o.Customer_iD = c.Customer_iD)
GROUP BY c.customer_ID
ORDER BY TotalOrders DESC

Answer:

"31"	"Save-a-lot Markets"	"Jose Pavarotti"	"SAVEA"
"30"	"Ernst Handel"	"Roland Mendel"	"ERNSH"
"28"	"QUICK-Stop"	"Horst Kloss"	"QUICK"
"19"	"Hungry Owl All-Night Grocers"	"Patricia McKenna"	"HUNGO"
"19"	"Folk och fä HB"	"Maria Larsson"	"FOLKO"
"18"	"Rattlesnake Canyon Grocery"	"Paula Wilson"	"RATTC"
"18"	"Berglunds snabbköp"	"Christina Berglund"	"BERGS"
"18"	"HILARION-Abastos"	"Carlos Hernández"	"HILAA"
"17"	"Bon app'"	"Laurence Lebihan"	"BONAP"
"15"	"Wartian Herkku"	"Pirkko Koskitalo"	"WARTH"

### list orders grouped by customer's city showing number of orders per city. Returns 69 Records with _Aachen_ showing 6 orders and _Albuquerque_ showing 18 orders.
> This is very similar to the previous two queries, however, it focuses on the City rather than the CustomerName

Code:

SELECT COUNT(DISTINCT o.Order_id) AS TotalOrders, c.city
FROM orders o JOIN customers c 
on (o.ship_city = c.city)
GROUP BY c.city
ORDER BY TotalOrders DESC

Answer:

"18"	"Albuquerque"
"6"	"Aachen"

"34"	"Rio de Janeiro"
"33"	"London"
"31"	"Sao Paulo"
"31"	"Boise"
"30"	"Graz"
"28"	"México D.F."
"28"	"Cunewalde"
"19"	"Cork"
"19"	"Bräcke"
"18"	"Albuquerque"

## Data Normalization

Note: This step does not use PostgreSQL!

Take the following data and normalize it into a 3NF database.

| Person Name | Pet Name | Pet Type | Pet Name 2 | Pet Type 2 | Pet Name 3 | Pet Type 3 | Fenced Yard | City Dweller |
|-------------|----------|----------|------------|------------|------------|------------|-------------|--------------|
| Jane        | Ellie    | Dog      | Tiger      | Cat        | Toby       | Turtle     | No          | Yes          |
| Bob         | Joe      | Horse    |            |            |            |            | No          | No           |
| Sam         | Ginger   | Dog      | Miss Kitty | Cat        | Bubble     | Fish       | Yes         | No           |

---

Answer -

Preson Table:
Person ID   Person Name  Dwelling ID

Pet Name Table:
Name ID   Person ID   Pet Type   Pet Name

Dwelling Table:
Dwelling ID   Fenced Yard   City Dweller





## Stretch Goals

### delete all customers that have no orders. Should delete 17 (or 18 if you haven't deleted the record added) records.
> This is done with a DELETE query

> In the WHERE clause, you can provide another list with an IN keyword this list can be the result of another SELECT query. Write a query to return a list of CustomerIDs that meet the criteria above. Pass that to the IN keyword of the WHERE clause as the list of IDs to be deleted
 
> Use a LEFT JOIN to join the Orders table onto the Customers table and check for a NULL value in the OrderID column

## Create Database and Table

### Keep track of the code you write and paste at the end of this document

- use pgAdmin to create a database, naming it `budget`.
- add an `accounts` table with the following _schema_:

  - `id`, numeric value with no decimal places that should autoincrement.
  - `name`, string, add whatever is necessary to make searching by name faster.
  - `budget` numeric value.

- constraints
  - the `id` should be the primary key for the table.
  - account `name` should be unique.
  - account `budget` is required.
