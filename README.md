# ark1979-DbaAssign4
Excercise 1 - user privileges

Inserting users

CREATE USER 'Inventory'@'localhost' IDENTIFIED BY 'inv123';

CREATE USER 'Bookkeeping'@'localhost' IDENTIFIED BY 'book123';

CREATE USER 'hr'@'localhost' IDENTIFIED BY 'hr123';
CREATE USER 'Sales'@'localhost' IDENTIFIED BY 'sales123';
CREATE USER 'IT'@'localhost' IDENTIFIED BY 'it123';
Granting privileges
GRANT SELECT, UPDATE, INSERT  ON classicmodels.products TO 'Inventory'@'localhost';
GRANT SELECT, UPDATE, INSERT  ON classicmodels.productlines TO 'Inventory'@'localhost';

GRANT SELECT ON classicmodels.orders TO 'Bookkeeping'@'localhost';
GRANT SELECT ON classicmodels.orderdetails TO 'Bookkeeping'@'localhost';

GRANT SELECT, UPDATE, INSERT ON classicmodels.employees TO 'hr'@'localhost';
GRANT SELECT, UPDATE, INSERT ON classicmodels.employees TO 'hr'@'localhost';

GRANT SELECT, UPDATE, INSERT ON classicmodels.orders TO 'Sales'@'localhost';
GRANT SELECT, UPDATE, INSERT ON classicmodels.orderdetails TO 'Sales'@'localhost';

GRANT ALL ON classicmodels.* TO 'IT'@'localhost';

FLUSH PRIVILEGES;
Why theses privileges?
Inventory - needs to manage products and product lines
Bookkeeping - just needs to be able to view oders & details
HR - they are managing employees and offices
Sales - in theory only needs to create orders but they should also be able to correct their mistakes in orders wihtout having to contact IT
IT - needs all access because they are IT
Exercise 2 - logging
Creating users:
| 17:00:47 | root[root] @ localhost []   | Query        | CREATE USER 'Inventory'@'localhost' IDENTIFIED WITH 'mysql_native_password' AS '<secret>'                                              |
| 17:00:47 | root[root] @ localhost []   | Query        | CREATE USER 'Bookkeeping'@'localhost' IDENTIFIED WITH 'mysql_native_password' AS '<secret>'                                            |
| 17:00:47 | root[root] @ localhost []   | Query        | CREATE USER 'hr'@'localhost' IDENTIFIED WITH 'mysql_native_password' AS '<secret>'                                                     |
| 17:00:47 | root[root] @ localhost []   | Query        | CREATE USER 'Sales'@'localhost' IDENTIFIED WITH 'mysql_native_password' AS '<secret>'                                                  |
| 17:00:47 | root[root] @ localhost []   | Query        | CREATE USER 'IT'@'localhost' IDENTIFIED WITH 'mysql_native_password' AS '<secret>'  
Granting privileges
| 17:02:23 | root[root] @ localhost []             | Query        | GRANT SELECT, UPDATE, INSERT  ON classicmodels.products TO 'Inventory'@'localhost'                                                     |
| 17:02:23 | root[root] @ localhost []             | Query        | GRANT SELECT, UPDATE, INSERT  ON classicmodels.productlines TO 'Inventory'@'localhost'                                                 |
| 17:02:23 | root[root] @ localhost []             | Query        | GRANT SELECT ON classicmodels.orders TO 'Bookkeeping'@'localhost'                                                                      |
| 17:02:23 | root[root] @ localhost []             | Query        | GRANT SELECT ON classicmodels.orderdetails TO 'Bookkeeping'@'localhost'                                                                |
| 17:02:23 | root[root] @ localhost []             | Query        | GRANT SELECT, UPDATE, INSERT ON classicmodels.employees TO 'hr'@'localhost'                                                            |
| 17:02:23 | root[root] @ localhost []             | Query        | GRANT SELECT, UPDATE, INSERT ON classicmodels.employees TO 'hr'@'localhost'                                                            |
| 17:02:23 | root[root] @ localhost []             | Query        | GRANT SELECT, UPDATE, INSERT ON classicmodels.orders TO 'Sales'@'localhost'                                                            |
| 17:02:23 | root[root] @ localhost []             | Query        | GRANT SELECT, UPDATE, INSERT ON classicmodels.orderdetails TO 'Sales'@'localhost'                                                      |
| 17:02:23 | root[root] @ localhost []             | Query        | GRANT ALL ON classicmodels.* TO 'IT'@'localhost'                                                                                       |
| 17:02:23 | root[root] @ localhost []             | Query        | FLUSH PRIVILEGES  
3 queries
| 17:05:24 | root[root] @ localhost [] | Query        | INSERT INTO `employees` (`employeeNumber`, `lastName`, `firstName`, `extension`, `email`, `officeCode`, `reportsTo`, `jobTitle`) VALUES ('2234324', 'dmd', 'eef', 'sef', 'fdf@ßdf', '4', '1286', 'sdffe')  |
| 17:05:16 | root[root] @ localhost [] | Query        | INSERT INTO `employees` (`employeeNumber`, `lastName`, `firstName`, `extension`, `email`, `officeCode`, `reportsTo`, `jobTitle`) VALUES ('2324', 'dmd', 'eef', 'sef', 'fdf@ßdf', '4', '1286', 'sdffe')     |
| 17:05:04 | root[root] @ localhost [] | Query        | INSERT INTO `employees` (`employeeNumber`, `lastName`, `firstName`, `extension`, `email`, `officeCode`, `reportsTo`, `jobTitle`) VALUES ('234324', 'dmd', 'eef', 'sef', 'fdf@ßdf', '4', '1286', 'sdffe')  |

| 17:07:21 | root[root] @ localhost []             | Query        | INSERT INTO `products` (`productCode`, `productName`, `productLine`, `productScale`, `productVendor`, `productDescription`, `quantityInStock`, `buyPrice`, `MSRP`) VALUES ('23433', 'sdsddf', 'Motorcycles', 'sdcse', 'esf', 'sed', '2323', '233', '34') |

| 17:09:09 | root[root] @ localhost []             | Query        | INSERT INTO `products` (`productCode`, `productName`, `productLine`, `productScale`, `productVendor`, `productDescription`, `quantityInStock`, `buyPrice`, `MSRP`) VALUES ('23sd3', 'sdsddf', 'Motorcycles', 'sdcse', 'esf', 'sed', '2323', '233', '34')                                                                                                                                                                                                                                                                                                               |


| 17:11:14 | Sales[Sales] @ localhost [] | Query        | drop database customers                                                                                                                |
Exercise 3 - backup and recovery
I did a logical dump using mysqldump.
