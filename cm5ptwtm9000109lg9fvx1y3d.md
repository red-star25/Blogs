---
title: "From Zero to Go Hero: Learn Go Programming with Me - Part 3"
datePublished: Thu Jan 09 2025 21:16:56 GMT+0000 (Coordinated Universal Time)
cuid: cm5ptwtm9000109lg9fvx1y3d
slug: from-zero-to-go-hero-learn-go-programming-with-me-part-3
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1736195375027/69c04f72-f889-4f38-b4e4-6ffce98a879c.png
tags: programming-blogs, go, programming, development, backend, developer, learning, beginners, rest-api, programming-languages

---

# Introduction

* Welcome to Part 3 of the Learning Go with Me series. I hope you like it so far and learned from it. Because that’s the most important thing. If you have any doubts or comments please feel free to comment it. I will try to help you out.
    
* In the last article, we learned lots of fundamental concepts of Go. And in this blog, I decided to just focus on the Pointers.
    
* Let’s start without further ado
    

---

# What is a Pointer?

* A pointer is nothing but a variable that stores the “**memory address”** of another variable. What does that mean?
    
* So instead of holding a direct value which we typically do like `age := 24`, the pointer holds the address of where that value is stored in memory.
    
* You can think of pointers as post office boxes.
    

![Mail boxes filled of leaflets and letters. Shallow DOF,Mailboxes and Lock in Rows at Entrance.](https://t4.ftcdn.net/jpg/01/78/09/19/240_F_178091901_TN6QoOQnM7HJ1iMAkyS7effr1zoaJK5c.jpg align="center")

* Each box points to a certain address/ house number. Similarly, if you have defined a variable like this:
    

```go
num := 42
```

* Then you can point to this variable using another variable with a pointer
    

```go
ptr := &num
```

* You need to first understand what ‘ **\* ‘ and ‘ & ’** lexical elements mean.
    

1. **Address Operator (&):**
    
    * The & operator is used to get the memory address of a variable. If `x` is an integer variable then `&x` will give you pointers to `x` that is, a memory address where the integer `x` is stored.
        
2. **Dereferencing Operator ( \* ):**
    
    * The \* operator is used to get the value stored at a memory address. If `p` is a pointer to an integer, then `*p` will give you the integer that `p` points to.
        

**Example:**

```go
func main(){
    num := 42
    ptr:= &num
    
    fmt.Println(ptr) // 0xc000104040 - Address where num is stored
    fmt.Println(*ptr) // 43 - Value at which ptr is pointing
}
```

* In this example, `ptr` is a pointer to `num`. You can get the value of `num` by dereferencing `ptr` with `*ptr`.
    

---

# Passing Pointer to Functions

* Pointers also come into play when you're dealing with functions.
    
* If you pass a variable to a function in Go, the function gets a copy of the variable. **Everything in go is a pass-by value**, if the function changes the variable, it won't affect the original. But if you pass a pointer to a variable, the function can dereference the pointer to change the original variable.
    
* Let’s take an example
    

```go
// Without Pointer - Pass by Value
func valueSemantic(num int){
    num = 43
}

func main(){
    num := 42
    
    fmt.Println("Before: ", num) // 42

    valueSemantic(num)

    fmt.Println("After: ", num) // 42
}
```

* This is because a copy of num is getting passed to the function `valueSemantic` and not the actual value. To update the value that we are passing from other functions we have to use a pointer.
    

```go
// With pointer - Pass by Value
func valueSemantic(num *int){
    *num = 43
}

func main(){
    num := 42
    
    fmt.Println("Before: ", num) // 42

    valueSemantic(&num)

    fmt.Println("After: ", num) // 43
}
```

* As you can see now it got changed. Why?
    
* Because now we are not passing just the copy of the `num` but we are passing it an address where `num` is stored.
    
* And in the function parameter now that we are passing an address to it we need to accept that address using a pointer. Because remember? The pointer points to another variable’s address.
    
* Inside the function, we can’t just do this and change the variable:
    

```go
num = 43
```

* Because `num` is a pointer. So first we need to get the value of that pointer by dereferencing it like this `*num` and then assign a new value to it.
    

```go
*num = 43
```

---

# Pointers with Structs

* Lastly, pointers are crucial when dealing with structs in Go. Since Go doesn’t have classes
    
    and objects, you can use structs to create complex types, and you can use pointers to structs to modify these structs or to avoid copying the structs around.
    
* Let’s take an example:
    

```go
type Person struct {
    name string
    age  int
}

func updateName(p *Person, newName string) {
    p.name = newName // Modify the struct via pointer
}

func main() {
    p := Person{name: "Alice", age: 30}

    fmt.Println("Before:", p.name) // Prints: Alice
    updateName(&p, "Bob")
    fmt.Println("After:", p.name) // Prints: Bob
}
```

* We aren’t doing anything new in this. We created a struct of type Person. It has `name` and `age` fields.
    
* And inside `main` function we are passing the address of this person `p` in `updateName` function.
    
* `updateName` takes two parameters. Pointer to a struct person and new name.
    
* But inside the function, you see we didn’t use `*` to deference it. Why?
    
* This is because Go is automatically dereferencing that struct for us. So when you have a pointer to a struct in Go, the language provides a convenience called **automatic dereferencing** for accessing fields or calling methods. You don't need to explicitly dereference the pointer using `*` before accessing fields or methods.
    

> **For Primitive Types (e.g., int, float, etc.):** You must use `*` to dereference the pointer and access the value.
> 
> **For Structs:** Go **automatically dereferences pointers to structs** when you access their fields or call methods.

---

* In my previous blog, I forgot two concepts to discuss which are `defer` and `switch case` statements. Let’s understand them one by one
    

---

# defer

* In Go, the `defer` the keyword is used to ensure that a function call is executed later in a program’s execution, usually for the purposes of cleanup.
    
* `defer` is often used where `ensure` and `finally` would be used in other languages.
    
* When a function call is deferred, it's placed onto a stack. The function calls on the stack are executed when the surrounding function returns, not when the `defer` the statement is called.
    
* They're executed in Last In, First Out (LIFO) order, so if you have multiple `defer` statements, the most recently deferred function will be the first one to execute when the function returns.
    

```go
func main() {
    fmt.Println("Start")
    
    defer fmt.Println("This will print last")
    
    fmt.Println("End")
}
```

**Output:**

```go
Start
End
This will print last
```

## Multiple `defer` Statements

```go
func main() {
    defer fmt.Println("First")
    defer fmt.Println("Second")
    defer fmt.Println("Third")
}
```

**Output**

```go
Third
Second
First

// LIFO order as explained above
```

## Real-World Example: Closing a File

```go
func main() {
    file, err := os.Open("example.txt") // Opening a file
    if err != nil {
        fmt.Println("Error opening file:", err)
        return
    }
    defer file.Close() // Ensure the file is closed before exiting the function

    // Perform file operations here...
    fmt.Println("File opened successfully")
}
```

* In real-world programming, we have many things open. We need to make sure we close those types of functions because otherwise, it will create memory leakage. Although Go has a Garbage collector that will dump those things down if not used, but it’s always a good practice to close the instance of it once the work is done.
    
* And that’s where `defer` can be used. We use defer right after we perform operations like opening a file to make sure we don’t forget.
    

---

# Switch

* `switch` in Go is a powerful way to control the flow of execution by matching a value against multiple cases. It is simpler and cleaner than writing multiple `if-else` conditions.
    

## How `switch` works

* `switch` evaluates a value and executes the first matching `case`.
    
* If no `case` matches, the `default` block if executed.
    

## Example

```go
func main() {
    day := "Monday"

    switch day {
    case "Monday":
        fmt.Println("Start of the workweek!")
    case "Friday":
        fmt.Println("Almost the weekend!")
    default:
        fmt.Println("Just another day.")
    }
}
```

* In the above example, the `switch` matches `day` to `Monday` and executes the corresponding block
    
* In Go we can use Switch without an Expression. So If we omit the expression, Go evaluates the first `case` that is `true`
    

```go
func main() {
    x := 15

    switch {
    case x < 10:
        fmt.Println("Less than 10")
    case x < 20:
        fmt.Println("Between 10 and 20") // Prints this
    default:
        fmt.Println("20 or more")
    }
}
```

## Fallthrough in `switch`

* The `fallthrough` keyword forces the execution of the next case, even if the condition is not `true`
    

```go
func main() {
    num := 2

    switch num {
    case 1:
        fmt.Println("One")
    case 2:
        fmt.Println("Two")
        fallthrough
    case 3:
        fmt.Println("Three")
    default:
        fmt.Println("Other")
    }
}

/* 
Output: 
Two 
Three
*/
```

---

# Wrapping Up

* In this article, we explored some of the fundamental concepts of Go, including pointers, defer statements, and switch statements.
    
* We learned that pointers store the memory address of variables, enabling functions to modify original data without creating copies.
    
* The `defer` statement schedules function calls to execute after the surrounding function completes.
    
* The `switch` statement offers a good control flow based on variable values.
    
* I think this is pretty much it for you to know to get started. So from the next article, we will start building out Book CRUD API. There are still a few things remaining to explain and I will be explaining on the go as it will make much more sense when we are building something.
    
* I hope you have learned something from this article. If you have any feedback or queries, feel free to ask them in the comments. I’ll be happy to answer all your questions
    
* See you in the next article, until then….
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711803084752/aa266313-a315-41a8-9538-8ff4370577fb.gif?auto=format,compress&gif-q=60&format=webm align="center")

* Connect with me on [**Twitter**, **Linke**](https://twitter.com/dhruv_nakum)[**dIn**, and **Gi**](https://www.linkedin.com/in/dhruv-nakum-4b1054176/)[**thub**.](https://github.com/red-star25)