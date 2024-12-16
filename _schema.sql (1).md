SETUP FLIPKART DATABASE SCHEMA

DROP TABLE IF EXISTS payments, shippings, sales, products, customers;

CREATE TABLE customers  
(  
	customer\_id	INT PRIMARY KEY,  
	customer\_name	VARCHAR(35),  
	state VARCHAR(25)  
);

CREATE TABLE products  
(  
	product\_id INT PRIMARY KEY,	  
	product\_name	VARCHAR(45),  
	price	FLOAT,  
	cogs	FLOAT,  
	category	VARCHAR(25),  
	brand VARCHAR(25)  
);

CREATE TABLE sales  
(  
order\_id	INT PRIMARY KEY,  
order\_date date,	  
customer\_id	INT REFERENCES customers(customer\_id),  
order\_status VARCHAR(25),	  
product\_id	INT REFERENCES products(product\_id),  
quantity	INT,   
price\_per\_unit FLOAT  
\-- ,CONSTRAINT customer\_id\_cust FOREIGN KEY (customer\_id) REFERENCES customers(customer\_id),  
\-- CONSTRAINT product\_id\_prod FOREIGN KEY (product\_id) REFERENCES products(product\_id)  
);

CREATE TABLE payments  
(  
payment\_id	INT,  
order\_id	INT REFERENCES sales(order\_id),  
payment\_date	date,  
payment\_status VARCHAR(55)  
);

CREATE TABLE shippings  
(  
shipping\_id INT,	  
order\_id	INT REFERENCES sales(order\_id),  
shipping\_date	DATE,  
return\_date	 DATE,  
shipping\_providers VARCHAR(55),	  
delivery\_status VARCHAR(55)	  
);

SELECT 'Flipkart Database created successfull\!';

