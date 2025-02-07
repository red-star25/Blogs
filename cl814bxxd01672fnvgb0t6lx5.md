---
title: "Object Oriented Programming in Dart: Encapsulation"
datePublished: Wed Sep 14 2022 04:24:06 GMT+0000 (Coordinated Universal Time)
cuid: cl814bxxd01672fnvgb0t6lx5
slug: object-oriented-programming-in-dart-encapsulation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1662808001665/h1Oxya1Qp.png
tags: programming-blogs, dart, flutter, beginners, object-oriented-programming

---

## In The Previous Article
- Welcome to the 4th article on OOPs in the Dart series. In the previous article, we learned about **Inheritance**. We saw what is it with some examples.
- We also learned about two important keywords `extends` and `with`. Then we went through different types of Inheritance.
- And last but not least we saw the difference between `extends`, `with`, and `implement` keywords.
- In this article, we will learn about an important pillar of OOPs which is **Encapsulation**.
- So, without further a do, let's get started.


![UpThumbsUpGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1662800213173/XBkU-wWg0.gif align="center")

---------

## What is Encapsulation 🤷🏻‍♂️?
- What if I tell you that we learned about Encapsulation already in our previous articles? Yup, you heard it right. We already learned about Encapsulation not directly 
but indirectly.
- If I have to tell you what Encapsulation means in a very high level and simple terms:

<center>*It is the act of combining data and functions into a single entity (referred to as a class) to ensure that no outside suspicious object can alter the data and its functionality.*</center>

### Example
- Okay, let's take a real-world example:
 - Assume you get a project from a bank as a client. They additionally  
 wants you to create a library with **Classes** related to that bank.

![encap1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662802456749/okPXGHBz2.png align="left")

 - Okay, So you started building that library. The library must have the following things. 

![encap2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662802721332/4sC0yxSJJ.png align="left")

 - Bank has their own Databases, And you need to connect to that DB in order to access the details. Okay, after all the compilation and all you created a library.

![encap3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662802858945/TNhwnT4GX.png align="left")

 - Now suppose, you made the Variables of the library **Public**, which means, now anyone with your library imported inside their code, has the ability to **Read** and **Write** into that variable.

 - So, For example, a developer named John created an app that shows Account Balance. As John doesn't have the access to the Bank's DB directly he used the library that you've created to fetch the details.


![encap4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662803498117/CNneAvv8g.png align="left")

 - Now, consider one more developer named Chris. Now, as you made the fields/variables of the library public, Chris got the power to change the account balance variable, although he doesn't have permission to do so.


![20220914_094656_0000.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1663129123836/PARstO-n_.png align="left")

- So, how can we overcome this problem? Well, Here is where Encapsulation comes into play.
- We need to make the variables defined in this library read-only, by doing so, now you only have the access to display the balance in your app, you cannot update it anymore.

> One thing to understand here is, Protecting your variables has nothing to do with Hackers. It has to do with other **Classes** only that you use. This is like giving the key to your home to neighbors whom you want to access your home, still, you want your locker room to be locked and not grant access to it. So think of variables as a safe box that you want to be private and not with public access.

- The above example is highly inspired by the [Amruta Jahagirdar](https://www.quora.com/profile/Amruta-Jahagirdar)'s Answer.

- Now, the question that comes into our mind is, How can we achieve this via Coding? Let's see.

---------
## How to achieve Encapsulation in Dart?
- To achieve encapsulation in Dart, you make fields **private ** and use the public **getter** and **setter** method to access and set the value of that field.
- In dart when you create an Object of a Class, you by default can use the variables defined inside the class using its default getter and setters. For example :

```dart
class BankDetails {
   int? bankBalance;
}

void main (){
   final john = BankDetails();
   john.bankBalance = 1000;

   print(john.bankBalance);
}
```
- Here, john.bankBalance is used to **set** the value `1000` then john.bankBalance to **get ** the value and then printed it.

- Now how can we make the field `bankBalance` private so no outer class has access to it

## Making Private Variable
- Programming languages like JAVA has keywords for making fields private,public. 
- But, Dart does not support keywords like `public`, `private`, and `protected`.
- To make any variable or function private, we just need to append `_` (Underscore) at the starting of the variable name (ex: _variableName).

```dart
// test.dart
class BankDetails {
   int? _bankBalance;
}
```

```dart
// main.dart
import 'test.dart'

void main (){
   final john = BankDetails();
   john.bankBalance = 1000; // Error

   print(john.bankBalance); // Error
}
```

> If you’re curious why Dart uses underscores instead of access modifier keywords like a public or private, see SDK [issue 33383](https://github.com/dart-lang/sdk/issues/33383)

- Now, you might wonder, What if some other verified entity wants to change the balance? To do that we can create custom getters and setters.

```dart
// test.dart

class BankDetails {
  BankDetails({
    required this.password,
  });

  int? _bankBalance;
  String password;

  set setBalance(int newBalance) {
    if(password == getActualPasswordFromDB())
    _bankBalance = newBalance;
  }

  get getBalance => _bankBalance ?? 'UnAuthorized Access';
}

```

```dart
// main.dart
import 'test.dart';

void main() {
  final john = BankDetails(password: '1234');
  john.setBalance = 1000;

  print(john.getBalance);
}
```

- As you can see we've added one extra layer of security now. We've created our custom getter and setter, which prevent any other entity to access the variable directly. 
- Now, When some other entity/class wants to access the variable of our class, we are now checking if the password matches or not. If yes, then the balance gets successfully updated otherwise throws an error saying 'UnAuthorized Access'.

---------

## Conclusion
- Encapsulation is a very crucial concept OOPs. It helps protect Data. Also the Code which is encapsulated looks more cleaner and flexible and can be changed as per the need.
- As we saw, We can change the code read-only or write-only by getter and setter methods. 
- Encapsulation provides reusability, The methods can be changed and the code can be reusable.
- The disadvantages to using Encapsulation are, The length of the code increases drastically. 
- As the code increases, you need to document each and everything to better understand the code. 
- By using encapsulation, the execution of code might get increase.
- But at the end, Using Encapsulation in your code is a good practice and makes your application more reliable, efficient, and secure.

----------

## Wrapping Up
- **I hope you enjoyed and learned something from this article. If you have any feedback/queries, leave them in the comments.**
- **Thank you for spending time reading this article. See you in the next article. Until then....**


![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1662807734205/oi99tMBpb.gif align="left")

- Connect with me on [Twitter](https://twitter.com/dhruv_nakum), [LinkedIn](https://www.linkedin.com/in/dhruv-nakum-4b1054176/), and [Github](https://github.com/red-star25).
