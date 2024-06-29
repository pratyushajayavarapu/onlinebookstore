# onlinebookstore
### Authors
| Attribute        | Type        |
|------------------|-------------|
| Author_id        | INT         |
| First_name       | VARCHAR(255)|
| Last_name        | VARCHAR(255)|
| Date_Of_Birth    | DATE		 |
| Country_Of_Origin| VARCHAR(255)|
| Genre            | VARCHAR(255)|
| Books_published  | INT         |
| Years_active     | INT         |

### Customers
| Attribute       | Type        |
|-----------------|-------------|
| Customer_id     | INT         |
| First_name      | VARCHAR(255)|
| Last_name       | VARCHAR(255)|
| Date_Of_Birth   | DATE        |
| Gender          | VARCHAR(255)|
| Email           | VARCHAR(255)|
| Phone_Number    | VARCHAR(255)|
| Address         | VARCHAR(255)|
| Amount_spent    | DECIMAL(10,2)|
| Last_purchase   | DATE        |


### Books
| Attribute        | Type        |
|------------------|-------------|
| Book_id          | INT         |
| Title            | VARCHAR(255)|
| Genre            | VARCHAR(100)|
| ISBN             | VARCHAR(100)|
| Description      | VARCHAR(100)|
| Author_id        | INT         |
| Price            | DECIMAL(10,2)|
| Publish_date     | DATE        |


### Reviews
| Attribute        | Type        |
|------------------|-------------|
| Review_id        | INT         |
| Book_id          | INT         |
| Customer_id      | INT         |
| Review_text      | VARCHAR(100)|
| Rating      	   | VARCHAR(100)|
| Review_date      | DATE        |


### Orders
| Attribute        | Type        |
|------------------|-------------|
| order_id         | INT         |
| Customer_id      | INT         |
| total_amount     | DECIMAL(10, 2)|
| order_date       | DATE        |
| Shipping_address  | VARCHAR(255)|
| Billing_address   | VARCHAR(255)|
| Tracking_number   | INT         |
| Order_status      | VARCHAR(255)|


### Order_Items
| Attribute        | Type        |
|------------------|-------------|
| order_item_id    | INT         |
| order_id         | INT         |
| book_id          | INT         |
| quantity         | INT         |

**### Created Tables for the above Attributes:** 

CREATE TABLE Authors (
    Author_id INT PRIMARY KEY,
    First_name VARCHAR(255) NOT NULL,
	Last_name VARCHAR(255) NOT NULL,
	Date_of_birth DATE NOT NULL,
	Country_of_origin VARCHAR(255) NOT NULL,
	Genre VARCHAR(255) NOT NULL,
	Books_published INT NOT NULL,
    Years_active INT NOT NULL
);


CREATE TABLE Customers (
    Customer_id INT PRIMARY KEY,
    First_name VARCHAR(255) NOT NULL,
    Last_name VARCHAR(255) NOT NULL,
	Date_of_birth DATE NOT NULL,
	Gender VARCHAR(255) NOT NULL,
    Email VARCHAR(255) NOT NULL,
	Phone_number VARCHAR(255) NOT NULL,
	Address VARCHAR(255) NOT NULL,
    Amount_spent DECIMAL(10, 2) DEFAULT 0,
    Last_purchase DATE NOT NULL
);


CREATE TABLE Books (
    book_id INT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
	genre VARCHAR(100) NOT NULL,
	ISBN VARCHAR(255) NOT NULL,
	Description VARCHAR(255) NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    publish_date DATE NOT NULL,
    author_id INT,
    FOREIGN KEY (author_id) REFERENCES Authors(author_id)
);


CREATE TABLE Reviews (
    review_id INT PRIMARY KEY,
    book_id INT,
    customer_id INT,
    rating INT CHECK (rating BETWEEN 1 AND 5),
    review_text VARCHAR(100),
    review_date DATE NOT NULL,
    FOREIGN KEY (book_id) REFERENCES Books(book_id),
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);


CREATE TABLE Orders (
    Order_id INT PRIMARY KEY,
    Customer_id INT,
    Order_date DATE NOT NULL,
    Total_amount DECIMAL(10, 2) NOT NULL,
	Shipping_address VARCHAR(255),
	Billing_address  VARCHAR(255),
	Tracking_number INT,
	Order_status VARCHAR(255),
    FOREIGN KEY (Customer_id) REFERENCES Customers(Customer_id)
);


CREATE TABLE Order_Items (
    order_item_id INT PRIMARY KEY,
    order_id INT,
    book_id INT,
    quantity INT NOT NULL,
    FOREIGN KEY (order_id) REFERENCES Orders(order_id),
    FOREIGN KEY (book_id) REFERENCES Books(book_id)
);

**###DDL Queries for Create Table:**

CREATE TABLE Customers (
    Customer_id INT PRIMARY KEY,
    First_name VARCHAR(255) NOT NULL,
    Last_name VARCHAR(255) NOT NULL,
	Date_Of_Birth DATE NOT NULL,
	Gender VARCHAR(255) NOT NULL,
    Email VARCHAR(255) UNIQUE NOT NULL,
	Phone_Number VARCHAR(255) UNIQUE NOT NULL,
	Address VARCHAR(255) NOT NULL,
    Amount_spent DECIMAL(10, 2) DEFAULT 0,
    Last_purchase DATE NOT NULL
);


**###DML: Insert Sample Data into Customers Table:**

INSERT INTO Customers (Customer_id, First_name, Last_name, Date_Of_Birth, Gender, Email, Phone_Number, Address, Amount_spent, Last_purchase) VALUES
(1, 'Alice', 'Johnson', '1940-08-05', 'Female', 'alice@example.com', '123-456-7890', '123 Main St', 150.75, '2022-05-10'),
(2, 'Bob', 'Williams', '1964-07-13', 'Male', 'bob@example.com', '098-765-4321', '456 Elm St', 200.00, '2018-01-25');
(3, 'John', 'Doe', '1980-05-12', 'Male', 'john.doe@example.com', '555-1234', '123 Elm St', 150.75, '2023-12-20'),
(4, 'Jane', 'Smith', '1992-08-30', 'Female', 'jane.smith@example.com', '555-5678', '456 Oak St', 250.00, '2024-01-15'),
(5, 'Jerry', 'Johnson', '1985-03-25', 'Female', 'alice.johnson@example.com', '555-9101', '789 Pine St', 325.50, '2024-02-10');
(6, 'Tom', 'Johnson', '1987-03-25', 'Female', 'alice.johnson@example.com', '555-9101', '799 Pine St', 325.50, '2024-02-10');


SELECT * FROM Customers WHERE customer_id = 3;


UPDATE Customers 
SET Address = '123 Larch Street' 
WHERE customer_id = 3;

DELETE FROM Customers WHERE customer_id = 3;

