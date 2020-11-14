# ict2task
SQL code for OLX database
--creating database
--location of company or product
CREATE TABLE Location
(
location_id int  not null,
location_city char(25),
PRIMARY KEY (location_id)
);
CREATE TABLE Customers
(
F_Name char(255) not null,
L_Name char(255) not null,
Verification bool not null,
Customers_id int  not null,
PRIMARY KEY (Customers_id)
);
--The company that publishes about the search for employees for such a position
CREATE TABLE Company
(
Company_id int not null,
Company_name varchar(50) not null,
Company_type varchar(50) not null,
location_id int not null,
FOREIGN KEY (location_id) REFERENCES Location (location_id),
PRIMARY KEY (Company_id)
);
--job vacancy
CREATE TABLE Company_vacancy
(
Vacancy_id int not null,
position char (255) not null,
description char(255),
min_Salary DECIMAL(25)not null,
max_Salary DECIMAL(25)not null,
Company_id int not null,
FOREIGN KEY (Company_id) REFERENCES Company (Company_id),
PRIMARY KEY (Vacancy_id)
);

CREATE TABLE Product_Category
(
Category_id int  not null,
Category char(50) not null,
PRIMARY KEY (Category_id)
);

CREATE TABLE Product_Status
(
Status_id int not null,
VIP bool not null,
used bool not null,
sold bool not null,
PRIMARY KEY (Status_id)
);

CREATE TABLE Product
(
Product_id int not null,
Product_name char (255) not null,
Description char(255) not null,
Product_Cost int  not null,
Category_id int  not null,
Status_id int  not null,
location_id int  not null,
PRIMARY KEY (Product_id),
FOREIGN KEY (Category_id) REFERENCES Product_Category (Category_id),
FOREIGN KEY (Status_id) REFERENCES Product_Status (Status_id),
FOREIGN KEY (location_id) REFERENCES Location (location_id)
);
CREATE TABLE Product_Photo
(
Photo_id int  not null,
Product_URL Char(255) not null,
Product_id int  not null,
FOREIGN KEY (Product_id) REFERENCES Product (Product_id),
PRIMARY KEY (Photo_id)
);
CREATE TABLE Salesman
(
Salesman_id int  not null,
First_Name char(255) not null,
Last_Name char(255) not null,
Verification bool not null,
Phone_Number DECIMAL(12) not null,
Product_id int  not null,
FOREIGN KEY (Product_id) REFERENCES Product (Product_id),
PRIMARY KEY (Salesman_id)
);
CREATE TABLE Order_Info
(
Order_id int not null,
Salesman_id int not null,
Customers_id int not null,
Product_id int not null,
delivered_status bool not null,
PRIMARY KEY (Order_id)
FOREIGN KEY (Salesman_id) REFERENCES Salesman (Salesman_id),
FOREIGN KEY (Customers_id) REFERENCES Customers (Customers_id),
FOREIGN KEY (Product_id) REFERENCES Product (Product_id),
);


