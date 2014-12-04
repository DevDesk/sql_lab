#SQL Lab


##Getting Started

To get started we'll need to import the booktown.sql file.

1. open terminal
2. use the command `psql -f booktown.sql`
3. type `sql` to open your psql console
4. type \list to ensure the booktown database was successfully completed

##Instructions
Provide the follow sql statements below each question.

##Order
1. Find all subjects sorted by subject
##### SELECT subject FROM subjects; 
2. Find all subjects sorted by location
##### SELECT subject,location FROM subjects ORDER BY location ASC; 

##Where
1. Find the book "Little Women"
##### SELECT title FROM books WHERE title = 'Little Women';
2. Find all books containing the word "Python"
##### SELECT title FROM books WHERE title ILIKE '%Python%';
3. Find all subjects with the location "Main St" sort them by subject
##### SELECT subject,location FROM subjects WHERE location ILIKE '%Main St%' ORDER BY subject;

##Joins
(should show 16 for 1st bullet)

1. Find all books about Computers list ONLY book title
##### SELECT books.title 
##### FROM books JOIN subjects 
##### ON books.subject_id = subjects.id;

* Find all books and display ONLY
	* Book title
	* Author's first name
	* Author's last name
	* Book subject

##### SELECT books.title, authors.first_name, authors.last_name, subjects.subject 
##### FROM books 
##### JOIN subjects 
#####     ON books.subject_id = subjects.id 
##### JOIN authors 
#####     ON books.author_id = authors.id

* Find all books that are listed in the stock table
	* Sort them by retail price (most expensive first)
	* Display ONLY: title and price
##### SELECT books.title, stock.retail
##### FROM editions 
##### JOIN books ON editions.book_id = books.id
##### JOIN stock ON editions.isbn = stock.isbn
##### ORDER BY stock.retail DESC

* Find the book "Dune" and display ONLY
	* Book title
	* ISBN number
	* Publisher name
	* Retail price
	
##### SELECT books.title, stock.isbn, publishers.name, stock.retail
##### FROM books 
##### JOIN editions ON editions.book_id = books.id
##### JOIN stock ON editions.isbn = stock.isbn
##### JOIN publishers ON publishers.id = editions.publisher_id
##### WHERE books.title = 'Dune'

* Find all shipments sorted by ship date display ONLY:
	* Customer first name
	* Customer last name
	* ship date
	* book title

##### SELECT shipments.ship_date, customers.first_name, customers.last_name, books.title
##### FROM shipments 
##### JOIN customers ON shipments.customer_id = customers.id
##### JOIN editions ON shipments.isbn = editions.isbn
##### JOIN books ON editions.book_id = books.id
##### ORDER BY shipments.ship_date

* Find all books that have either a 2nd or 3rd edition associated to it display ONLY:
	* Book title
	* Book Author
	* Edition Number
	
##### SELECT editions.edition, books.title, authors.first_name, authors.last_name
##### FROM editions
##### JOIN books ON editions.book_id = books.id
##### JOIN authors ON books.author_id = authors.id
##### WHERE editions.edition = 2 OR editions.edition = 3
