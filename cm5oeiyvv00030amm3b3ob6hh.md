---
title: "From Zero to Go Hero: Learn Go Programming with Me - Part 2"
datePublished: Wed Jan 08 2025 21:18:29 GMT+0000 (Coordinated Universal Time)
cuid: cm5oeiyvv00030amm3b3ob6hh
slug: from-zero-to-go-hero-learn-go-programming-with-me-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1736111954991/510adc38-ef21-493e-aa2f-062b4d2fde96.png
tags: programming-blogs, go, programming, development, backend, developer, learning, beginners, rest-api, programming-languages

---

# Introduction

* Hey there! Welcome to Part 2 of the series of Learning Go with me. In Part 1 we set the stage by introducing the project, defining its goals, and setting up the basic folder structure for our Go project.
    
* Now it’s time to dive deeper into some fundamental concepts of Go programming.
    
* In this part, we’ll cover core topics like how Go organizes code using **packages** and **imports,** how **exported names work,** and explore **basic Go constructs** such as types, variables, constants, functions, slices, maps, loops, and conditionals. Then we’ll also understand how **structs** and **pointers** work.
    
* I will try my best to explain each concept in a beginner-friendly way and in a way that I understand because I am also learning with you. I will try to incorporate these concepts in a way that after understanding it we can directly apply it to our CRUD API project.
    
* By the end of this section, you’ll have a strong grasp of these concepts and be ready to use them to bring our API to life.
    
* Let’s jump right in it without wasting any more time
    

---

# Packages

## What is a Package in Go?

* In Go, packages are a way to organize and reuse code. What does that mean?
    
* Think of a Package like a Folder on your computer. Inside that folder, you have related files. Similarly in Go, the files inside a package folder work together to provide some functionality
    
* For example:
    
    * If you are familiar with `math` package in any other language then you must know that it contains tons of mathematical operations. So all these operations are inside this math package
        
* And when you want these functions which are defined somewhere else inside your program, you use **“import“.**
    

## Types of Packages

1. **Standard Library Packages:**
    
    * These are built-in packages in Go. Packages like `math` for mathematical operations, `net/http` for handling HTTP requests, `encoding/json` for working with JSON, etc.
        
2. **Third-Party Packages:**
    
    * These are the additional packages that are created by people in the Go community. If you remember, in Part 1 we installed a few dependencies using `go get` the command. Those belong to this type.
        
3. **Custom Packages:**
    
    * You can create your own packages too which you can use to organize code. We will see this in action soon.
        

## How Packages Work?

* **In Go, every program belongs to a package.** The `main` package is special because it’s where the program starts running. When we define the main package inside a file, Go will know from where it should start the program.
    

## Using Packages in Our Project

* In Part 1 we created different folders and files. If you have noticed, every folder and files are in **red** color which shows that something is wrong. This is because we need to tell which file belongs to which package. Let’s resolve this.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736114848714/e4de1df9-f335-49c4-b211-4b100b3474ee.png align="center")

* Go to each file and write the folder name as a package it belongs to.
    

```go
// cmd/main.go
package main

// config/config.go
package config

// databse/db.go
package database

// internal/books/handler.go, model.go and service.go
package books

// routes/routes.go
package routes

//pkg/logger
package logger
```

* All the errors should be gone after giving the package name inside every file.
    

---

## Imports

* To use any package inside a Go project, we need to import it using `import` a keyword.
    

```go
import "fmt"
```

* If you have multiple packages then list them in parentheses
    

```go
import (
    "fmt"    // for printing.
    "net/http"    // to handle HTTP requests and responses.    
    "encoding/json"    // to parse and generate JSON data
)
```

---

# Exported Names

## What Are Exported Names?

* So in Go, we don’t have keywords like `private` or `public` like other languages.
    
* If the name starts with an **uppercase letter**, then it is considered as exported, meaning it can be accessed from outside the package where they’re defined.
    
* Names starting with a **lowercase letter** are unexpected and private to the package.
    

### Example

```go
type Book struct {    // Exported struct
    Title string    // Exported field
    Author string    // Exported field
}

type car struct {    // Unexported struct
    brand string    // Unexported field
    isElectric bool    // Unexported field
}
```

* Above we created two structs (don’t worry if you don’t know about structs. We will see it in detail in this blog below).
    
* Here `Book` starts with an uppercase letter, meaning we can get this struct in other packages whereas `car` starts with a lowercase letter, meaning we can’t access this struct anywhere else.
    

---

# Basic Go Concepts

## Types and Variables

* Go is a statically typed language. This means every variable must have a type that’s known at compile time. Common types include:
    
    * `int`: Integer values
        
    * `string`: Text data
        
    * `bool`: Boolean values (true/false)
        
    * `float`: Decimal values
        

## Declaring Variables

* There are two ways you can declare a variable:
    

1. **Explicit Declaration**
    

```go
var age int = 24
var name string = "Dhruv"
```

2. **Implicit Declaration**
    

```go
age := 24
name := "Dhruv"
```

* You can also declare with no value like this:
    

```go
var age int    // Defaut: 0
var name string    // Default: ""
```

---

## Constants

* Constants are immutable values, which means we can’t change them once defined.
    
* Use `const` keyword to declare constants
    
* Why Use Constants?
    
    * We use it to prevent accidental changes to critical values.
        
    * To improve the readability and maintainability of code
        

```go
const apiVersion = "v1"
const defaultPort = 8080
```

* You can use parentheses for multiple declarations too
    

```go
const (
    apiVersion = "v1"
    defaultPort = 8080
)
```

---

## Functions

* We use `func` keyword to declare functions in Go.
    

```go
func functionName(){
    // logic
}
```

* You can have parameters inside parentheses
    

```go
func functionName(parameter1 type, parameter2 type){
    // logic
}
```

* You can return from a function by defining a return type like this
    

```go
// Single value return
func functionName() int {
    return 0   
}

// For multiple value return
func functionName() int, string {
    return 0, "Hello"
}
```

---

## Conditionals

* The `if` statement is used for decision-making
    

```go
marks := 85
if marks >= 9- {
    fmt.Println("Grade: A")
} else if marks >= 75 {
    fmt.Println("Grade: B")
} else {
    fmt.Println("Grade: F")
}
```

* Short Statement with `if`. In this, we are first declaring `num` , and right after that we are checking the condition for it.
    

```go
if num := 10; num%2 == 0 {
    fmt.Println("The number is even.")
} else {
    fmt.Println("The number is odd.")
}
```

---

## Loops

* In Go we have only `for loop` for looping. There are different ways you can use `for` loop. Let’s see it in action
    

```go
// Basic `for` loop
for i:= 0; i<5; i++ {
    fmt.Println("Value of i: ,", i)
}

// Infinite Loop
count := 0
for {
    fmt.Println("Looping forever")
    count++
    if count == 3 {
        break // Exists the loop
    }
}

// Condition Only Loop
count:= 0
for count < 3 {
    fmt.Println("Count: ", count)
    count++
}
```

---

# Struct

* If you come from programming languages like Javascript, Dart, or Python, you must be familiar with `class` and `objects`.
    
* In Go we don’t have that. We use `struct` to group data together.
    
* Let’s take an example of our CRUD API project. We need to represent a book with multiple details like a `title`, `id`, `name`, etc.
    
* So instead of creating separate variables for each piece of data, you can use a `struct` to combine all of those into one entity.
    

## Defining a Struct

* To define a structure, you use the `type` keyword followed by the structure name and its field. Each field has a name and a type
    

```go
type Book struct {
    ID string
    Title string
    Author string
    Year int
}
```

## Creating and Using a Struct

* Once we have defined a structure, we can use it to create an object and assign values to its fields
    

```go
var book1 Book    // Creates an instance of `Book` struct
book1.ID = "1"    // Assigns the value "1" to the ID field of struct
book1.Title = "Maths"
book1.Author = "Jane"
book1.Year = 2012
```

## Initializing a Struct in Different Ways

1. Using Field Names
    
    * We can initialize a struct by specifying the field names and their values like below
        
    
    ```go
    book1 := Book{
        ID: "1"
        Title: "Maths"
        Author: "Jane"
        Year: 2012
    }
    ```
    
    * This looks clear, isn’t it?
        
2. Without Field Names
    
    * We can initialize it without field names too like this
        
    
    ```go
    book1 := Book{
         "1"
         "Maths"
         "Jane"
         2012
    }
    ```
    
    * This is less readable because it relies on the order of fields.
        

## Structs with Methods

* A method is a function that is attached to a specific type. This type of method initialization was new and kinda weird for me at first. Because usually we are required to create methods inside a class in other languages right? but here we create it separately and then attach it to the structure using the receiver.
    
* Let me show you how
    

```go
type Book struct {
    ID string
    Title string
    Author string
    Year int
}

func (b Book) SayBookName() {
    fmt.Println("This book name is: ", b.Title)
}

func main() {
    book1 := Book{
        ID: "1"
        Title: "Maths"
        Author: "Jane"
        Year: 2012
    }

    book1.SayBookName() // Call the SayBookName method
}
```

* As you can see to attach this `SayBookName` method to `Book` struct we provided receiver before the method name inside the parenthesis `(b Book)`. So Inside this file wherever any method has this receiver it will automatically get attached to this struct.
    
* You can also nest struct inside a struct like this
    

```go
type Book struct {
    ID string
    Title string
    Author Author // Nested struct
    Year int
}

type Author struct {
    FirstName string
    LastName string
}

func main() {
     book1 := Book{
        ID: "1"
        Title: "Maths"
        Author: Author{
            FirstName: "Jane"
            LastName: "Doe"
        }
        Year: 2012
    }
}
```

---

# Slice

* A **slice** in Go is a data structure used to hold a collection of elements of the same type.
    
* Think of it as a more powerful and flexible version of an array.
    
* While arrays have fixed sizes, slices can grow and shrink dynamically.
    
* It’s really simple to use
    

## Creating Slices

1. **Using the** `make` **function**
    
    * The `make` function creates a slice with a specific length and capacity.
        

```go
slice := make([]int, 3, 5) // Create a slice of type int, of length 3 and capacity 5
```

* Here length represents the number of elements currently in the slice which is 3 here: \[0,0,0\]
    
* And Capacity represents the total space allocated for the slice which is (5). This means this slice can have max 5 elements in it.
    

2. **Using a Slice Literal**
    
    * We can define a slice directly with values using slice literal
        

```go
slice := []int{1,2,3,4,5}
```

## Adding Elements to a Slice

* We can add elements to a any slice using `append` function.
    

```go
slice := []int{1,2,3}
slice = append(slice, 4,5) // adding 4 and 5 to the slice
```

* We need to pass the slice where we want to add elements as the first parameter and then we can pass as many elements as we want after that.
    

## Iterating Over a Slice

* We use `for` loop to access elements in a slice
    

```go
slice := []int[1,2,3,4,5]

for index, value := range slice {
    fmt.Println("Index: ", index, "Value: ",value)
}

for _, value := range slice {
    fmt.Println("Value: ",value)
}
```

### Range

* Here `range` the keyword is used to iterate over elements in a variety of data structures. In the above example, we use `range` to print the index and value in a slice.
    
* We use underscore (`_`) to skip the variable if it’s not needed
    

## Slicing a Slice

* We can create a new slice by slicing an existing one.
    

```go
slice := []int{1,2,3,4,5}
newSlice := slice[1:3] // Slice from index 1 to 2 (3 is exclusive)

// newSlice: [2,3]
```

## Length And Capacity

* Slices have both length and capacity as we saw above. To get the length and capacity of a slice we use `len()` and `cap()` functions
    

```go
slice := []int{1,2,3,4,5}
fmt.Println("Length: ", len(slice)) // 5
fmt.Println("Capacity: ", cap(slice)) // 5
```

## Appending Slices

* We can add a whole new slice to an existing slice using `. . .` (unpack operator)
    
    ```go
    slice := []int{1,2,3,4,5}
    slice2 := []int {6,7,8}
    
    combined := append(slice, slice2...) // [1,2,3,4,5,6,7,8]
    ```
    

---

# Map

* This is another very helpful data structure in Go which is built in inside it. It stores `key` , `value` . This is similar to dictionaries in Python or hash maps in other programming languages.
    
* Keys must be of a comparable type that is `string`, `int` and values can be of any type.
    
* This data structure is useful, especially for lookups when the key uniquely identifies the data. In our case, it is Book ID
    

## Declaring and Initializing a Map

1. **Using** `make`
    

```go
myMap := make(map[string]int)

myMap["Maths"] = 2
myMap["Biology"] = 3
```

* Here **\[string\]** represents `key` and **int** represents `value`
    

2. **Using Map Literal**
    
    * We can initialize and create a map in a single step like we did in struct
        

```go
myMap := map[string]int{
    "Math": 2,
    "Biology": 3,
}
```

## Accessing Values in a Map

* To get the value associated with a key, you have to use the map followed by the key in square brackets
    

```go
myMap := map[string]int{
    "Math": 2,
    "Biology": 3,
}

fmt.Println(myMap["Maths"]) // 2
```

## Checking if a Key Exists

* We use the **comma ok idiom** to check if a key exists or not. This is very useful when we need to check if certain keys exist in a map or not. We can do that in a single line of code
    

```go
myMap := map[string]int{
    "Math": 2,
    "Biology": 3,
}

value, ok := myMap["Physics"]

if exists {
    fmt.Println("Value: ", value)
} else {
    fmt.Println("Key does not exist")
}
```

* `value, exists := myMap["Physics"]`: ok is `true` if the key is present and `false` otherwise.
    

## Adding and Updating Elements

* It’s really easy, you just access the value using the key and add a new value or assign a different value to it
    

```go
myMap := map[string]int{
    "Math": 2,
    "Biology": 3,
}

myMap["Physics"] = 4 // Adding new element

myMap["Math"] = 1 // Updating exisitng element
```

## Deleting Elements

* We use `delete()` function to remove a key-value pair from the map
    

```go
myMap := map[string]int{
    "Math": 2,
    "Biology": 3,
}

delete(myMap, "Math") // Remove the key "Math"
```

## Iterating Over a Map

* We use again `for` loop with `range` to iterate over all key-value pairs.
    

```go
myMap := map[string]int{
    "Math": 2,
    "Biology": 3,
}

for key, value:= range myMap {
    fmt.Println("Key: ", key, "Value: ", value)
}
```

---

# Wrapping Up

* I think that’s pretty much all you need to know for now. We learned lots of fundamental stuff in this article. I tried to make it as concise as possible in order to quickly grasp the underlying concepts because going into too much detail with all the theory doesn’t make sense at this point.
    
* There is still one concept remaining which is **Pointers.** I wanted to cover it in this blog only but then thought it would become quite a big read so I will be explaining it in detail in the next blog.
    
* I hope after this article you are at least comfortable with the basic stuff and syntaxes. Just practice the syntax that you find difficult to grasp. It will all make sense and your hands will then flow naturally on the keyboard afterwards.
    
* See you in the next one, until then…
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711803084752/aa266313-a315-41a8-9538-8ff4370577fb.gif?auto=format,compress&gif-q=60&format=webm align="center")

* Connect with me on [**Twitter**](https://twitter.com/dhruv_nakum), [**LinkedIn**](https://www.linkedin.com/in/dhruv-nakum-4b1054176/), and [**Github**](https://github.com/red-star25)