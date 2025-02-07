---
title: "Master The Art of Dependency Injection"
seoTitle: "What is Dependency Injection | Dependency Injection in Flutter"
seoDescription: "What is Dependency Injection? Why Dependency Injection? How to Inject Dependencies? How to achieve Dependency Injection In Flutter?"
datePublished: Sat Aug 21 2021 05:16:17 GMT+0000 (Coordinated Universal Time)
cuid: ckslbwotk0jt02xs1davt61ma
slug: master-the-art-of-dependency-injection
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1629521726733/xniEG3DYJ.png
tags: programming-blogs, programming, dart, flutter, dependency-injection

---

## Introduction
- Dependency injection is one of the most useful design patterns that allow developers to write loosely coupled code. It also helps to keep our code testable. 
- Dependency injection is a concept that keeps popping up in the tech world. However, it is also a concept people usually don’t fully understand. 
- It can be hard to understand what it means or how it works across different frameworks. 
- In this guide, I will break down dependency injection and talk you through some common implementations using Dart and Flutter.
- **Buckle Up **......
![UpThumbsUpGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629351350236/4cMTDzeiY.gif)

----------------------------------------

## What is Dependency Injection ??
- First of all, let's understand what **Dependency** and **Dependent** Is. 
- When some class **A** needs class **B** to perform its operation then class **A** is called **Dependent** and class **B** is called **Dependency**
- 
![Dependency and Dependent.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629352993854/LnRqzZ2Rp.png)
- Simple explanation of DI (Dependency Injection) by John Munsch for 5 years olds :
> When you go and get things out of the refrigerator for yourself, you can cause problems. You might leave the door open, you might get something Mommy or Daddy don't want you to have. You might even be looking for something we don't even have or which has expired.
> What you should be doing is stating a need, "I need something to drink with lunch," and then we will make sure you have something when you sit down to eat.
- It means you don't have to go anywhere. You will get what you want.
- **In Technical Term: **
> DI is a design pattern in which a class requests dependencies from** external sources** rather than **creating** them. It means the dependent objects are injected or supplied to your class. The class doesn't have to do any initialization by itself. It will get what it wants by the injector.

----------------------------------------

## Why we need Dependency Injection
- DI helps you to make your code **loose coupled ** rather than **tightly coupled**.
- **Loose coupling**: When an object gets the object to be used from external sources, we call it loose coupling. In other words, loose coupling means that the objects are independent.
- **Tight coupling**: When a group of classes are highly dependent on one another then it is called tight coupling.
- By using DI pattern we can make the code more **readable**, **reusable**, and **testable**.
- Let's see one example with and without **DI**.
- ### **Without DI**
- Let's make a Car class that has **Engine** as a **dependency**. It means **Car** is now dependent on **Engine**.
- 
```
// Car.dart
import 'package:blog/Engine.dart';
```
- 
```
class Car {
       Engine _engine = Engine();
       void start() {
         _engine.start();
       }
}
```
- **Engine** class has one `start` method. Which simply prints a message.
```
// Engine.dart
class Engine {
       void start() {
         print("Engine Started");
       }
}
```
- Now creating a **Car** object and starting its engine.
```
// main.dart
import 'package:blog/Car.dart';
```
```
void main() {
       Car car = Car();
       car.start();
}
```
- Here our class **Car** is **tightly coupled**. It means the class **Car** is highly dependent on dependency **Engine**.
- Now imagine the **Car** manufacturer wants to change their normal **Engine** to **ElectricEngine**. They should be able to do it right?
- But if we look at the class **Car** there is no way to change the **Engine**. 
- We have hardcoded the **Engine** in the **Car** class.
- We can solve this problem by using the **Dependency Injection** pattern. Dependency Injection is a technique that facilitates **loosely coupled** object-oriented software systems.
- There are different ways to achieve dependency injection in programming :
- **Constructor Injection**
- **Property Injection (aka setter injection)**
- **Method Injection**

- ### With DI (Constructor Injection)
- We can solve the above issue by passing the **Engine** object as a parameter of the **Car** constructor.
- 
```
// Car.dart
import 'package:blog/Engine.dart';
```
- Passing Engine object as a parameter
```
// Car.dart
class Car {
  Engine? _engine;

  Car(Engine engine) {
    this._engine = engine;
  }

  void start() {
    _engine!.start();
     }
}
```
- 
```
// main.dart
import 'package:blog/Car.dart';
import 'package:blog/Engine.dart';
```
- Creating Engine Object and passing it to the **Car**'s `constructor`.
```
// main.dart
void main() {
  Engine normalEngine = Engine();
  Car car = Car(normalEngine);
  car.start();
}
```
- Now if we want to pass a different implementation of **Engine** for example **ElectricEngine**, we can simply create the class **ElectricEngine** which is an implementation of **Engine** class and pass it to the **Car** `constructor`.
- 
```
class ElectricEngine implements Engine {
  @override
  void start() {
    print("Electric Engine Started");
  }
}
```
- 
```
// main.dart
void main() {
     // Engine normalEngine = Engine();
     Engine eletricEngine = ElectricEngine();
     Car car = Car(eletricEngine);
     car.start();
}
```
- As we can see we are **injecting** the **dependency** from outside the implementation of the class.
- That's It !! This is called **Dependency Injection**. It's easy, right? But constructor injection will also become an overhead when the application is large. That's why many languages provide their own libraries and frameworks to implement DI in a large project.
- DI is very useful in **Unit Testing **. 
- It's because dependencies are injected from outside of the class. That's why our class is not any more dependent on other dependencies. And we can easily test our class in isolation.

------------------------------------------
- This is the overall explanation of **What is DI** and **Why DI**.
- Now we are going to see how we can implement **Dependency Injection** in our **Flutter Application**.

----------------------------------------------

## Dependency Injection in Flutter
- In **Flutter** we can implement **Dependency Injection** in different ways :
- Using **Constructor**,
- Using **InheritedWidget**,
- Using Packages like **get_it**, **provider** etc.
- Let's apply **Dependency Injection** by using these three approaches.
### Constructor as Dependency Injection
- Consider the below code where we have 4 Pages :
- 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629393028577/FZ9haCTrB.png)
- Now assume that the **Page 4** requires the same **Car** object that is declared in the **Page 1**.
- To give **Page 4** that object, we have to manually pass that object of the **Car** to all the way down to the **Page 4**, like below
- 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629393830640/yRb8RWhQP.png)
- As you can see it's not the best way to pass any object like this.
- It is because even if the **Page 2** and **Page 3** don't require the **Car** object, they still have to declare it inside their class. And that is not efficient.

### `InheritedWidget` as Dependency Injection
- To solve the above issue Flutter Provides an **InheritedWidget**. 
- It helps us to access any objects, methods, variables, etc which is defined in the `InheritedWidget` in the widget tree.
- Example:
- Here I've simply created an **InheritedWidget**.
- 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629394562489/gGHeyMG4a.png)
- Now wrap the **MaterialApp** inside the **InheritedDI**
- 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629394842007/hEa1VOSIC.png)
- Now we can access all the variables, methods, and objects, etc that are available inside the **InheritedDI** from anywhere inside the widget tree.
- Let's see how we can access that car object inside **Page 4** directly :
- 
![main.dart.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629395942959/q16E_tiNB.png)
- That's pretty neat, right? Now we can access the **Car** object inside any page without any prop drilling.
- But there is one problem. See the below code :
- 
```
InheritedDI.of(context)!.getCar
```
- InheritedWidget needs `context` to access the object.
- We can't inject this dependency inside the class which doesn't have `context`.
- So that's a problem now. What if we want to access `dependencies` inside the classes like DB, Client, etc? There we won't have `context`, because they're just simple regular classes.

### `get_it` as Dependency Injection 
- To solve the above issue we can use `get_it` package. `get_it` is a `Service Locator`. 
The purpose of the Service Locator pattern is to return the service instances on demand.
-  > If you are not familiar with the concept of Service Locators, it's a way to decouple the interface (abstract base class) from a concrete implementation, and at the same time allows to access the concrete implementation from everywhere in your App over the interface.
- **Note**: There are some differences between **Dependency Injection** and **Service Locator**. [Check this answer for more detail](https://softwareengineering.stackexchange.com/questions/390755/whats-the-difference-between-using-dependency-injection-with-a-container-and-us).
- Let's see how to use `get_it` as Dependency Injection.
- First of all, install the `get_it` package inside `pubspec.yaml`
- 
```
get_it: ^7.2.0
```
- Now create `serviceLocator.dart` file. In this file first, create **instance** of **GetIt**.
- At your start-up you register all the objects you want to access later like this:
- 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629397520940/haTlYCP3l.png)
- After that call the `setup()` method before the app initialization i.e inside `main()` method
- 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629397492514/Cwgw6pG86.png)
- And now use it like this :
- 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629397593219/xFc8MS1s2.png)
- As we can see that `get_it` makes **dependency injection ** very easy for us.
- Because now we can access this dependency inside any type of class, whether that class has `context` or not.
- `get_it` provides many different ways to register dependencies. Two of the common ways are:
- `registerFactory` will give a new instance every time get<T>() is called.
```
void registerFactory<T>(FactoryFunc<T> func) // returns an NEW instance of an implementation of T ```
- `registerSingleton`  will create only one instance of the **Car** at the initialization. This will not generate new instances every time like `registerFactory`.
```
void registerSingleton<T>(T instance) // returns a singleton instance of an implementation of T
```

---------------------------------

## Wrapping Up
- Thank you for reading. Hope you liked it.
- **Comments ** and **Feedbacks ** are welcomed 🙂
- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629398281133/r_GAKNI_T.gif)
