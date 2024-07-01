# onlinebookstore
 **Clearly title and identify the tables required and what type each of the attribute is**
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
**code block containing only valid SQL syntax which will create your sample data base **

```sql
CREATE TABLE authors
  (
     author_id         INT PRIMARY KEY,
     first_name        VARCHAR(255) NOT NULL,
     last_name         VARCHAR(255) NOT NULL,
     date_of_birth     DATE NOT NULL,
     country_of_origin VARCHAR(255) NOT NULL,
     genre             VARCHAR(255) NOT NULL,
     books_published   INT NOT NULL,
     years_active      INT NOT NULL
  ); 
```


```sql
CREATE TABLE customers
  (
     customer_id   INT PRIMARY KEY,
     first_name    VARCHAR(255) NOT NULL,
     last_name     VARCHAR(255) NOT NULL,
     date_of_birth DATE NOT NULL,
     gender        VARCHAR(255) NOT NULL,
     email         VARCHAR(255) NOT NULL,
     phone_number  VARCHAR(255) NOT NULL,
     address       VARCHAR(255) NOT NULL,
     amount_spent  DECIMAL(10, 2) DEFAULT 0,
     last_purchase DATE NOT NULL
  );
``` 



```sql
CREATE TABLE books
  (
     book_id      INT PRIMARY KEY,
     title        VARCHAR(255) NOT NULL,
     genre        VARCHAR(100) NOT NULL,
     isbn         VARCHAR(255) NOT NULL,
     description  VARCHAR(255) NOT NULL,
     price        DECIMAL(10, 2) NOT NULL,
     publish_date DATE NOT NULL,
     author_id    INT,
     FOREIGN KEY (author_id) REFERENCES authors(author_id)
  );
```


```sql
CREATE TABLE reviews
  (
     review_id   INT PRIMARY KEY,
     book_id     INT,
     customer_id INT,
     rating      INT CHECK (rating BETWEEN 1 AND 5),
     review_text VARCHAR(100),
     review_date DATE NOT NULL,
     FOREIGN KEY (book_id) REFERENCES books(book_id),
     FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
  );

```

```sql
CREATE TABLE orders
  (
     order_id         INT PRIMARY KEY,
     customer_id      INT,
     order_date       DATE NOT NULL,
     total_amount     DECIMAL(10, 2) NOT NULL,
     shipping_address VARCHAR(255),
     billing_address  VARCHAR(255),
     tracking_number  INT,
     order_status     VARCHAR(255),
     FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
  ); 
```


```sql
CREATE TABLE order_items
  (
     order_item_id INT PRIMARY KEY,
     order_id      INT,
     book_id       INT,
     quantity      INT NOT NULL,
     FOREIGN KEY (order_id) REFERENCES orders(order_id),
     FOREIGN KEY (book_id) REFERENCES books(book_id)
  ); 
```

**set of DDL/DML For customers tables**


```sql
CREATE TABLE customers
  (
     customer_id   INT PRIMARY KEY,
     first_name    VARCHAR(255) NOT NULL,
     last_name     VARCHAR(255) NOT NULL,
     date_of_birth DATE NOT NULL,
     gender        VARCHAR(255) NOT NULL,
     email         VARCHAR(255) UNIQUE NOT NULL,
     phone_number  VARCHAR(255) UNIQUE NOT NULL,
     address       VARCHAR(255) NOT NULL,
     amount_spent  DECIMAL(10, 2) DEFAULT 0,
     last_purchase DATE NOT NULL
  );

```

**INSERT Query:**
```sql
INSERT INTO Customers (Customer_id, First_name, Last_name, Date_Of_Birth, Gender, Email, Phone_Number, Address, Amount_spent, Last_purchase) VALUES
(1, 'Alice', 'Johnson', '1940-08-05', 'Female', 'alice@example.com', '123-456-7890', '123 Main St', 150.75, '2022-05-10'),
(2, 'Bob', 'Williams', '1964-07-13', 'Male', 'bob@example.com', '098-765-4321', '456 Elm St', 200.00, '2018-01-25');
(3, 'John', 'Doe', '1980-05-12', 'Male', 'john.doe@example.com', '555-1234', '123 Elm St', 150.75, '2023-12-20'),
(4, 'Jane', 'Smith', '1992-08-30', 'Female', 'jane.smith@example.com', '555-5678', '456 Oak St', 250.00, '2024-01-15'),
(5, 'Jerry', 'Johnson', '1985-03-25', 'Female', 'alice.johnson@example.com', '555-9101', '789 Pine St', 325.50, '2024-02-10');
(6, 'Tom', 'Johnson', '1987-03-25', 'Female', 'alice.johnson@example.com', '555-9101', '799 Pine St', 325.50, '2024-02-10');

```
**SELECT QUERY:**
```sql
SELECT * FROM Customers WHERE customer_id = 3;

```
**UPDATE QUERY:**
```sql
UPDATE Customers 
SET Address = '123 Larch Street' 
WHERE customer_id = 3;

```
**DELETE QUERY:**
```sql
DELETE FROM Customers WHERE customer_id = 3;
```
**Power writers (authors) with more than X books in the same genre published within the last X years **
```sql
SELECT 
    a.author_id, 
    a.genre, 
    COUNT(b.book_id) AS book_count
FROM 
    Authors a
JOIN 
    Books b ON a.author_id = b.author_id
WHERE 
    b.publish_date >= CURRENT_DATE - INTERVAL '5 years'
GROUP BY 
    a.author_id,a.genre
HAVING 
    COUNT(b.book_id) > 1;

```
    

**Loyal Customers who has spent more than X dollars in the last year**
```sql
SELECT customer_id, First_name, Last_name, Email, Amount_spent,Last_purchase
FROM Customers
WHERE Amount_spent > 200 AND Last_purchase >= CURRENT_DATE - INTERVAL '1 year';

```

**Well Reviewed books that has a better user rating than average**
```sql
SELECT B.book_id,b.title,R.rating
FROM Books B
JOIN Reviews R ON B.book_id = R.book_id
where R.rating > (SELECT AVG(rating) FROM Reviews);

```

**The most popular genre by sales**
```sql
SELECT books.genre, SUM(order_items.quantity ) AS total_sales
FROM Books books
JOIN Order_Items order_items ON books.book_id = order_items.book_id
GROUP BY genre
ORDER BY total_sales DESC
LIMIT 1;

```
**The 10 most recent posted reviews by Customers**
```sql
SELECT review_id, book_id, customer_id, rating, review_text, review_date
FROM Reviews
ORDER BY review_date DESC
LIMIT 10;

```

**Create a Typescript interface that will allow modification to a table.**

import { Pool } from 'pg';

// Configure the PostgreSQL connection
const pool = new Pool({
    user: postgres,
    host: localhost,
    database: online_Book_Store,
    password: password,
    port: 5432,
});

// TypeScript interface for the Books table
interface Book {
    book_id: number;
    title: string;
    genre: string;
    isbn: string;
    description: string;
    author_id: number;
    price: number;
    publish_date: string;
}

// Create a new book
async function createBook(book: Book): Promise<void> {
    const query = `
        INSERT INTO Books (book_id, title, genre, isbn, description, author_id, price, publish_date)
        VALUES ($1, $2, $3, $4, $5, $6, $7, $8)
    `;
    const values = [book.book_id, book.title, book.genre, book.isbn, book.description, book.author_id, book.price, book.publish_date];
    
    try {
        await pool.query(query, values);
        console.log('Book created successfully');
    } catch (err) {
        console.error('Error creating book:', err);
    }
}

// Read a book
async function readBook(book_id: number): Promise<Book | null> {
    const query = 'SELECT * FROM Books WHERE book_id = $1';
    
    try {
        const res = await pool.query(query, [book_id]);
        if (res.rows.length) {
            return res.rows[0] as Book;
        } else {
            console.log('Book not found');
            return null;
        }
    } catch (err) {
        console.error('Error reading book:', err);
        return null;
    }
}

// Update a book
async function updateBook(book: Book): Promise<void> {
    const query = `
        UPDATE Books
        SET title = $1, genre = $2, isbn = $3, description = $4, author_id = $5, price = $6, publish_date = $7
        WHERE book_id = $8
    `;
    const values = [book.title, book.genre, book.isbn, book.description, book.author_id, book.price, book.publish_date, book.book_id];
    
    try {
        await pool.query(query, values);
        console.log('Book updated successfully');
    } catch (err) {
        console.error('Error updating book:', err);
    }
}

// Delete a book
async function deleteBook(book_id: number): Promise<void> {
    const query = 'DELETE FROM Books WHERE book_id = $1';
    
    try {
        await pool.query(query, [book_id]);
        console.log('Book deleted successfully');
    } catch (err) {
        console.error('Error deleting book:', err);
    }
}

(async () => {
    // Create a new book
    const newBook: Book = {
        book_id: 1,
        title: '1984',
        genre: 'Dystopian',
        isbn: '9780451524935',
        description: 'totalitarian regime',
        author_id: 1,
        price: 15.99,
        publish_date: '1949-06-08',
    };
    await createBook(newBook);

    // Read the book
    const book = await readBook(1);
    console.log('Read book:', book);

    // Update the book
    if (book) {
        book.title = 'Nineteen Eighty-Four';
        await updateBook(book);
    }

    // Delete the book
    await deleteBook(1);

    // Close the pool
    await pool.end();
})();
