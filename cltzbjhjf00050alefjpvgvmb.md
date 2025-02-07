---
title: "Becoming an Expert in Flutter with Clean Architecture: A Comprehensive Guide"
datePublished: Wed Mar 20 2024 04:43:54 GMT+0000 (Coordinated Universal Time)
cuid: cltzbjhjf00050alefjpvgvmb
slug: becoming-an-expert-in-flutter-with-clean-architecture-a-comprehensive-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710844103664/cb016085-d06f-476a-9d69-30bfda07b3e1.png
tags: programming-blogs, dart, flutter, architecture, developer, clean-architecture

---

# Introduction

Hey there! 👋 Thank you so much for stopping by and taking the time to read this blog 😃

* Okay so, picture this: You're about to go on an exciting adventure 🛣️ – not across towering mountains or through jungles, but across the vast and vibrant landscape of software development 🧑🏻‍💻. And the coolest part? You get to be the master architect of this digital realm🌐!
    
* Now, close your eyes 🫣 (well, not literally, because you need to read this 🙃). Picture yourself building a fancy treehouse in your backyard. You start with a strong foundation, right? That's your **Clean Architecture** – the strong base that holds everything together.
    
* But what exactly is Clean Architecture 🤔? Think of it as the blueprint for your software. It's all about keeping things neat and tidy, like organizing your toys into different boxes. Each box has its own purpose, and they all work together.
    
* But why should you care about Clean Architecture 🤷🏻‍♂️? Well, imagine you're on a quest to build the coolest app ever. Without Clean Architecture, it's like setting off on an adventure without a map – you'll get lost in messy code and tangled dependencies.
    
* But don't worry, my friend! Clean Architecture is here to help you on this epic journey. By following its principles, you can tackle any coding challenges ⚔️, slay dragons (bugs 🐞), and emerge victorious as a coding hero 😎!
    
* So Grab your swords (uh, I mean keyboards ⌨️) – it's time to embark on this thrilling journey!
    

---

# **Introduction to Clean Architecture**

> 💡 Just so you know, the brain behind Clean Architecture is none other than Uncle Bob (Robert C. Martin). You've probably heard of him!

![Adventures in Automation: Uncle Bob Martin: The Agile Manifesto, 15 years  later](https://4.bp.blogspot.com/-jcrrXuZVvb4/VuEBngY7SXI/AAAAAAAAK8c/HweGw5zA5Gs/s1600/Robert_Martin-nobull.jpg align="center")

* So according to Uncle Bob, Clean Architecture is a software architectural pattern that focuses on the **Separation of Concerns** which means your code will be separated into different modules.
    
* This way, if one part of the code needs to change, it won't affect other parts, making it easier to maintain and update.
    
* At its heart, Clean Architecture is all about arranging code in a way that makes it **flexible**, **scalable**, and **easy to maintain**. It offers a set of rules and ideas for organizing software, making sure that the important stuff (like business logic) doesn't get mixed up with things like how data is stored or how it's shown to users.
    
* This separation helps keep our code clean and tidy, making it easier to work with and adapt as our projects grow.
    

---

# Understanding The Layers

There are mainly three different layers. Each has its own specific responsibilities.

* Presentation Layer
    
* Domain Layer
    
* Data Layer
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710591792515/9b475db2-d119-4d45-adb2-52380d0335d9.png align="center")
    
    Let's understand each layer one by one now.
    

### Presentation Layer

Okay so, this layer is the interface between your user and the application. It is responsible for handling user interactions like clicking a button, navigating through screens, etc and presenting information to the user in a way that is clear and visually appealing.

* In Flutter, the presentation layer typically consists of :
    
    * **Pages**
        
    * **UI Components such as Widgets** and
        
    * **Business Logic**
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710593059066/f91d42a6-7492-40cf-9235-223e30a7875c.png align="center")

#### Pages

* As the name suggests, this represents the various screens or pages of the applications. They define the layout and structure of the user interface and are responsible for arranging **UI widgets** in a meaningful way.
    
* Pages often listen for user input and interact with the **business logic** to update the UI accordingly.
    

---

#### Widgets

* These are the building blocks of the user interface in Flutter.
    
* Widgets are responsible for rendering visual elements on the screen, such as buttons, text fields, and images.
    
* Widgets combine how UI elements look and behave, making it simple to build complex user interfaces.
    

---

#### Business Logic

* The business Logic Component acts as a bridge between the views and the underlying business logic.
    
* They handle user input, trigger actions in response to user interactions, and update the views with the latest data from the **domain layer**.
    
* This separates the visual part of the app from the business logic, making it simpler to test and keep up to date.
    
* In Flutter, we basically implement the state management of our choice here. For example, Bloc, Riverpod, Mobx, etc.
    

Let's update the diagram

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710600654508/80c27494-55d8-4eac-813e-85fbb85df32d.png align="center")

> To sum up,
> 
> The presentation layer acts as the bridge between users and the app. It deals with user inputs, shows information, and includes UI widgets and views in Flutter apps. This setup keeps the visual parts and business logic separate, making testing and updates easier.

---

### Domain Layer

Clean architecture is an architectural pattern that puts the focus on **Domain**. And that's why it is a **Domain Centric Architecture.** It's the core layer of Clean architecture and serves as the heart of the application.

This layer interacts with two different layers:

* **Presentation Layer:**
    
    * The presentation layer handles user input and provides data for display which it gets from the domain layer.
        
    * This interaction ensures that the presentation layer remains focused on the user interface while the domain layer handles the core business logic of the application.
        
* **Data Layer:**
    
    * The domain layer also interacts with the data layer to retrieve and persist data.
        
    * This interaction ensures that the domain layer remains independent of specific data sources (like remote and local data sources), allowing it to focus on business logic without being tightly coupled to external data sources.
        

Domain Layer typically consists of:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710601521542/cc2525f9-3895-4e3c-b487-3ef78d5663c7.png align="center")

#### Entities

* Entities in Clean Architecture are like the main characters in a story. Think of entities as real-world things or ideas relevant to your application. In an e-commerce application, entities might be `Product`, `Customer`, and `Order`.
    
* Entities don't just hold data. They also define the rules and behaviours that control that data. For example, a `Product` entity might have properties like `name`, `price`, and `stockLevel`, along with **methods** to calculate discounts or check if there's enough inventory.
    
* Entities should not be tied to any specific database, framework, or UI. This makes your code more adaptable and reusable across different implementations.
    
* Let's see an Example of News app, what do you think the entity would be, Article right, so here is how ArticleEntity will look like:
    

```dart
class ArticlesEntity extends Equatable {
  final String? author;
  final String? title;
  final String? description;
  final String? url;
  final String? urlToImage;
  final String? publishedAt;
  final String? content;

  const ArticlesEntity(
    {
      this.author,
      this.title,
      this.description,
      this.url,
      this.urlToImage,
      this.publishedAt,
      this.content
    }
);

  @override
  List<Object?> get props => [author,title,description,url,urlToImage,publishedAt,content];
}
```

---

#### **Use Cases**

* Use cases **represent specific actions** that users can perform to achieve something within your application. They serve as the **bridge between** the user's action and the domain logic encapsulated by entities.
    
* Use cases describe functionality from the user's perspective, For example, `Create a new task` or `Search for completed tasks`, `Login`, `Sign up`, etc.
    
* Use cases typically take inputs from the presentation layer (e.g., user form data) and return outputs representing the results of the domain operations (e.g., success/failure messages, updated data).
    
* Let me give you an example so that you will have a clear understanding.
    

**(Example) Imagine Use Cases as Waiters in a Restaurant**

> **User (Customer):** You (the user) want something specific in the restaurant (the application).
> 
> **Use Case (Waiter):** The waiter takes your order (the user's action, like "Create a new task").
> 
> **Domain (Kitchen):** The waiter relays the order to the kitchen (the domain logic) where the cooks (entities) prepare your food.
> 
> **Presentation (Menu):** The menu (presentation layer) doesn't cook the food, but it shows you what you can order (available actions).
> 
> **Inputs & Outputs:** You tell the waiter what you want (input), and the waiter brings you your food (output, like a success message or updated task).

---

#### Repository (Interface/Abstract Class)

* A repository acts as a **bridge** between the **domain layer** and the **data layer**. Think of it as a middleman responsible for handling data operations without the domain layer needing to know the specific details of how data is stored or retrieved.
    
* Example:
    
    * Imagine you're a librarian (the repository).
        
    * Your job is to manage the books (data) in the library (data layer) and provide them to the readers (domain layer) when they need them.
        
    * You know where each book is located and how to get it, but the readers don't need to know these details. They just tell you which book they want, and you take care of the rest.
        
* So all in all, Repositories hide the details of how data is stored and retrieved from the domain layer.
    

Now, let's update the diagram

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710655470072/ec1e92f9-cee6-400f-95bc-cbce0947b620.png align="center")

> To Sum Up,
> 
> Domain layer serves as the heart of the application, encapsulating the core business logic, entities, and use cases.
> 
> Entities represent the fundamental concepts within the application's domain, while use cases define specific tasks or operations that the application can perform.
> 
> Repositories act as intermediaries between the domain layer and the data layer, abstracting away the complexities of data storage and retrieval.

---

## Data Layer

The data layer in Clean Architecture handles the app's data. It connects the repository layer, which is the access point, to the real data sources like databases, files, and APIs.

It deals with getting, saving, and changing data, making sure the business logic (Domain Layer) and the user interface (UI) don't have to worry about these details.

Data layers consist of:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710656003472/328e55fe-1b54-499b-9198-82fd5fac897c.png align="center")

#### Models:

* Models are like the blueprints for real-life stuff in our code. They're classes or structures that outline what attributes these things have and sometimes even how they behave.
    
* It's pretty similar to Entities, but it comes with functions like `fromJson` and `toMap`. This helps the data layer turn the info/data from third-party APIs or databases into something we can work with.
    

Example:

```dart
class NewsModel extends NewsEntity {
  const NewsModel({
    required String? status,
    required int? totalResults,
    required List<ArticleModel>? articles,
  }) : super(
          status: status,
          totalResults: totalResults,
          articles: articles,
        );

  factory NewsModel.fromJson(Map<String, dynamic> json) {
    return NewsModel(
      status: json['status'],
      totalResults: json['totalResults'],
      articles: (json['articles'] as List)
          .map((e) => ArticleModel.fromJson(e))
          .toList(),
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'status': status,
      'totalResults': totalResults,
      'articles':
          articles?.cast<ArticleModel>().map((e) => e.toJson()).toList(),
    };
  }
}
```

---

#### Repository

* The Data layer's Repository is like the middleman between your app's core logic and where your data lives (like databases or APIs). It's the go-to place for getting and managing data.
    
* It talks directly to either the Remote or Local data sources, deals with any errors that pop up when accessing data and makes sure these errors are handled in a consistent way that the rest of the app can work with.
    
* It also takes on the job of converting data from the way it comes from the data source (like raw JSON) into the way your app needs it (like custom objects).
    

Example:

```dart
class NewsRepositoryImpl implements NewsRepository {
  final NewsRemoteDataSource remoteDataSource;
  final NewsLocalDataSource localDataSource;
  final networkInfo = getIt.get<NetworkInfo>();

  NewsRepositoryImpl(
      {required this.remoteDataSource, required this.localDataSource});

  @override
  Future<Either<Failure, NewsModel>> getNews() async {
    if (await networkInfo.isConnected!) { 
      // Get data from remote if connected
    } else { 
      // Get data from local databse if internet is disconnected
    }
  }
}
```

---

#### Data Sources

* This layer is all about talking with different kinds of data sources, whether it's grabbing stuff from APIs out there on the internet or digging into databases and files stored locally.
    
* When we talk about data sources, we're looking at a whole bunch of options. You've got your traditional databases (think SQLite or MySQL), the cool NoSQL ones (like MongoDB), places to stash your files and settings, or even those network APIs for when you need to pull data from somewhere else.
    
* Repositories act as the intermediary between the domain layer and data sources. They handle the specifics of interacting with each data source.
    
* This decoupling allows you to switch between different data sources without affecting the core functionality of the application.
    

Example

```dart
abstract class NewsRemoteDataSource {
  Future<Response> getNews();
}

class NewsRemoteDataSourceImpl implements NewsRemoteDataSource {
  @override
  Future<Response> getNews() async {
   // Get data from APIs
  }
}
```

Let's now update the diagram finally:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710777529693/1d06efa1-948b-4201-a2b0-6101f703c828.png align="center")

> To Sum up,
> 
> The data layer acts as the **silent orchestra** behind your application's data management. It ensures smooth data access and manipulation, independent of how the domain logic operates.
> 
> **Repositories:** The access point for the data layer. They provide interface for the domain layer to interact with data, hiding the complexities of specific data sources.
> 
> **Data Sources:** The physical locations where your application's data resides, such as databases, files, or APIs.

---

## Conclusion

* That was a lot to take in at once, I bet. But if you've clearly understood these concepts, you'll find it much easier when we start to apply Clean Architecture in our Flutter app in the next article.
    
* If you have any question, I would be happy to answer all in the comments. So make sure you leave a comment.
    
* We looked at the three main layers: **Presentation**, **Domain**, and **Data**,
    
* Each layer has its own job, from handling user interactions to managing the core business logic and data.
    
* We covered entities, use cases, and repositories, which are key parts of your app, making it flexible and efficient.
    

---

## In the next blog...

* In our next blog, we're going to apply everything we've talked about so far.
    
* We'll start building two real-world examples from scratch.
    
* This hands-on approach will help you really understand entities, use cases, and repositories by seeing how they work in actual applications.
    
* An upcoming blog will help you develop an app that's both flexible and easy to maintain. Stay tuned as I will show you how to turn these concepts into real software applications.
    

---

## Are you still here?

I hope you enjoyed reading the blog and found it useful. If you learned something, I would appreciate a comment and a thumbs up.

We will meet again in the next article until then...

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710778497475/1106a531-6d01-4fcf-9795-992aed2f4941.gif align="center")

* Connect with me on [**Twitter**](https://twitter.com/dhruv_nakum), [**LinkedIn**](https://www.linkedin.com/in/dhruv-nakum-4b1054176/), and [**Github**](https://github.com/red-star25).