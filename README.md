## Create tables

``` sql
CREATE TABLE IF NOT EXISTS Author (
id SERIAL PRIMARY KEY,
name VARCHAR(100),
nationality VARCHAR(50),
birth_year INT,
death_year INT
);


CREATE TABLE IF NOT EXISTS Books (
id SERIAL PRIMARY KEY,
title VARCHAR(100) NOT NULL,
authorId INT REFERENCES Author(id),
genres TEXT[],
published_year INT
);

CREATE TABLE Patrons (
id SERIAL PRIMARY KEY,
name VARCHAR(100) NOT NULL,
email VARCHAR(100) NOT NULL,
borrowed_books INT[]                
);

```

## Inserting Data
``` sql
INSERT INTO Author (id, name, nationality, birth_year, death_year) VALUES

('George Orwell', 'British', 1903, 1950),
('Harper Lee', 'American', 1926, 2016),
('F. Scott Fitzgerald', 'American', 1896, 1940),
('Aldous Huxley', 'British', 1894, 1963),
('J.D. Salinger', 'American', 1919, 2010),
('Herman Melville', 'American', 1819, 1891),
('Jane Austen', 'British', 1775, 1817),
('Leo Tolstoy', 'Russian', 1828, 1910),
('Fyodor Dostoevsky', 'Russian', 1821, 1881),
('J.R.R. Tolkien', 'British', 1892, 1973);


//ALTER TABLE Books ADD COLUMN available BOOLEAN;

INSERT INTO Books (id, title, authorId, genres, published_year, available) VALUES

('1984', 1, ARRAY['Dystopian', 'Political Fiction'], 1949, TRUE),
('To Kill a Mockingbird', 2, ARRAY['Southern Gothic', 'Bildungsroman'], 1960, TRUE),
('The Great Gatsby', 3, ARRAY['Tragedy'], 1925, TRUE),
('Brave New World', 4, ARRAY['Dystopian', 'Science Fiction'], 1932, TRUE),
('The Catcher in the Rye', 5, ARRAY['Realist Novel', 'Bildungsroman'], 1951, TRUE),
('Moby-Dick', 6, ARRAY['Adventure Fiction'], 1851, TRUE),
('Pride and Prejudice', 7, ARRAY['Romantic Novel'], 1813, TRUE),
('War and Peace', 8, ARRAY['Historical Novel'], 1869, TRUE),
('Crime and Punishment', 9, ARRAY['Philosophical Novel'], 1866, TRUE),
('The Hobbit', 10, ARRAY['Fantasy'], 1937, TRUE);

INSERT INTO Patrons (id,name, email, borrowed_books) VALUES

(1, 'Alice Johnson', 'alice@example.com', ARRAY[]::INT[]),
(2, 'Bob Smith', 'bob@example.com', ARRAY[1, 2]),
(3, 'Carol White', 'carol@example.com', ARRAY[]::INT[]),
(4, 'David Brown', 'david@example.com', ARRAY[3]),
(5, 'Eve Davis', 'eve@example.com', ARRAY[]::INT[]),
(6, 'Frank Moore', 'frank@example.com', ARRAY[4, 5]),
(7, 'Grace Miller', 'grace@example.com', ARRAY[]::INT[]),
(8, 'Hank Wilson', 'hank@example.com', ARRAY[6]),
(9, 'Ivy Taylor', 'ivy@example.com', ARRAY[]::INT[]),
(10, 'Jack Anderson', 'jack@example.com', ARRAY[7, 8]);

```
## Get all Books
``` sql
SELECT * FROM BOOKS;

SELECT * FROM BOOKS
 WHERE title = 'Brave New World';

 SELECT * FROM Books 
WHERE authorId = 2;

SELECT * FROM Books 
WHERE available = true;


UPDATE Books
SET available = false
WHERE title = 'To Kill a Mockingbird';

UPDATE Books
SET genres[2] = 'Historical Novel'
WHERE id = 7;

 UPDATE Books
 SET genres = genres || ARRAY['horror']
WHERE id = 3;

UPDATE Books
SET genres = array_prepend('action', genres)
WHERE id = 7;


UPDATE Patrons
SET borrowed_books = array_append(borrowed_books, 8)
WHERE id = 3;

UPDATE Patrons
SET[1] = 3
WHERE id = 1;
```

``` bash
UPDATE Patrons
SET[1] = 3
WHERE id = 1;
```
