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

- `SELECT * FROM "Order Details" LIMIT 10;`

RESULTS:
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
  
- `select suppliers.CompanyName, ProductName, UnitPrice FROM Suppliers INNER JOIN Products ON Suppliers.supplierid = Products.supplierid LIMIT 10;`

RESULTS:
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
