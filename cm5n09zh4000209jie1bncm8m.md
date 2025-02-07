---
title: "From Zero to Go Hero: Learn Go Programming with Me - Part 1"
datePublished: Tue Jan 07 2025 21:51:49 GMT+0000 (Coordinated Universal Time)
cuid: cm5n09zh4000209jie1bncm8m
slug: from-zero-to-go-hero-learn-go-programming-with-me-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1736061078296/caa153bc-3448-4397-bae5-629bbc6468a0.png
tags: programming-blogs, go, programming, development, backend, learning, beginners, rest-api

---

# Introduction

* Hello, everyone. It’s been a while since I last published anything on my blog. A lot has happened during this time, including leaving my full-time job and moving to the United States for my master's degree.
    
* So, as my full-time job was more focused on the front-end side. I always wanted to learn a backend programming language. I researched what’s going on in the software industry. And I found GO programming language which is in the trend in recent years. From what I have felt so far by learning a few things in GO till now I absolutely agree with this trend.
    
* There are many things that makes Golang a good choice for companies to use as their backend language. And so I started learning it and as you might be knowing if are my reader that I share what I learn. Because I like to learn in public and share everything that I am learning. So here I am with a series on Learning GO.
    
* I personally like to learn by building something. So, you and me both will be learning and building a backend system together in this series. I am so excited and looking forward to this series. I hope you get something from this. So without further a do, let’s get started.
    

---

## Why GO?

* Go, also known as Golang is a programming language by Google. The creators of the Go programming language are Robert Griesemer, Rob Pike, and Ken Thompson.
    

![Understand Go in 5 minutes - Je suis un dev](https://i.imgur.com/Dg8PHQF.png align="center")

* What I like about Go is, it is very fast and it’s really easy to pick up if you know any other programming languages. It is designed to be simple, efficient, and highly scalable which makes it an excellent choice for building web servers, APIs, and large-scale systems.
    
* I am listing down few points for you to understand why Go has become so popular among developers in recent years.
    
    * **Ease of Learning:**
        
        * It’s easy to learn as its syntax is clean and beginner friendly. It is syntactically similar to C language but it also has memory safety, garbage collection, structural typing and concurrency.
            
    * **Performance:**
        
        * As I mentioned, it is really fast, it compiles the code in seconds. This makes it perfect for web applications.
            
    * **Concurrency Built in:**
        
        * Go has powerful tools for handling multiple tasks simultaneously (more about concurrency in future blogs).
            
    * **Wide Adoption**
        
        * Companies like Google, Uber, Dropbox and many big tech giants are using Go as their primary backend language which gives programmers a sense of trust that this is something on which they can make a career and earn money.
            
* I personally think that learning Go might seem a little tricky due to its syntax. But once you pick up and know syntax it’s easy to code. There are a few things that might surprise you because Go doesn’t have few things that other programming languages have. We will see it in upcoming blogs.
    

---

## What is a CRUD API?

* If you are fresher and don’t know about CRUD then this section is for you. So CRUD basically stands for **Create, Read, Update and Delete.** These are you can say the base of any backend system. These operations allow users to interact with a database.
    
* For example, you use Instagram. There are certain things you do like, Creating new Posts (**Create**), Reading Messages (**Read**), Update your profile (**Update**), Delete your past posts (**Delete**).
    
* You see, all these are CRUD operations in action. In this series we will learn how to create these operations. We will be applying all these operations in our books example. I picked this project because this is perfect for beginners like you and me as it is straightforward yet comprehensive enough to cover key programming concepts.
    

---

## What Will You Learn?

* In this series of blogs, We will learn basics and some advance stuff of Go while building a RESTful API. And by the end of this project, you’ll have practical knowledge of:
    
    * **Structs** and **slices** to organize and manipulate data.
        
    * How to use **http** package to setup a web server.
        
    * How to manage **router.**
        
    * Encoding and decoding **JSON** to handle API requests and responses.
        
    * Writing clean, reusable, and maintainable Go code
        
    * We will also be learning advance concepts like **contexts, go routines, channels, etc.**
        
    * and so on…
        

---

## Why Hands-On Projects Work Best

* I personally think that a person cannot learn a programming language by just reading or watching videos online. It’s not just about memorizing rules and syntax of it. It’s more about building something real. And that’s why In my blog also I try to use some real world example to make it simple to understand.
    
* This type of learning reinforces concepts which one can immediately apply on what you’ve learned to see how it works
    
* Also by building something while learning gives a sense of confidence that “Yes, I can do this!“
    
* And last but not least, you can add this to your resume because that is what an employer look for in a candidate which is Practical skills.
    

---

So roll up your sleeves, fire up your favorite code editor, and let’s get started. Because this isn’t just about learning Go- It’s about empowering yourself to build things. Let’s make coding fun, practical, and rewarding.

![Golang Quickstart with Homebrew (MacOS) | by Devesu | Medium](https://miro.medium.com/v2/resize:fit:1400/1*Ifpd_HtDiK9u6h68SZgNuA.png align="left")

---

# Prerequisites

* So before we go ahead there are few things which you need to make sure you have setup on your side. Don’t worry if you are new to Go. We will go step by step. So here’s what you’ll need to get started:
    

1. **Basic Knowledge:**
    
    * To follow along with this series you don’t need to be an expert programmer. However, a basic understanding of concepts like variables, functions, and loops will be helpful. So if you are completely new to coding, you might want to spend a little time learning these fundamentals first.
        
2. **Install Go on Your Machine:**
    
    * As it is not that complicated to install Go in your machine. I would like you to install by your own.
        
    * You have to just visit the [official Go download page](https://go.dev/doc/install). And grab the installer for your OS (Windows, Mac or Linux)
        
    * Then run the installer and follow the instructions. Once installed, Go should be added to your system’s PATH.
        
    * You can verify the installation by opening the terminal or command prompt and type:
        
    * ```bash
              go version
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736059226413/7b2a588b-5feb-40b7-9f51-43759c32fb85.png align="left")
        
    * If you see a message like go version go1.xx.x, you are good to go!
        
3. **Set Up a Code Editor**
    

* While there are many options available online for code editor, I personally recommend VS Code for its simplicity and its excellent Go support. If you don’t have it already.
    
    1. Download and Install [VS Code](https://code.visualstudio.com/download).
        
    2. Install this Go extension.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736047757052/72edb3b1-424e-4f5b-898a-9a9911ec719b.png align="center")

---

# Project Overview

* Now that we are setup up, let’s see what are we gonna building. So the goal of this project is to create a simple RESTful API using Go while learning Go concepts.
    
* This API will allow users to manage collection of books by performing CRUD operations: **Create**, **Read**, **Update** and **Delete**.
    

## What is a RESTful API?

* If you are completely new to this terms REST, then this section is for you. Basically a RESTful API is a way for different softwares to communicate over the web. REST stands for (Representational State Transfer). It is a design principle that make sure that APIs are simple, scalable and easy to use.
    
* In our case, we will be building an API that uses HTTP methods like:
    
    * **GET** to retrieve data.
        
    * **POST** to create new data.
        
    * **PUT** to update existing data.
        
    * **DELETE** to remove data.
        

---

## Project Features

* Our API will manage list of books. So we will be having these properties in books:
    
    * **ID -** a unique identifier for each book.
        
    * **Title -** the name of the book.
        
    * **Author -** the person who wrote the book.
        
    * **Year -** the year the book was published.
        

Here’s is a sneak peak at what our API will do:

1. **Add a New Book:** Accept data from the user and add book to the list.
    
2. **View All Books:** Return a list of all books.
    
3. **Update a Book:** Modify the details of an existing book.
    
4. **Delete a Book:** Remove a book from the list based on its ID.
    

---

# Setting Up Your Go Project

* Now we are ready to dive into coding. The first step is to setup your Go project.
    
* We need to setup a proper project structure for our Go application. Following an industry standard folder structure ensures that our code is clean, modular and easy to maintain as the project grows. Here is how to do it step by step.
    

---

## Create the Project Directory

1. Open your terminal and navigate to the folder where you want to store your project.
    
2. Create new directory for the project:
    

```bash
mkdir crud-api
cd crud-api
```

3. Initialize a new **Go module**:
    

```bash
go mod init github.com/red-star25/crud-api
```

---

## Go Modules

* If you are familiar with Javascript, Node, Flutter, then you might be knowing the file called `package.json` or `pubspec.yaml`
    
* This file is responsible for maintaining the dependencies/packages. Whether it is built-in in the language or third-party, all the dependencies with their versions are mentioned in this file.
    
* This dependency management system is introduces in **Go 1.11** and made the default in **Go 1.13**.
    
* So what this above `go mod init` command will do is it will create `go.mod` file in the root directory of your project.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736049300881/5943c14c-ea07-47e3-9f1b-eb0af482ad7c.png align="center")

* This file specifies few things:
    
    1. The **module’s name**, typically repository URL or a path that identifies the codebase.
        
    2. **Dependencies** required by the project and their versions.
        
    3. The **Go language version** used.
        

> You might have noticed that we are using GitHub repository URL for module. It is because Git repo ensures that no conflicts is there when fetching dependencies.
> 
> Another reason is because of versioning. Repo often follow semantic versioning using Git tags (ex., v1.0.0) which Go modules use to resolve the correct dependency version.

## Installing dependencies

* In this project we will be using `MySql` as our database and also `Chi` package for managing routing. We will also be using `godotenv` for environmental configuration. Don’t worry if you don’t have any idea about it just install these packages for now and we will see what it does and how it works in upcoming blogs.
    
* So to install packages in our go project we have `go get <package-name>` command.
    

```bash
go get -u github.com/go-chi/chi/v5
go get -u github.com/go-sql-driver/mysql
go get -u github.com/joho/godotenv
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736055754658/2c021e09-9526-4a26-b9d7-686f66c335f5.png align="center")

---

## Folder Structure

* Go encourages simplicity, but for larger applications, it is good practice to follow a clear folder structure.
    
* There are many tools available like: [Go Project Layout](https://github.com/golang-standards/project-layout) and [Go Blueprint](https://github.com/Melkeydev/go-blueprint). Which helps you to create a base project for your Go application.
    
* So let’s create folder structure for our project.
    

```bash
crud-api/
│
├── cmd/
│   └── main/
│       └── main.go            # Main entry point for the application
│
├── config/
│   └── config.go              # Environment and configuration management
│
├── internal/
│   ├── routes/
│   │   └── routes.go          # Centralized route definitions
│   ├── books/                 # Business logic for managing books
│   │   ├── handler.go         # HTTP handlers for book operations
│   │   ├── model.go           # Book data structure and database queries
│   │   └── service.go         # Business logic for books
│   ├── database/              # Database utilities
│   │   └── db.go              # Database connection logic
│
├── pkg/                       # Shared utility packages
│   └── logger/                # Logging utilities
│       └── logger.go
│
├── .env                       # Environment variables
├── go.mod                     # Go module dependencies
└── go.sum                     # Dependency checksums
|__ .gitignore
```

* Let’s understand this structure first before we go ahead.
    

### Top Level Files

* **.env**
    
    * This contains environment specific configuration variables (e.g., database credentials, API keys).
        
* **go.mod**
    
    * We already know what it is now
        
* **go.sum**
    
    * Contains the checksum of dependencies to ensure integrity and consistency across builds.
        
* **.gitignore**
    
    * Files to ignore in Git commit
        

> To add .gitignore file for Go, I recommend using `gitignore` VS code extension by **CodeZombie. It will pull up Go specific .gitignore file for you**
> 
> After installing, press Cmd + Shift + P or Ctrl + Shift + P and type **Add gitignore. It will ask for languages, so search for Go and hit Enter.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736055980678/6e4b05b6-88d1-46dd-afef-f67459e8089c.png align="center")

* Final Top Level Structure will look like this.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736056009266/3b98c23f-2e06-4d67-aa0e-674efdbed263.png align="center")

### Folder and File Structure

* `cmd/main.go`:
    
    * So in go you must define an entry point for the program to start. And to define it we create `main.go` file inside `cmd` folder
        
    * `main.go` have main function inside which initializes the application. We setup routes, server and handle the configuration of the project here in this function.
        
* `config/config.go`:
    
    * In this file we load all the environment variables which is defined in `.env` .
        
    * Remember we installed `godotenv` package? This package help us reading these values. There are many other packages which does the same. I will leave it for you to search it.
        
    * So basically it defines `structs` which will hold configuration data for example, database credentials, server ports, etc. (more on `structs` later)
        
* `internal/`
    
    * This folder holds the core business logic and internal code.
        
    * Code written inside this will not be exposed as part of the public API.
        
    
    1. `routes/routes.go`
        
        * In this we register all our routes for API like `/books`, `/authors` which will be mapped to it’s respective handlers/functions. Again don’t worry if you don’t understand any of these term, we will be seeing it in action soon for better understanding. Just get the basic understanding for now.
            
    2. `books/`
        
        * This folder handles all the business logic related to the “Books“ resource.
            
        * `handler.go`:
            
            * In this we define HTTP handlers for CRUD operations.
                
            * Ex: `CreateBook`, `GetBooks`, `UpdateBook`, `DeleteBook`
                
            * Basically we have the logic of our CRUD operations for book in this file for handling HTTP requests and responses.
                
        * `model.go`:
            
            * In this we have `Book` structure with fields like `ID`, `Title`, `Author`.
                
            * Also we implement database queries here like `FindAllBooks`, `SaveBook` etc.
                
        * `service.go`:
            
            * This contains all the business rules and logic for books and it will act as a Bridge between the handler and model like validating data.
                
    3. `database/db.go`:
        
        * As the name suggests it has the logic for handling database connection and utilities.
            
        * In this we initialize database connection.
            
    4. `pkg/`:
        
        * This folder contains code which is shared across different parts of the application or even other projects.
            
        * `logger/logger.go`:
            
            * This file implements logging logic using packages like `logrus` or `zap`
                
            * It may include support for logging levels like `INFO`, `DEBUG`, `ERROR`.
                

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736057409526/968512c8-f521-4505-a0a3-552e8bb3487a.png align="center")

### How It All Fits Together

* Let’s understand how all these files are connected to each other.
    
    * `cmd/main/main.go` Loads configuration from `config/`
        
    * It connects to database via `internal/database/`
        
    * Sets up routes using `internal/routes/`
        
    * And finally starts the server.
        
* `internal/books` handles CRUD operations for book and `pkg/logger` provides a way to log information or errors from anywhere in the project.
    
* `.env` is loaded to proved sensitive or environment specific configurations
    

> This organization ensure clean separation of concerns, making the codebase scalable, maintainable and testable.

* I know I spent a lot of time explaining folder structure but it’s a one time investment. Almost every go project will have similar kind of structure, so in future if you encounter this you will have an idea of what each part is used for.
    

---

## Configure Environment Variables

* Go to `.env` file in the root directory and let’s add configuration values:
    

```plaintext
DB_USER=root
DB_PASSWORD=crudAPI@1234
DB_HOST=127.0.0.1:3306
DB_NAME=crud_api
PORT=8080
```

* As we will be using MySQL database we need to configure variables like username, password and host value. So we mention everything inside `.env` file as we don’t want to expose these sensitive values publicly.
    

---

# Wrapping Up

* I will end this blog here. We learned many things about Go:
    
    * Why Go?
        
    * What is CRUD operations?
        
    * What is RESTful APIs?
        
    * Go Modules
        
    * How to install packages in Go?
        
    * Folder Structure of Go project
        
    * Environmental variables file.
        
* Before we dive into coding. We first need to understand few concepts of Go. Which I will be explaining in the next blog.
    
* I hope you like the blog and learned something from it. If you have any questions or suggestions please leave them in the comment section. I would love to answer and discuss them.
    
* See you in the next article. Until then….
    

![Peace Out GIFs | Tenor](https://media.tenor.com/H9y5_3rPqkAAAAAM/peace-out-im-out.gif align="center")

* Connect with me on [**Twitter**](https://twitter.com/dhruv_nakum), [**LinkedIn**](https://www.linkedin.com/in/dhruv-nakum-4b1054176/), and [**Github**](https://github.com/red-star25).