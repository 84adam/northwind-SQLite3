# northwind-SQLite3

This is a version of the Microsoft Access 2000 Northwind sample database, re-engineered for SQLite3.

The Northwind sample database was provided with Microsoft Access as a tutorial schema for managing small business customers, orders, inventory, purchasing, suppliers, shipping, and employees. Northwind is an excellent tutorial schema for a small-business ERP, with customers, orders, inventory, purchasing, suppliers, shipping, employees, and single-entry accounting.

All the TABLES and VIEWS from the MSSQL-2000 version have been converted to Sqlite3 and included here. Also included are two versions prepopulated with data - a small verison and a large version. Should you decide to, you can use the included python script to pump the database full of more data.

![alt tag](https://raw.githubusercontent.com/jpwhite3/northwind-SQLite3/master/Northwind_ERD.png)

## Installation

To use this database, follow these steps:

1. Download this code repository and extract the archive: `wget -O northwind-SQLite3.zip https://github.com/84adam/northwind-SQLite3/archive/master.zip ; unzip -j northwind-SQLite3.zip -d northwind-SQLite3 ; cd northwind-SQLite3 ; ls`
2. Create a new local database: `sqlite3 Northwind.db`
3. Run the script to create the tables and fill them with data: `.read Northwind_Sqlite.sql`
4. Now you can execute queries such as those shown below:

- **Ex. #1: Select All**
```
SELECT *
FROM "Order Details"
LIMIT 10;
```

- RESULTS:
```
OrderID|ProductID|UnitPrice|Quantity|Discount
10248|11|14|12|0.0
10248|42|9.8|10|0.0
10248|72|34.8|5|0.0
10249|14|18.6|9|0.0
10249|51|42.4|40|0.0
10250|41|7.7|10|0.0
10250|51|42.4|35|0.15
10250|65|16.8|15|0.15
10251|22|16.8|6|0.05
10251|57|15.6|15|0.05
```
  
- **Ex. #2: Inner Join**
```
select suppliers.CompanyName, ProductName, UnitPrice
FROM Suppliers
INNER JOIN Products ON Suppliers.supplierid = Products.supplierid
LIMIT 10;
```

- RESULTS:
```
CompanyName|ProductName|UnitPrice
Exotic Liquids|Chai|18
Exotic Liquids|Chang|19
Exotic Liquids|Aniseed Syrup|10
New Orleans Cajun Delights|Chef Anton's Cajun Seasoning|22
New Orleans Cajun Delights|Chef Anton's Gumbo Mix|21.35
Grandma Kelly's Homestead|Grandma's Boysenberry Spread|25
Grandma Kelly's Homestead|Uncle Bob's Organic Dried Pears|30
Grandma Kelly's Homestead|Northwoods Cranberry Sauce|40
Tokyo Traders|Mishi Kobe Niku|97
Tokyo Traders|Ikura|31
```

- **Ex. #3: Inner Join with 3 Tables**
```
SELECT o.OrderID, c.CompanyName, e.LastName
FROM ((Orders o INNER JOIN Customers c ON o.CustomerID = c.CustomerID)
INNER JOIN Employees e ON o.EmployeeID = e.EmployeeID)
LIMIT 10;
```

- RESULTS:

```
OrderID|CompanyName|LastName
10248|Vins et alcools Chevalier|Buchanan
10249|Toms Spezialit�ten|Suyama
10250|Hanari Carnes|Peacock
10251|Victuailles en stock|Leverling
10252|Supr�mes d�lices|Peacock
10253|Hanari Carnes|Leverling
10254|Chop-suey Chinese|Buchanan
10255|Richter Supermarkt|Dodsworth
10256|Wellington Importadora|Leverling
10257|HILARION-Abastos|Peacock
```

- **Ex. #4: Working with Strings (Generate 'UserName' from FirstName + LastName + EmployeeID)**

```
SELECT
    EmployeeID
    ,FirstName
    ,LastName
    ,LOWER(SUBSTR(FirstName,1,1)||SUBSTR(LastName,1,8))||EmployeeID AS UserName
FROM Employees;
```

- RESULTS:

```
EmployeeID|FirstName|LastName|UserName
1|Nancy|Davolio|ndavolio1
2|Andrew|Fuller|afuller2
3|Janet|Leverling|jleverlin3
4|Margaret|Peacock|mpeacock4
5|Steven|Buchanan|sbuchanan5
6|Michael|Suyama|msuyama6
7|Robert|King|rking7
8|Laura|Callahan|lcallahan8
9|Anne|Dodsworth|adodswort9
```
