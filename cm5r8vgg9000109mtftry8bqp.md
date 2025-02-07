---
title: "From Zero to Go Hero: Learn Go Programming with Me - Part 4"
datePublished: Fri Jan 10 2025 21:03:33 GMT+0000 (Coordinated Universal Time)
cuid: cm5r8vgg9000109mtftry8bqp
slug: from-zero-to-go-hero-learn-go-programming-with-me-part-4
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1736228159917/fee94889-26b2-4966-80bb-cbdc14d95be9.png
tags: programming-blogs, go, programming, development, backend, developer, learning, beginners, rest-api, programming-languages

---

# Introduction

* Heyy Gophers!!! Welcome to the Part 4 of Learning Go with Me. Thanks for coming alone to till here. I hope you are learning and enjoying this series.
    
* Till now we almost covered the fundamentals of Go and now we are ready to write out the first API.
    
* It’s gonna be exciting as we will learn a lot of new things which will help you in your first programming career
    
* Let’s get started without wasting any more time.
    

---

* We already have the project structure ready for us
    

```plaintext
crud-api/
│
├── cmd/
│   └── main/
│       └── main.go           # Entry point for the application
│
├── config/
│   └── config.go             # Environment variable management
│
├── internal/
│   ├── routes/
│   │   └── routes.go         # API routes definition
│   ├── books/
│   │   ├── handler.go        # HTTP handlers for book operations
│   │   ├── model.go          # Book database model and queries
│   │   └── service.go        # Business logic for books
│   ├── database/
│   │   └── db.go             # Database connection logic
│
├── .env                      # Environment variables
├── go.mod                    # Go module dependencies
└── .gitignore                # Ignored files
```

* Also we have dependencies installed in our project from Part 1 of this series
    

```go
go get github.com/go-chi/chi/v5
go get github.com/go-sql-driver/mysql
go get github.com/joho/godotenvfg
```

* And lastly, we have the environment file ready for us
    

```go
// .env
PORT=8080
DB_USER=root
DB_PASSWORD=password
DB_HOST=127.0.0.1:3306
DB_NAME=crud_api
```

* Now let’s go step by step. As we already have the .env file ready for us, why not create a function to load it inside our project?
    
* Before that let’s see the main.go file
    

```go
// main.go

package main

func main() {
	// TODO: Load .env file

	// TODO: Setup database connection

	// TODO: Setup router

	// TODO: Run server
}
```

* These are our TODOs which we need to complete
    

---

# Loading `.env` Variables

* To load values inside our `.go` files we are using `godotenv` package. This package helps us get environmental values inside our file.
    
* We implement this function inside `config.go` file. So head over to `config.go` and let’s write `LoadEnv` function. But before that let’s import a few packages
    

```go
// config/config.go

package config

import (
	"log"
	"os"

	"github.com/joho/godotenv"
)
```

* We are using `log`, `os` and `godotenv` packages here.
    

---

## `fmt` and `log` Packages

* In Go we mostly use these two packages to print out values and logs in the terminal. At first, these two may look similar but they both serve different purposes.
    
* `log` is specifically designed for logging messages. This means we can get more information like time stamping and error reporting with this. So we mostly use it during application runtime like debugging, informational logs, and error logs.
    
    * It includes functions like `log.Fatal`(Exists the program after logging) and `log.Panic` (Logs and then panic)
        
* Whereas `fmt` is used for general-purpose printing text. It is commonly used for printing in a console with formatted strings. So we use it mostly when we are printing user-facing messages.
    

### Example

```go
fmt.Println("Hello World") // Hello World
fmt.Printf("Hello %s", "World") // Hello World

log.Fatalf("This is a fatal error.") // This is a fatal error. (After this program stops)
log.Panic("This is a panic error.") // This is a panic error. (After this program stops)
```

* More on `fmt` visit: [https://pkg.go.dev/fmt](https://pkg.go.dev/fmt)
    
* More on `log` visit: [https://pkg.go.dev/log](https://pkg.go.dev/log)
    

---

## `os` Package

* The `os` package in Go is used for tasks related to the operating system. For example accessing the files, and environment variable.
    
* In our example, we are focused on accessing the .env file and it has `Getenv()` a function that receives the values of environment variables named by `key`
    

---

* Now let’s write `LoadEnv()` function
    

```go
import (...)

func LoadEnv() {
	err := godotenv.Load("../.env")
	if err != nil {
		log.Fatal("Error loading .env file")
	}
}
```

* We get `Load()` function inside `godotenv` package. `Load` will read the `.env` file and load them into ENV for this process. Notice that you pass the path of your .env file.
    
* This function returns an error so we are collecting it inside `err` variable and then checking if the `err` has anything. If the `err` is not `nil` which means something went wrong. If so, we need to show the error message and exit the program. Because if the env file is not loaded then there is no point in starting the program.
    
* Now to get a specific value from the env file we need to make one function that will get us the value of the asked key from the env file
    

```go
package config

import (...)

func LoadEnv() {
	...
}

func GetEnv(key, fallback string) string {
	if value, ok := os.LookupEnv(key); ok {
		return value
	}
	return fallback
}
```

* We created the `GetEnv` function, which takes `key` and `fallback` strings as parameters and returns a string.
    
* The `key` is the string for which we need the value in our code. For example, inside our `.env` file, we have different values. If we need only `DB_USER`, we pass this key to the function, and it returns the related value.
    
* We also accept a fallback string, so if the requested value isn’t found, we use the default fallback value.
    
* Here, we are using the `os` package, which includes the `LookupEnv` function. This function takes a `key` as an argument and returns two things: a `string` and a `bool`. If the value is found, `ok` will be true; otherwise, it will be false. By checking `ok`, we can determine if a value was returned and decide whether to return the fallback value.
    
* Let’s check if it is working or not
    

```go
package main

import (
	"fmt"

	"github.com/red-star25/crud-api/config"
)

func main() {
	config.LoadEnv()
	fmt.Println(config.GetEnvValue("DB_USER", "root"))

   	// TODO: Setup database connection

	// TODO: Setup router

	// TODO: Run server
}
```

**Output:**

```go
root
```

* That’s awesome. Let’s now set out the Database Connection
    

---

# Setting Up the Database Connection

## Importing Packages

* As you know we are using MySQL for storing our application’s data. We need to first set up the connection and create an instance of the SQL DB.
    
* Head over to `db.go` file and let’s first import all the required packages
    

```go
package database

import (
	"database/sql"
	"fmt"
	"log"
	"os"

	_ "github.com/go-sql-driver/mysql"
)
```

* We have seen the usage of `fmt`, `log` and `os`. Let’s see what are the remaining ones.
    
* `database/sql`: This is a built-in library for SQL database interactions.
    
* `_ "`[`github.com/go-sql-driver/mysql`](http://github.com/go-sql-driver/mysql)`"`: Imports the MySQL driver as a side effect to register it with `database/sql`. Here `_` (underscore) represent that this import is used as a side effect. Which means this package is not directly used.
    

## Creating Database

```go
var DB *sql.DB
```

* Here type DB is a pointer to `sql.DB` an object. We are making it globally accessible so that anyone can reuse it without creating it again and again on each query
    
* You must be wondering Why it is a type of pointer.
    
    * So, If `DB` were a simple variable (not a pointer), any changes made to it inside a function, wouldn't affect the global variable itself. Instead, Go would create a copy of the value, and the global `DB` would remain unchanged.
        
    * By using a pointer, it updates the global `DB` directly. This makes the database connection immediately available to all parts of the application.
        

## Connect function

* Now let’s create a function `Connect` that will be responsible for opening the database connection and making a connection.
    

```go
func Connect() {
	dsn := fmt.Sprintf("%s:%s@tcp(%s)/%s",
		config.GetEnvValue("DB_USER", "root"),
		config.GetEnvValue("DB_PASSWORD", ""),
		config.GetEnvValue("DB_HOST", "localhost"),
		config.GetEnvValue("DB_NAME", "crud_api"),
	)
}
```

* Here we have created a variable `dsn`(Data Source Name) which is a type of string. So before we connect to MySQL we need to have a URL to which we want to connect.
    
* So here we have used a formatted string from `fmt` package. Here function `Sprintf` returns a formatted string without printing it to the console. `%s` is a placeholder for `string` values here.
    
* And we are getting all the values from our `.env` file using config’s `GetEnvValue` function.
    
* Example `dsn`
    

```plaintext
username:password@tcp(localhost)/mydatabase
```

## Opening Connection

* Now that our data source URL is ready, we are ready to open our SQL connection.
    
* To do that `mysql` provides `Open()` function which takes
    
    * `driverName` (which is nothing but a database name, ex: MySQL, MongoDB, Postgres, etc). You can provide any driver here and open the connection and
        
    * `dataSourceName` is a URL of the database that we just created above.
        

```go
var err error
DB, err = sql.Open("mysql", dsn)
if err != nil {
    log.Fatalf("Error connecting to database: %v", err)
}
```

* This function returns two things: `db` object and `err`.
    
* So what we are doing here is, we are assigning the returned SQL db object to our globally defined **DB**.
    
* And then we check if there is any error occurred or not.
    

> You will see this type of error handling thoughtout any Go project. This is a convention in Go. It might seems little overdoing but it is a good practice that we are handling error just after calling function.
> 
> Also note that there is no `try` `catch` or `finally` keywords in Go. You can read why they are using this type of error handling in this article : [https://go.dev/doc/faq#exceptions](https://go.dev/doc/faq#exceptions)

## Verifying the DB Connection

* To verify whether the connection is successful or not we have `Ping` function that verifies if the database connection is still alive, and it also establishes the connection if necessary.
    

```go
if err := DB.Ping(); err != nil {
	log.Fatalf("Error verifying database connection: %v", err)
}
```

* That’s pretty much it. We can log the message after this that the Database is connected successfully.
    

## Final `db.go` code

```go
package database

import (
	"database/sql"
	"fmt"
	"log"

	_ "github.com/go-sql-driver/mysql"
	"github.com/red-star25/crud-api/config"
)

var DB *sql.DB

func Connect() {
	dsn := fmt.Sprintf("%s:%s@tcp(%s)/%s",
		config.GetEnvValue("DB_USER", "root"),
		config.GetEnvValue("DB_PASSWORD", ""),
		config.GetEnvValue("DB_HOST", "localhost"),
		config.GetEnvValue("DB_NAME", "crud_api"),
	)

	var err error
	DB, err = sql.Open("mysql", dsn)
	if err != nil {
		log.Fatalf("Error connecting to database: %v", err)
	}

	if err := DB.Ping(); err != nil {
		log.Fatalf("Error verifying database connection: %v", err)
	}

	log.Println("Database connected successfully!")

}
```

* And now call this `Connect` function inside `main.go`
    

```go
package main

import (
	"github.com/red-star25/crud-api/config"
	"github.com/red-star25/crud-api/database"
)

func main() {
	config.LoadEnv()

	database.Connect()

	// TODO: Setup router

	// TODO: Run server

}
```

* If everything goes right then you will see this message after you run the program.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736390331806/d9bc489e-a75f-4469-952b-122406a2af13.png align="center")
    
    > Make sure you have MySQL up and running on your computer.
    

---

# Creating `Book` model

* We are creating CRUD API for managing Books. So in order to view data in a structured manner with all the required fields we need to create a Book model using `struct`
    

> In Go, the term **"model"** refers to a structured representation of data used within an application, typically to map data between a program and an external data source, such as a database or an API. Models are often implemented as `structs` in Go, which are a way to define and organize related data fields.

* Let’s create our Book model
    

```go
// internal/books/model.go
package books

type Book struct {
	ID     int
	Title  string
	Author string
	Year   int
}
```

* Here we have four fields inside our Book struct. `ID`, `Title`, `Author`, `Year`.
    
* That’s easy, right? Yes. But there is one more thing which we need to do. So as we know that when we deal with APIs, we use JSON to serialize and deserialize the data that we are getting from the user and data we are sending to the user.
    
* And generally, they are represented in lowercase like `id`, `name`, `author`, `year` like that. But if you see our Book struct we have the first letter capital for each field. And that is intentional. Because we need those struct’s fields outside to use. And to make it globally accessible we capitalize the first letter of any variable.
    
* So to resolve this issue, we use what we call in go “ **struct tags “**. In other programming languages, we refer to this as “ **annotations** “.
    
* This helps us convert these struct fields to proper naming conventions. Let’s see how we do that
    

```go
package books

type Book struct {
	ID     int    `json:"id"`
	Title  string `json:"title"`
	Author string `json:"author"`
	Year   int    `json:"year"`
}
```

* So what we do is after giving the type of the struct field we use backticks \` \`. And in there we write json: and then whatever name we want.
    

---

# Implement Database Queries (CRUD)

* Now that our database is up and running let’s write database queries for **C**reate, **R**ead, **U**pdate, and **D**elete.
    
* First of all, let’s import two required packages
    

```go
package books

import (
	"crud-api/internal/database"
	"errors"
)
```

* We are importing a database for accessing the **DB** object. Using this we can perform all the queries.
    
* And `errors` we use for handling errors.
    

## The `GetAllBooks` Function

* Firstly we are creating a function to get all the books from the database
    

```go
func GetAllBooks() ([]Book, error) {
    rows, err := database.DB.Query("SELECT * FROM books")
    if err != nil {
        return nil, err
    }
    defer rows.Close()
    
    ...
}
```

* Here we created a function called `GetAllBooks` which is responsible for getting all the books from the database.
    
* It returns two values:
    
    * **\[ \]Book:** A slice of struct Book.
        
    * **error:** Go’s error object.
        
* Inside the function body, we are making a query to the SQL database using the DB variable’s `Query` function. It takes a string where we write a raw SQL query.
    
* In this function, we need all the books with data. And to do that we wrote this query **“SELECT \* FROM books“.** Which will get all the books from the database.
    
* And then we checked if it threw any errors
    
* After that, we defer call the rows.Close() to close it once this function is finished.
    

---

* This `rows` object allows us to iterate over the results we get from the Query. And to iterate over the results we have `rows.Next()` function which goes over all the results.
    
* We can take advantage of this function and create a for loop inside which we can fill all the data inside a slice of the book
    

```go
func GetAllBooks() ([]Book, error) {    
    ...
    var books []Book
    for rows.Next() {
        var book Book
        if err := rows.Scan(&book.ID, &book.Title, &book.Author, &book.Year); err != nil {
            return nil, err
        }
        books = append(books, book)
    }
    return books, nil
}
```

* Here we have created a temporary slice of the book variable. In this, we will fill in all the data.
    
* Then we looped through `rows.Next()` which will go over all the rows and inside the for the body we are getting all mapping the data in a row to the Book struct using `rows.Scan`
    
* And after that, we are appending that book to the `books` slice
    
* And once every row is scanned we return it from the function.
    

> NOTE: Make sure you have the book table in MySQL database: If you don’t have one then create it and then run the project, otherwise it will throw an error
> 
> You can run this query inside your MySQL Workbench
> 
> ```sql
> CREATE TABLE books (
>     id INT AUTO_INCREMENT PRIMARY KEY,
>     title VARCHAR(255) NOT NULL,
>     author VARCHAR(255) NOT NULL,
>     year INT NOT NULL
> );
> ```

* Let’s test `GetAllBooks`.
    

```go
// main.go

func main() {
	config.LoadEnv()

	database.Connect()

	data, err := books.GetAllBooks()
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println("Books:",data)
	// TODO: Setup router

	// TODO: Run server

}
```

**Output:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736402535605/d8d513dd-ea92-4969-b88d-14a69dd7b53a.png align="center")

* It ran!!!!
    

![a man in a suit and black turtleneck is giving a yes sign](https://media.tenor.com/jfufeww3U04AAAAM/jeff-blim-starkid.gif align="center")

---

* This is great! Now let’s create a Handler function for this function. Because we need to send this data to the user too, right? Till now we just got the data from the database.
    
* To do that head over to `handler.go` file
    

---

# Setting up HTTP Handlers

* Let’s first import the required packages
    

```go
// handler.go

import (
	"encoding/json"
	"net/http"
)
```

* Here `encoding/json` is used. This is used for converting JSON data into Go structures and Go data structures into JSON.
    
* `net/http` is used for handling HTTP requests.
    
* I’ll first show all the code to you and then we will understand what it does
    

```go
package books

import (
	"encoding/json"
	"net/http"
)

func GetAllBooksHandler(w http.ResponseWriter, r *http.Request) {
	books, err := GetAllBooks()
	if err != nil {
		http.Error(w, "Failed to fetch books", http.StatusInternalServerError)
		return
	}

	w.Header().Set("Content-Type", "application/json")
	json.NewEncoder(w).Encode(books)
}
```

* `func GetAllBooksHandler(w http.ResponseWriter, r *http.Request) {`
    
    * Here we have two parameters:
        
        * `w http.ResponseWriter`: This is used for sending data back to the client.
            
        * `r *http.Request`: This is used for getting data from the client.
            

## Fetching the Books

* `books, err := GetAllBooks()`
    
    * Here, the function `GetAllBooks` is called to retrieve a list of books. As we saw, that function will get the data from the database and return all the books with an err object.
        

## Error Handling

```go
if err != nil {
	http.Error(w, "Failed to fetch books", http.StatusInternalServerError)
	return
}
```

* If that function returns any error, we check it inside this if block and send back the HTTP error of `InternalServerError`.
    
* And then exiting the function with `return`
    
* Here, The `http.Error` function simplifies sending error responses. This has all the different types of errors you can throw according to your functionalities.
    

## Setting the Response Header

```go
w.Header().Set("Content-Type", "application/json")
```

* This line sets the `Content-Type` header of the response to `application/json`. It informs the client that the response body contains JSON data.
    

## Encoding and Sending the Response

```go
json.NewEncoder(w).Encode(books)
```

* Now we need to encode the slice of a book in JSON format for the client. To do data we use json Encoder method.
    
* This sent the data as the HTTP response. And it ensures compatibility with clients expecting data in JSON format.
    

---

# Configuring Routes

* Now, how these handlers are going to trigger? Of course when the user hits a certain URL, or to be specific an Endpoint from their end.
    
* And so we want to return data for that particular endpoint/route right? For that, we need to create a route called `/book`.
    
* And to create routes we are using the **Chi package**.
    
* Go to `routes.go` and paste the below code
    

```go
package routes

import (
	"crud-api/internal/books"

	"github.com/go-chi/chi/v5"
)

func SetupRouter() *chi.Mux {
	r := chi.NewRouter()

	r.Get("/books", books.GetAllBooksHandler)

	return r
}
```

* Here the SetupRouter function will configure all the routes.
    
* First, we need to create an instance of chi router. This router will handle the incoming HTTP requests and route them to the appropriate handlers.
    
* `r := chi.NewRouter()` - This line does that
    
* And now using this variable `r` we can create a map of the routes to the handlers.
    

```go
r.Get("/books", books.GetAllBooksHandler)
```

* For different HTTP request, we have different HTTP Methods in `r`. POST, UPDATE, DELETE,etc
    
* Here we need GET as we are getting the data from the database. Inside `r.Get()`, first, we need to give the route as `/books`. This means once this endpoint is hit by the client, the handler defined in the second parameter will be triggered.
    
* And at the end, we are returning the pointer to the chi.Mux because we need it for the server in the `main.go`. You will see why below.
    

---

# Finalizing the `main.go` file

* Now that we have everything set up we can start the server and listen to the endpoints.
    

```go
package main

import (
	"log"
	"net/http"

	"github.com/red-star25/crud-api/config"
	"github.com/red-star25/crud-api/database"
	"github.com/red-star25/crud-api/internal/routes"
)

func main() {
	config.LoadEnv()
	database.Connect()

	router := routes.SetupRouter()
	port := config.GetEnvValue("PORT", "8080")
	log.Printf("Server running on port %s", port)
	log.Fatal(http.ListenAndServe(":"+port, router))
}
```

* Inside the main function, we are loading the environment variables.
    
* Then we connect to the database.
    
* And then we call SetupRouter to configure all the routes.
    
* To run the server we have `ListenAndServe` function inside `http` package. Inside we have to first pass the address and then the router that we set up. And we also have to check for any errors. So we are wrapping this function inside `log.Fatal`
    

---

# Running The Server

* Now let’s cross our fingers and check if everything is working. To check the functionality of our program. We are using the Postman application.
    
* So open it up and run it
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736405665069/0aeaacae-70a0-400d-abec-0600f04fdd56.png align="center")

![a baby is sitting in a crowd with a woman holding him and screaming yes .](https://media1.tenor.com/m/J8GV21cQO3QAAAAd/bb-baby.gif align="center")

* You will see an empty slice because we have not added any data yet. We will be implementing other HTTP methods in the next article.
    

---

# Wrapping Up

* If you came this far to the end of this article, then congratulations for making it.
    
* In the next article, we will be implementing the remaining CRUD operations which are Update, Delete, and Create. It will be fun because now we have the base setup for us, so now we just need to work on the functionalities.
    
* Hope you learned something from this article. There are lots of blogs coming in the future with more amazing topics and projects and I am so excited to write about all of it.
    
* See you in the next blog, until then….
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711803084752/aa266313-a315-41a8-9538-8ff4370577fb.gif?auto=format,compress&gif-q=60&format=webm&auto=format,compress&gif-q=60&format=webm align="center")

* Connect with me on [**Twitter**](https://twitter.com/dhruv_nakum), [**LinkedIn**](https://www.linkedin.com/in/dhruv-nakum-4b1054176/), and [**Github**](https://github.com/red-star25)