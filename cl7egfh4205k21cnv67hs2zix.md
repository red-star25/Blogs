---
title: "Object Oriented Programming in Dart: Abstraction"
datePublished: Mon Aug 29 2022 07:44:04 GMT+0000 (Coordinated Universal Time)
cuid: cl7egfh4205k21cnv67hs2zix
slug: object-oriented-programming-in-dart-abstraction
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1661681512203/53BTNuzGA.png
tags: programming-blogs, dart, flutter, beginners, object-oriented-programming

---

## In The Previous Article....

- Welcome to the 2nd article on the OOPs in the Dart series. In the first article, we learned about some basic terms and concepts of OOPs.
- We learned about **Classes** and **Object**, and then we went through the concept of **Constructors** and different types of it.
- In this article, we will learn about **ABSTRACTION**.
- Let's get started 🔥

--------
## What is Abstraction 🤷🏻‍♂️?
- I do not want to throw you a definition of Abstraction just like any other article. Let's take two examples, and I can assure you, that you will never forget Abstraction in your life again. 

### Example 1:
- Let's take an example of **Vehicle**. Now take a **Car** and a **Bus**. 
- Answer the Question: What's Car and a Bus?
 - Answer is: Both are the type of **Vehicle**. Right ✅
- Now can you drive a Car or a Bus? Of course 😒.
- Ok last one: Can you drive a Vehicle 🤔? No. Why? Because Vehicle is not a real thing or object, it is just an **Abstract** thing/concept.
- Let's say, You are writing a program and you wanted to create a Bus or Car object. Now think about it, All vehicle has some basic common features and functionalities, For example, Wheels, Steering, Brakes, Engine, Doors, etc.
- So, writing all these properties again and again inside all the vehicle types becomes repetitive a task. In that case, we can model a Vehicle class so that we can supply all these common properties there. And whenever we create any new Vehicle we can automatically get access to all these properties by just extending the Vehicle class.
- Here modeling a Vehicle means, you basically avoid writing similar code again and again in the Car and Bus. 
- So this way, we can **take away** / ** abstract out** some common functionalities. And that's basically an Abstraction.
- **Abstraction** is based on a metaphor of 
<center>*“taking something away from its original context”.*</center>
- The implementation of the Vehicle and Car classes is shown below. 

```dart
abstract class Vehicle {
  int? doors;
  int? wheels;

  void hornSound();
}

class Car extends Vehicle {
  @override
  int? doors = 2;

  @override
  int? wheels = 4;

  @override
  void hornSound() {
    print('Beeeeeep');
  }
}

class Bus extends Vehicle {
  @override
  int? doors = 2;

  @override
  int? wheels = 4;

  @override
  void hornSound() {
    print('Hooooonkk');
  }
}
```


### Example 2:
- In this example, let's take an example of a real-world object **Pen**. Considering the pen as an object, the question is what is being abstracted here or hidden here?

- If you want to know this, you have to consider different types of pens. Let's take a ballpoint pen and a fountain pen. Now, we need to answer 2 questions:
 - What are the similarities in behavior?
 - What are the differences in similar behaviors?

- In the case of our example, the similar behavior will be both of the pens will **write**. So, writing is a behavior, which both of them do.
- And now, for the second question - what are the differences in common behavior ?, Well let's say the ball-point uses a rotating ball to ink flow, others use an ink channel for that. The rate of ink flow was different for each of them etc. etc. 
- Now, you are giving either one of the pens to a person - he’s gonna **write ** with that without considering the parameters of ball nib or high rate of ink. **So, writing is important, & the way how writing is achieved is not. **
- So normally in a pen **the process of writing** is abstracted. Below is the code implementation :

```dart
abstract class Pen {
  int? rateOfInkFlow;

  void write();
  }
}
```

- So to be more precise, the process of finding the abstraction involves
 - Find the various possible forms of the object. In our case, there are at least 10 types of pen 
 - Find the most generalized form of the object. The generalization of a ball-point, fountain, etc. is **Pen**.
 - Find if there are similar behaviors and differences in the similar behaviors. If you could find one, then that is to be abstracted / that is the abstraction.


![ReliefPhewGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1661607588330/ItwXcY8PG.gif align="center")
- I hope, you understood the underlying concept of abstraction. Now let's understand what are the Abstract Classes and Methods.

-------

## Abstract Class and Abstract Methods
- To create an Abstract class in Dart, we use **abstract** keyword. 

```dart
abstract class Pen {}
```
- A class created using the **abstract** keyword can have abstract and non-abstract methods (method with the body). Now, what are abstract methods?
- Abstract methods are methods that don't have any implementation. They are just sitting there, waiting for some other classes to implement them.
- In our Pen example, the function `write` here is known as an **abstract method**. It's because it has not been implemented yet.

```dart
abstract class Pen {
  int? rateOfInkFlow;

  void write();
}
```
- Now that we know, what Abstraction is, let's see some points which is required to understand when we are dealing with Abstraction.
## Rules of Abstraction

### 1. Abstract classes can't be instantiated.
- The first rule is you cannot Instantiate the abstract class. For example, you cannot do like this :

```dart
void main() {
  final pen = Pen(); // Error: Abstract classes can't be instantiated.
}
```

- Why? Because as I said, abstract classes are just concepts or an idea. 
- Remember the first example? *You can drive Car but not a Vehicle.*

```dart
abstract class Vehicle{//...}

class Car extends Vehicle {//...}

void main (){
   final vehicle= Vehicle() // ❌
   final car = Car() // ✅
}
```

### 2. All abstract methods of the parent class must be implemented in the subclass
- In our Pen example, we've one abstract method called `write()`. 
- Now when you extend the BallPoint class (SubClass) with the Pen class (Abstract Class) you must implement all of the **abstract methods** which is defined in the Pen class (Abstract Class). Otherwise, you will get an error as shown below

![errorabstact.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661608997049/bp3VNl5RN.png align="left")


### 3. An abstract class can have a method with implementation.
- This is an interesting one. Let's try to implement `write()` method.

```dart
abstract class Pen {
  int? rateOfInkFlow;

  void write() {
    print('Writing...');
  }
}

class BallPoint extends Pen {}

void main() {
  final ballPoint = BallPoint();
  ballPoint.write();
}
```

- You will not get any errors. The code will compile without any errors.

```dart
Output : Writing...
```

- But, keep this in mind that, when you are adding some code to an abstract method, you are effectively making that method non-abstract. So, Now the **abstract** doesn't have any importance anymore.
- In short: Methods with No Logic mean Abstraction and methods with Logic mean no Abstraction.

- Consider the below code.

```dart
abstract class Pen {
  int? rateOfInkFlow;

  void write() {
    print('Writing...');
  }
}

class BallPoint extends Pen {
  @override
  void write() {
    // TODO: implement write
  }
}

void main() {
  final ballPoint = BallPoint();
  ballPoint.write();
}
```
- Try to analyze, what should be the output 🤔. Well, nothing will be printed on the console. 🤷🏻‍♂️
- It's because, you have **override** the write() function inside a BallPoint class, and when you override this function you will not get the implementation of the superclass.
- The implementation of the write of Pen is ignoring a call to Pen. 
- What if there is some important logic inside the Pen's `write()` method and we need it inside the BallPoint class? That's where **super()** comes into the picture.

 - **super()** : It is basically a reference to the super class. In our case it is **Pen**. You can call any method or access any variable of the super class using this. 
 - 
```dart
class BallPoint extends Pen {
    @override
    void write() {
      super.write();
      print('Writing with BallPoint');
    }
}
```
- And now if you run the code, you will see first of all the super class log and then the subclasss' log. It's because you called `super.write()` before in the BallPoint's write() method.

### 4. Abstract classes can have Constructor
- Yoo hold on, We already saw in rule #1 that Abstract classes cannot be instantiated, then how can it have a Constructor, and what is the use of it if we cannot instantiate it? Right?
- Well, the thing here is, the abstract classes cannot be **directly **instantiated as we do for a normal class. We cannot do like below :

```dart
abstract class Pen { //.... }

void main() {
  final pen = Pen();
}
```
- **BUT**, you can call an abstract class's constructor using the subclass. In our case, You can call a Constructor of Pen class inside the BallPoint class.
![WhatThePointWentOverYourHeadGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1661617928188/ATvgY7M85.gif align="center")
- Okay fine, lemme give you an example.
- Consider the below code :

```dart
abstract class Pen {
  int rateOfInkFlow;
  
  Pen({
    required this.rateOfInkFlow,
  });

  void write();
}
```
- Here I've created a constructor and supplied the `rateOfInkFlow` variable. As soon as you do this the IDE will warn you as shown below :

![errorabstact2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661618186387/zetQR9ubS.png align="left")

- What the above code means after creating this constructor is, that now it requires subclasses to pass this rateOfInkFlow value to the Pen class.
- We can resolve the above error, by passing the value to the super()

```dart
class BallPoint extends Pen {
  BallPoint() : super(rateOfInkFlow: 1);
  @override
  void write() {
    print('Writing with BallPoint');
  }
}
```

## Implicit Interfaces
- If you are familiar with Java, there is a concept of Interfaces. 
- But, Dart does not have a syntax for declaring interfaces. Class declarations are themselves interfaces in Dart.
<center>**Classes should use the *implements *keyword to be able to use an interface.**</center>
- Example: 

```dart
class A {
   void run() {
     print('Running');
  }
}

class B implements A{
  @override
  void run() {
    // TODO: implement run
  }
}
```
- Here B class implements the A interface, so **it has to implement** all methods of A.
- When you use the **implement** keyword, you **must** implement all the properties and methods of the superclass.

---------

## When to use Abstract Class
- When you have a requirement where your **base class** should provide a default implementation of certain methods whereas other methods should be open to being overridden by child classes use abstract classes.
- The purpose of an abstract class is to provide a common definition of a base class that multiple derived classes can share.
- In short, Use an Abstract Class :
 - When creating a class that will be widely distributed or reused.
 - To define a common base class.
 - To provide default behavior.

---------

## Wrapping Up
- **I hope you enjoyed and learned something from this article. If you have any feedback/queries, leave them in the comments.**

- **Thank you for spending time reading this article. See you in the next article. Until then....**


![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1661681009039/JeP48w9qQ.gif align="left")

-------

- **Connect with me on [Twitter](https://twitter.com/dhruv_nakum), [LinkedIn](https://www.linkedin.com/in/dhruv-nakum-4b1054176/), and [Github](https://github.com/red-star25).**
