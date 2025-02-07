---
title: "Object Oriented Programming in Dart: Classes & Objects"
datePublished: Mon Aug 22 2022 05:50:38 GMT+0000 (Coordinated Universal Time)
cuid: cl74cammr024gncnvat2w89ac
slug: object-oriented-programming-in-dart-classes-objects
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1660932310038/C95CPY__J.png
tags: programming-blogs, dart, flutter, beginners, object-oriented-programming

---

- Yoooo...what's going on🤩? Over a month has passed since I published my last article ☹️. But I'm back now with an interesting topic 😎.
- I'm launching a new series of articles in which I'll discuss the most crucial topic that every developer or programmer must know in order to get hired or placed or to get better in programming in general, and that topic is none other than  🥁🥁🥁   🥁🥁🥁  🥁🥁🥁  

![oops.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660923727179/yRAdhLfg0.png align="left")
- In this series, I'll try to explain each OOPs concept by not just giving you the theory (as universities and schools do), but by also providing examples of how it may be used in real-world situations.
- I'll try my best to cover all the stuff you need to know, and we'll move from simple examples to more complex ones so you can better understand the topic.
- In this first article of the series, I'll try to discuss some of the fundamental elements with OOPs. So fasten your seatbelt and prepare.


![BuckleUpIncrediblesGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1660905699223/UvwebMmKQ.gif align="center")

-------------

## Why OOPs 🤷🏻‍♂️?

- Before learning anything, you should ask yourself, "**Why the heck should I learn this thing?**" or "**How is it going to benefit me, right?**"

- Well, Let me answer that:
 - 👉🏻 All of today‟s modern programming languages heavily rely on OOPs. 

![programming langs.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660923914627/XyGy_FD9E.png align="left")

Because of this, understanding how the OOP functions are essential.
 - 👉🏻As most languages are based on OOP, if you know one language and wanted to shift to another, and if you know basic concepts of OOPs then it will be very easy for you, as the underlying concepts of OOPs remain the same in every programming languages.
 - 👉🏻 Additionally, OOPs is a programming paradigm that has been adopted to a great extent by the IT sector. Therefore, as I previously stated, if you want to land a job at your desired firm, sharpen your OOPs principles.

- Alright, so the next thing that should cross your mind is, What is OOP 🤔?

------------

## What is OOP 🤔 ?
- You know what, let's ask **Steve Jobs** this question, Yup you heard it right. In **1994** Rolling Stone Interview **Jeff Godell** asked the same question to Steve Jobs:  
<br/>
<center>**Would you explain, in simple terms, exactly what object-oriented programming is?**</center>

<br/>

- **Steve Jobs:**
 - Objects are like people. They’re living, breathing things that have knowledge inside them about how to do things and have a memory inside them so they can remember things. 
 - And rather than interacting with them at a very `low level`, you interact with them at a very `high level` of abstraction, like we’re doing right here.
 - *Here’s an example*: If I’m your laundry object, you can give me your dirty clothes and send me a message that says, “Can you get my clothes laundered, please.” I happen to know where the best laundry place in San Francisco is. 
 - And I speak English, and I have dollars in my pockets. So I go out and hail a taxicab and tell the driver to take me to this place in San Francisco. I go get your clothes laundered, I jump back in the cab, I get back here. I give you your clean clothes and say, “Here are your clean clothes.”
 - You have no idea how I did that. You have no knowledge of the laundry place. Maybe you speak French, and you can’t even hail a taxi. You can’t pay for one, you don’t have dollars in your pocket. 
 - Yet I knew how to do all of that. And you didn’t have to know any of it. All that complexity was hidden inside of me, and we were able to interact at a very high level of abstraction. That’s what objects are. They encapsulate complexity, and the interfaces to that complexity are high-level.



- I hope you got some idea from the above example, It is a very high-level explanation and doesn't cover all the concepts of the OOPs, but I think you get the point. You will get more clarity as we will proceed further

------------

## Classes and Objects :

![c&o.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660924062087/ZCBUSQPsg.png align="left")

- **Class** and **Objects** are the two most basic and essential OOPs concepts.
- These two ideas are presented in OOPs to help programmers solve real-world problems.
- To further understand it, let's use an example from the real world:
- There is a company that makes cars. Engineers create a **Blueprint/Draft** of a car before proceeding with the development of the car. 

![carblueprint.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660924224597/cRVQcU3XG.png align="center")

- The factory employees are then given this plan by the engineers. The parts are subsequently assembled in accordance with the blueprint, and the car is then produced.
- Technically speaking, every Car produced using that blueprint is nothing more than **OBJECTS**, and the blueprint is referred to as **CLASS**.

![classObjectcar.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660924324315/k1CoImu4K.png align="left")

- In simple terms Objects can be any living or non-living thing, and to give instruction to that object, how it should work or behave, what it should contain, what kind of action it can perform, all these things are mentioned in the Class
- Another simple example can be: an Apple is an `Object` of `Class` Fruits and have features like red color, sweet taste, etc.


![apple.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660924625758/CclnPlpHv.png align="left")

--------

## Let's Code 🧑🏻‍💻
- Alright, enough theory; let's get our hands dirty with some coding.
- Open up your favorite IDE or just [DartPad](https://dartpad.dev/) if you have not installed dart on your machine.
- Let's take the same example we've seen of Apple and try to implement it in our code.
- In dart to create a class you need to use the `class` keyword followed by the name of the class and then open and close curly braces.
```
class Fruit {}
```
- Now, all fruits have some characteristics, such as name, color, taste, etc. Let's add those parameters to the Fruits class.

```
class Fruit {
 String? color;
 String? taste;
 String? name;
}
```
- Using the fruits, we may carry out some activity, such as "eat." We may define certain functions and methods in class as well. 
- Therefore, let's add a method to our Fruit class named "eat." Additionally, let's print the fruit's name and taste within.
```
class Fruit {
 String? color;
 String? taste;
 String? name;

  void eat() {
     print("The taste of $name is $taste");
  }
}
```

- Now we can say that we've created a blueprint for a Fruit class. Which has different properties like `color`, `name`, `taste`, and a function called `eat` which is basically used to see what that fruit taste like.
- Now let's make an Object of this class inside our main function.

```
class Fruit {
 String? color;
 String? taste;
 String? name;

  void eat() {
     print("The taste of $name is $taste");
  }
}


void main() {
  final apple = Fruit();
}
```

- As you can see we've created an Apple from the class Fruit / from the blueprint of Fruit.
- Now, we need to set the color, name, and taste of this `apple` object. Let's see how to achieve that.

```
void main() {
  final apple = Fruit();
  
  apple.color = "Red";
  apple.taste = "Sweet";
  apple.name = "Apple";
}
```
- You must use the ". " operator to access a Class's properties. If you use '.' after the object name on an IDE, all of that class's properties and methods will be shown.
- The methods of the class can be accessed in the same way as what is shown below:

```
void main() {
  final apple = Fruit();
  
  apple.color = "Red";
  apple.taste = "Sweet";
  apple.name = "Apple";
  
  apple.eat();
}
```
- Run the below code.

<iframe style="width:100%;height:500px;" src="https://dartpad.dev/embed-inline.html?id=89cb753c7800af81bc028480b7b99b71&split=80&theme=dark"></iframe>

- You can see that it says, "The taste of an apple is sweet." Cool. Let's add a banana to our list of objects.

```
void main() {
  final apple = Fruit();
  
  apple.color = "Red";
  apple.taste = "Sweet";
  apple.name = "Apple";
  
  apple.eat();
  
  final banana = Fruit()
    ..color = "Yellow"
    ..taste = "Sweet"
    ..name = "Banana"
    ..eat();
}
```
- Yoo, what does `..` mean? It is known as the **Cascade Operator** in dart. Basically, it's used to avoid repeatedly typing the object name in order to access properties and functions directly. 
- More on Cascade Operator visit : [here](https://dart.dev/guides/language/language-tour#cascade-notation)
- Okay, run this as well.

<iframe style="width:100%;height:400px;" src="https://dartpad.dev/embed-inline.html?id=43e0e6ad0c662cd776ddf1d5daa5cad6&split=80&theme=dark"></iframe>

> Note: The memory is not assigned to a Class when it is created. Only when you construct an Object from it is the memory allotted to it.

------------

## Constructor
- If you've noticed in the above example. We are creating an object like the below :

```
final apple = Fruit(); // What's `()` after Fruit ??
```
- Usually, when writing a method or function, the parenthesis "()" is used. 
- But When we write "()" after the class name, we are essentially accessing a special type of function of that class that is responsible for creating—or more precisely, constructing an object.
- The name of this specialized function is **Constructor**. If you don’t declare a constructor, a default no-argument constructor is provided for you.


### Types of Constructors
- There are 3 ways to construct an Object using Constructor : 
 - **Default Constructor** or **no-arg Constructor**.
 - **Parameter Constructor**.
 - **Named Constructor**.

#### Default Constructor :
- A Constructor which has no parameter is called a default constructor or no-arg constructor. 
- If we don't define it in the class, the Dart compiler will automatically generate it

```
class Fruit {
 
 Fruit(){
   print("Fruit is Created");
 }
 
 String? color;
 String? taste;
 String? name;

  void eat() {
     print("The taste of $name is $taste");
  }
}
```

<iframe style="width:100%;height:400px;" src="https://dartpad.dev/embed-inline.html?id=77456c6043041fae40be96bcac589d70&split=80&theme=dark"></iframe>

> Important: The Constructor is the first thing that is called when you construct any Object from the Class. It means that you can carry out any action here before calling any other methods or accessing any other properties.

#### Parameterized Constructor
- When you pass some parameters/arguments to the constructor, it is called a Parameterized Constructor.
- This type of constructor is usually used when you want to initialize the properties of an object. You can pass single or multiple arguments to this constructor.
- Till now we are assigning the properties of an object (i.e Apple) by `.` operator. But there is a better alternative, which is shown below.


<iframe style="width:100%;height:400px;" src="https://dartpad.dev/embed-inline.html?id=3642de7e1488fdd16112c164d76ff355&split=80&theme=dark"></iframe>

- Here, The `this` keyword refers to the current instance.
> Note:  Use this only when there is a name conflict. Otherwise, the Dart style omits this.

- Don't you think this looks clean? All of the properties have been provided within the constructor itself.

> Note: The Order must be the same as defined in the class otherwise it will throw an error or show an unexpected result.

- In dart, you can also provide **Named **arguments. Named means that when you call a function, you attach the argument to a label.
- Named parameters are written a bit differently. When defining the function, wrap any named parameters in curly braces ({ }). This line defines a function with named parameters:

```
class Fruit {
 Fruit({String color, String taste, String name}){
   this.color = color;
   this.taste = taste;
   this.name = name;
 }
}

void main() {
  final apple = Fruit(color: "Red", name: "Apple", taste: "Sweet");
}
```
- As you can see, now the order doesn't matter.


#### Named Constructor
- Sometimes we need more than one constructor to perform different functionalities. But you can't create multiple constructors with the same name.
- To overcome this problem, dart allows the user to make multiple constructors with a different names.
- The example is shown below :

```
class Fruit { 
 Fruit.foo(){} // Named Constructor
 Fruit.bar(){} // Named Constructor
 
 //...
}
```

### Important Properties of Constructor
1. The Constructor name should same as the Class Name.
2. The Constructor doesn't return anything. It doesn't have any return type.
3. The Constructor is called only once in its lifetime, which is when the Object is created.
-----------
- In the actual world, whatever is made or built has the potential to be destroyed too.
- In C++, we can declare a **destructor** to destroy the created object. It has the same syntax as a constructor.
- But there isn't anything like a destroyer in Dart. Dart's highly advanced garbage collection system takes care of everything by itself.
- So, if someone asks you how to define a destroyer in Dart. You answer it with no, you cannot.

----------------

## Wrapping Up
- Okay, So We've discussed Why we need OOP?, What is exactly an OOP? and 2 fundamental concepts of OOP i.e **Class** and **Object**. We've also seen what are constructors. What are the different types of Constructors in Dart and how we can use them?
- This is you can say an Introductory article to Object Oriented Programming in Dart. Now from the next article onwards, we will be discussing the main pillars of OOP i.e
 - **Abstraction**
 - **Encapsulation** 
 - **Inheritance**
 - **Polymorphism**

- **I hope you enjoyed and learned something from this article. If you have any feedback/queries, leave them in the comments. **
- **Thank you for spending time reading this article. See you in the next article. Until then....**


![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1660931925922/Caj1bfbt8.gif align="left")

--------

- Connect with me on [Twitter](https://twitter.com/dhruv_nakum), [LinkedIn](https://www.linkedin.com/in/dhruv-nakum-4b1054176/), and [Github](https://github.com/red-star25).