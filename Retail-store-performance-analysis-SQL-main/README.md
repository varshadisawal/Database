
# Retail Store Performance Analysis - SQL

## Objective

To analyse transaction history of Retail Store in order to optimally allocate performance bonuses to employees and stores based on their sales, with respect to customers served, products sold, and total cart value.

## Dataset Overview

Dataset Source Link - https://www.kaggle.com/datasets/vivek468/superstore-dataset-final

Refined Dataset Link - https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail_Store_Main.xlsx

Initially, the dataset had **21 columns** and **9994 rows**. I have refined the dataset to minimize the records to  **18 columns** and **9800 rows** for feasibility of my project scope. **6 tables** have been created using this dataset. 

Details of the Refined Dataset - 

| Table Name | Rows | Columns |
| ---------- | ------- | ----- |
| Customer | 8 | 794 |
| Location | 5 | 628 |
| Product | 4 | 1862 |
| Order | 8 | 4923 |
| Employee | 7 | 1500 |
| Transact | 3 | 4923 |

## Data Cleaning

- NULL VALUES : Checked for null values and removed them.
- DUPLICATE DATA : Checked for any duplicated rows and removed them.

## Data Preprocessing

| Table Name | Action | Details |
| ---------- | ------- | ----- |
| Customer | Created 3 new columns  | Phone Number, Gender, Email ID |
| Employee | Created 1 new column | Email ID |

## Relations

Customer (**cstId**, cstFirstName, cstLastName, cstPhone, cstGender, cstEmail, cstSegment) 

Location (**locPostalCode**, locCity, locState, locRegion) 

Product (**prdId**, prdName, prdCategory, prdSubCategory) 

Order (**ordId**, ordDate, ordShipDate, ordShipMode, ordAmount, *empId*, *cstId*) 

Employee (**empId**, empFirstName, empLastName, empAge, empDesignation, empEmail,  *locPostalCode*)

Transact (***ordId, prdId, locPostalCode***)

### Customer table details

Customer : Each customer is described by a unique customer id, customer name, consisting of first name and last name, gender, customer phone number, email address, and the customer segment, eg. home office, corporate etc. 

| Table Name | Action | 
| ---------- | ------- | 
| **CstID** | **Primary Key** of the customer table. Accepts a not null variable character of length 10. |
| cstFirstName | First name of the customer. Accepts a not null variable character of length 20. |
| cstLastName | Last name of the customer. Accepts a not null variable character of length 20. |
| cstPhone | Phone number of the customer. Accepts a variable character of length 15. | 
| cstGender | Gender of the customer. Accepts a character of length 1. | 
| cstEmail | Email of the customer. Accepts a variable character of length 40. | 
| cstSegment | Segment of the customer. Accepts a variable character of length 20. | 

### Location table details

Location : Each store location is identified by a unique postal code, city, state and region.

| Table Name | Action | 
| ---------- | ------- | 
| **locPostalCode** | **Primary Key** of the location table. Accepts a not null variable character of length 6. |
| locCity | City in which the store resides. Accepts a not null variable character of length 30. |
| locState | State in which the store resides. Accepts a not null variable character of length 30. |
| locRegion | Region in which the store resides. Accepts a variable character of length 10. | 

### Product table details

Product : Each product is described by a unique product id, product name, product category and product subcategory.

| Table Name | Action | 
| ---------- | ------- | 
| **prdId** | **Primary Key** of the location table. Accepts a not null variable character of length 20. |
| prdName | Name of the product. Accepts a not null variable character of length 100. |
| prdCategory | Category of the product. Accepts a variable character of length 30. |
| prdSubCategory | Subcategory of the product. Accepts a variable character of length 30. | 

### Employee table details

Employee : Each employee has a unique employee id, employee first name, last name, age, designation, email.

| Table Name | Action | 
| ---------- | ------- | 
| **empId** | **Primary Key** of the employee table. Accepts a not null variable character of length 10.
| empFirstName| Stores the first name of the employee. Accepts a not null variable character of length 20. |
| empLastName | Stores the last name of the employee. Accepts a not null variable character of length 20. |
| empAge | Stores the age of the employee. Accepts a not null integer input. |
| empDesignation | Stores the designation of the employee. Accepts a not null variable character of length 20. |
| empEmail | Stores the email of the employee. Accepts a variable character of length 40. | 
| *locPostalCode* | Stores the postal code of the store location where employee works. This is a foreign key that references to the Location table. Accepts a variable character of length 6.| 

### Order table details

Order : Each product is described by a unique product id, product name, product category and product subcategory.

| Table Name | Action | 
| ---------- | ------- | 
| **ordId** | **Primary Key** of the order table. Accepts a not null variable character of length 20. |
| ordDate| Stores the date on which the order was placed. Accepts a date type input. |
| ordShipDate | Stores the date on which the order was shipped. Accepts a date type input.|
| ordShipMode | Stores the mode in which the order was shipped. Accepts a variable character of length 14. |
| ordAmount | Stores the order amount. Accepts an integer input. |
| *empId* | Stores employee Id of the employee associated with the order. This is a foreign key. References to the Employee table. | 
| *cstID* | Stores customer Id of the customer associated with the order. This is a foreign key. References to the Customer table.| 


### Transact table details

Transact : Each transaction records order Id, product Id, location postal code referencing to the order relation, product relation and location relation respectively.

| Table Name | Action | 
| ---------- | ------- | 
| ***ordId*** | **Composite Primary Key** of the transact table made out of foreign key of order table. Accepts a variable character of length 20. |
| ***prdId***| **Composite Primary key** of the transact table made out of foreign key of product table. Accepts a variable character of length 20. |
| ***locPostalCode*** | **Composite Primary key** of the transact table made out of foreign key of location table. Accepts a variable character of length 6|


### Entity Relationship Diagram

Link - https://lucid.app/lucidchart/c7ba9f38-0b2b-4a14-a9a2-db625b1a85d9/edit?page=0_0&invitationId=inv_14e36bc6-329d-430b-9ea0-c99ce5ee256f#

![Summary_Page](https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail%20Store%20-%20Query%20Screenshots/ERD.png?raw=true)

### Relationships

**Work: binary relationship**

    1 Location to 1 or many Employees
    1 Employee to 0 or 1 Location


**Assist: binary relationship**
    
    1 Employee to 0 or many Orders
    1 Order to 0 or 1 Employee


**Place: binary relationship**

    1 Customer to 1 or many Orders
    1 Order to 1 Customer


**Transact: ternary relationship**

    1 Product and 1 Order to 1 Location
    1 Order and 1 Location to 1 or many Products
    1 Location and 1 Product to 1 or many Orders

## SQL Queries

### Create Queries:

#### Customer Table

    CREATE TABLE OSS_Customer (
	    cstId VARCHAR (10) NOT NULL,
	    cstFirstName VARCHAR (20) NOT NULL,
	    cstLastName VARCHAR (20) NOT NULL,
	    cstPhone VARCHAR (15),
	    cstGender CHAR (1),
	    cstEmail VARCHAR (40),
	    cstSegment VARCHAR (20),
	    CONSTRAINT pk_Customer_cstId PRIMARY KEY (cstId)
        )

#### Location Table
    CREATE TABLE OSS_Location (
	    locPostalCode VARCHAR (6) NOT NULL,
	    locCity VARCHAR (30) NOT NULL,
	    locState VARCHAR (30) NOT NULL,
	    locRegion VARCHAR (10),
	    CONSTRAINT pk_Location_locPostalCode PRIMARY KEY (locPostalCode)
	    )

#### Product Table

    CREATE TABLE OSS_Product (
	    prdId VARCHAR (20) NOT NULL,
	    prdName VARCHAR (100) NOT NULL,
	    prdCategory VARCHAR (30),
	    prdSubCategory VARCHAR (30),
	    CONSTRAINT pk_Product_prdId PRIMARY KEY (prdId)
	    )

#### Employee Table:

    CREATE TABLE OSS_Employee (
	    empId VARCHAR (10) NOT NULL,
	    empFirstName VARCHAR (20) NOT NULL,
	    empLastName VARCHAR (20) NOT NULL,
	    empAge INT NOT NULL,
	    empDesignation VARCHAR (20),
	    empEmail VARCHAR (40),
	    locPostalCode VARCHAR (6),
	    CONSTRAINT pk_Employee_empId PRIMARY KEY (empId),
	    ONSTRAINT fk_Employee_locPostalCode FOREIGN KEY (locPostalCode)
		    REFERENCES  OSS_Location (locPostalCode)
		    ON DELETE SET NULL ON UPDATE CASCADE 
	    )

#### Order Table:

    CREATE TABLE OSS_Order (
	    ordId VARCHAR (20) NOT NULL,
	    ordDate DATE,
	    ordShipDate DATE,
	    ordShipMode VARCHAR (14),
	    ordAmount INT,
	    empId VARCHAR (10),
	    cstId VARCHAR (10) NOT NULL,
	    CONSTRAINT pk_Order_ordId PRIMARY KEY (ordId),
	    CONSTRAINT fk_Order_empId FOREIGN KEY (empId)
		    REFERENCES  OSS_Employee (empID)
		    ON DELETE SET NULL ON UPDATE CASCADE, 
	    CONSTRAINT fk_Order_cstId FOREIGN KEY (cstId)
		    REFERENCES  OSS_Customer (cstID)
		    ON DELETE NO ACTION ON UPDATE CASCADE
	    )

#### Transact Table:

    CREATE TABLE OSS_Transact (
	    ordId VARCHAR (20),
	    prdId VARCHAR (20),
	    locPostalCode VARCHAR (6),
	    CONSTRAINT pk_Transact_ordId_prdId_locPostalCodeId PRIMARY KEY (ordId, prdId, locPostalCode),
	    CONSTRAINT fk_Transact_ordId FOREIGN KEY (ordId)
		    REFERENCES  OSS_Order (ordID)
		    ON DELETE NO ACTION ON UPDATE CASCADE,
	    CONSTRAINT fk_Transact_prdId FOREIGN KEY (prdId)
		    REFERENCES  OSS_Product (prdID)
		    ON DELETE NO ACTION ON UPDATE CASCADE, 
	    CONSTRAINT fk_Transact_locPostalCode FOREIGN KEY (locPostalCode)
		    REFERENCES  OSS_Location (locPostalCode)
		    ON DELETE NO ACTION ON UPDATE NO ACTION 
	    )


### Insert Queries:
#### INSERT INTO Customer Table

**All the insert tables are just examples of what I have done in the INSERT tables.**

    INSERT INTO OSS_Customer
    VALUES
    ('CG-12520','Claire','Gute','6780859887','F','claire.gute@gmail.com','Consumer'),
    ('DV-13045','Darrin','Van Huff','7801448479','M','darrin.van huff@gmail.com','Corporate'),
    ('SO-20335','Sean','ODonnell','2174655175','F','sean.odonnell@gmail.com','Consumer'),
    ('BH-11710','Brosina','Hoffman','4167062315','F','brosina.hoffman@gmail.com','Consumer'),
    ('AA-10480','Andrew','Allen','8419450527','M','andrew.allen@gmail.com','Consumer'),
    ('IM-15070','Irene','Maddox','8090322746','M','irene.maddox@gmail.com','Consumer'),
    ('HP-14815','Harold','Pawlan','3403498607','M','harold.pawlan@gmail.com','Home Office'),
    ('PK-19075','Pete','Kriz','5294497572','F','pete.kriz@gmail.com','Consumer')

#### Output
![Summary_Page](https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail%20Store%20-%20Query%20Screenshots/Insert1.png?raw=true)

### INSERT INTO Location table:
    INSERT INTO OSS_Location
    VALUES
    ('42420','Henderson','Kentucky','South'),
    ('90036','Los Angeles','California','West'),
    ('33311','Fort Lauderdale','Florida','South'),
    ('90032','Los Angeles','California','West'),
    ('28027','Concord','North Carolina','South'),
    ('98103','Seattle','Washington','West'),
    ('76106','Fort Worth','Texas','Central'),
    ('53711','Madison','Wisconsin','Central'),

#### Output
![Summary_Page](https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail%20Store%20-%20Query%20Screenshots/Insert2.png?raw=true)

### INSERT INTO Employee Table:
    INSERT INTO OSS_Employee
    VALUES
    ('1001','Ana','Fuller',41,'Sales Assistant','ana.fuller@gmail.com','94509'),
    ('1002','Clint','Freeman',24,'Sales Assistant','clint.freeman@gmail.com','66502'),
    ('1003','Jamie','Bell',19,'Sales Assistant','jamie.bell@gmail.com','78666'),
    ('1004','Amanda','Wells',44,'Sales Assistant','amanda.wells@gmail.com','7011'),
    ('1005','Kate','Norman',26,'Sales Assistant','kate.norman@gmail.com','49201'),
    ('1006','Tommy','Horton',29,'Sales Assistant','tommy.horton@gmail.com','28027'),
    ('1007','Jennie','Webb',26,'Sales Assistant','jennie.webb@gmail.com','55044'),
    ('1008','Jackie','Long',41,'Sales Assistant','jackie.long@gmail.com','53142'),

#### Output
![Summary_Page](https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail%20Store%20-%20Query%20Screenshots/Insert3.png?raw=true)

#### INSERT INTO Order Table:

    INSERT INTO OSS_Order
    VALUES
    ('CA-2018-114412','2018/04/15','2018/04/20','Standard Class',15.552,'1001','AA-10480'),
    ('US-2018-156909','2018/07/16','2018/07/18','Second Class',71.372,'1002','AG-10270'),
    ('CA-2016-106320','2016/09/25','2016/09/30','Standard Class',1044.63,'1003','BH-11710'),
    ('CA-2017-121755','2017/01/16','2017/01/17','Second Class',102.218,'1004','CG-12520'),
    ('US-2016-150630','2016/09/17','2016/09/21','Standard Class',3329.434,'1005','DV-13045'),
    ('CA-2016-117415','2016/12/27','2016/12/31','Standard Class',1228.9532,'1006','EB-13870')

#### Output
![Summary_Page](https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail%20Store%20-%20Query%20Screenshots/Insert4.png?raw=true)

#### INSERT INTO Product Table:

    INSERT INTO OSS_Product
    VALUES
    ('OFF-PA-10002365','Xerox 1967','Office Supplies','Paper'),
    ('TEC-AC-10003027','Imation 8GB Mini TravelDrive USB 2.0 Flash Drive','Technology','Accessories'),
    ('FUR-BO-10002545','Atlantic Metals Mobile 3-Shelf Bookcases, Custom Colors','Furniture','Bookcases'),
    ('FUR-TA-10000577','Bretford CR4500 Series Slim Rectangular Table','Furniture','Tables'),
    ('FUR-BO-10000112','Bush Birmingham Collection Bookcase, Dark Cherry','Furniture','Bookcases'),
    ('FUR-BO-10000330','Sauder Camden County Barrister Bookcase, Planked Cherry Finish','Furniture','Bookcases'),
    ('FUR-BO-10000362','Sauder Inglewood Library Bookcases','Furniture','Bookcases'),
    ('FUR-BO-10000468','OSullivan 2-Shelf Heavy-Duty Bookcases','Furniture','Bookcases')

#### Output
![Summary_Page](https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail%20Store%20-%20Query%20Screenshots/Insert5.png?raw=true)

#### INSERT INTO Transact Table:

    INSERT INTO OSS_Transact
    VALUES
    ('CA-2016-106320','FUR-TA-10000577','84057'),
    ('CA-2016-117415','FUR-BO-10002545','77041'),
    ('CA-2017-121755','TEC-AC-10003027','90049'),
    ('CA-2018-114412','OFF-PA-10002365','28027')

#### Output
![Summary_Page](https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail%20Store%20-%20Query%20Screenshots/Insert6.png?raw=true)

### Drop Queries:
    DROP TABLE IF EXISTS OSS_Transact;
    DROP TABLE IF EXISTS OSS_Order;
    DROP TABLE IF EXISTS OSS_Employee;
    DROP TABLE IF EXISTS OSS_Product;
    DROP TABLE IF EXISTS OSS_Location;
    DROP TABLE IF EXISTS OSS_Customer;

### Business Transactions SQL Queries and Outputs:

#### Query 1:
**What are the top performing stores in the United States?**

    SELECT Top 10 p.locPostalCode AS 'Postal Code', l.locCity AS 'City', l.locState AS 'State', l.locRegion AS 'Region', SUM(o.ordAmount) as 'Total Sales ($)'

    FROM OSS_Order o, (SELECT DISTINCT ordId, locPostalCode FROM OSS_Transact) p, OSS_Location l

    WHERE o.ordId = p.ordId and p.locPostalCode = l.locPostalCode

    GROUP BY p.locPostalCode, l.locCity, l.locState, l.locRegion

    ORDER BY SUM(o.ordAmount) DESC

#### Output:
![Summary_Page](https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail%20Store%20-%20Query%20Screenshots/OutputQ1.png?raw=true)

#### Query 2:

**What are the top 10 highest selling products based on quantity sold?**
    
    SELECT TOP 10  p.prdId, p.prdName, p.prdCategory, p.prdSubCategory, COUNT(t.ordId) as "Quantity Sold"
    FROM OSS_Transact t, OSS_Product p
    WHERE t.prdId = p.prdId
    GROUP BY p.prdId, p.prdName, p.prdCategory, p.prdSubCategory
    ORDER BY COUNT(t.ordId) DESC

#### Output:
![Summary_Page](https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail%20Store%20-%20Query%20Screenshots/OutputQ2.png?raw=true)

#### Query 3:

**What are the top 10 highest selling products based on revenue?**
    
    SELECT TOP 10 p.prdId, p.prdName, p.prdCategory, p.prdSubCategory, SUM(o.ordAmount) AS "Total Sales ($)"
    FROM OSS_Transact t, OSS_Order o, OSS_Product p
    WHERE t.ordId = o.ordId AND t.prdId = p.prdId
    GROUP BY p.prdId, p.prdName, p.prdCategory, p.prdSubCategory
    ORDER by SUM(o.ordAmount) DESC

#### Output:

![Summary_Page](https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail%20Store%20-%20Query%20Screenshots/OutputQ3.png?raw=true)

#### Query 4:

**What are the lowest 10 selling products based on quantity sold?**
    
    SELECT TOP 10 p.prdId, p.prdName, p.prdCategory, p.prdSubCategory, COUNT(t.ordId) as  "Quantity Sold"
    FROM OSS_Transact t, OSS_Product p
    WHERE t.prdId = p.prdId
    GROUP BY p.prdId, p.prdName, p.prdCategory, p.prdSubCategory
    ORDER BY COUNT(t.ordId) ASC

#### Output:
![Summary_Page](https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail%20Store%20-%20Query%20Screenshots/OutputQ4.png?raw=true)

#### Query 5:

**What are the 10 lowest selling products based on revenue?**
    
    SELECT TOP 10 p.prdId, p.prdName, p.prdCategory, p.prdSubCategory, SUM(o.ordAmount) AS "Total Sales ($)"
    FROM OSS_Transact t, OSS_Order o, OSS_Product p
    WHERE t.ordId = o.ordId AND t.prdId = p.prdId
    GROUP BY p.prdId, p.prdName, p.prdCategory, p.prdSubCategory
    ORDER by SUM(o.ordAmount) ASC

#### Output:

![Summary_Page](https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail%20Store%20-%20Query%20Screenshots/OutputQ5.png?raw=true)

#### Query 6:

**What is the highest revenue generating segment of customers?**
    
    WITH Revenue (Customer_Segment, TotalRevenue) AS
    (
        SELECT c.cstSegment, SUM(o.ordAmount) AS 'Revenue ($)'
        FROM OSS_Customer c, OSS_Order o
        WHERE o.cstId = c.cstId
        GROUP BY c.cstSegment
    )
    SELECT r.Customer_Segment, r.TotalRevenue
    FROM Revenue r
    ORDER BY r.TotalRevenue DESC


#### Output:

![Summary_Page](https://github.com/nikunjachoure/Retail-store-performance-analysis-SQL/blob/main/Retail%20Store%20-%20Query%20Screenshots/OutputQ6.png?raw=true)
