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

