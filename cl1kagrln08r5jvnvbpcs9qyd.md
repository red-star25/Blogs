---
title: "Very Good CLI - A Very Good Starter Project Generator for Flutter"
datePublished: Mon Apr 04 2022 05:45:30 GMT+0000 (Coordinated Universal Time)
cuid: cl1kagrln08r5jvnvbpcs9qyd
slug: very-good-cli-a-very-good-starter-project-generator-for-flutter
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1648994760554/r2ckF0_7G.png
tags: productivity, dart, flutter, developer, beginners

---

## Introduction
- As you create new Flutter projects, it can be hard to know how to structure your project. How do you structure your applications? Is there a standard way to use the prerequisites? What are the best practices? 
- By using, [Very Good CLI](https://pub.dev/packages/very_good_cli), you will be sure that the best practices for this kind of project are put in place for you. 
- This leaves you free to focus on specific details for your specific application. It also guarantees that you have certain practices in places such as testing, linting, etc.
- Let's dive into the starter project created with the help of Very Good CLI and see what good things are set up for you.

-----------

## Very Good CLI

![logo.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648977667023/G5WOluxAs.png)

- A Very Good Command Line Interface (CLI) is a tool created by the [Very Good Venture](https://verygood.ventures/) team that generates a Flutter starter project for creating a production-level application with many features including like, testing, linting, state management, internationalization, null safety, CI, Logging, Built Flavors, and many more.
- Let's start with the installation part of this CLI.

----------

## Installation
- In order to use Very Good CLI, you need to activate the [very_good_cli](https://verygood.ventures/) package from [**pub. dev**](https://pub.dev/). 
- So, open up a terminal on your window and run the below command

```
dart pub global activate very_good_cli
```
- After the installation has finished you can run `very_good --version` to check that the installation has been done succesfully.

----------

## Creating a Starter Project with Very Good CLI
- In order to create a starter project using Very Good CLI run the below command in your terminal

```
very_good create my_project
```
- The project name is `my_project` in this case. You have the option of changing the name to match your requirements.
- After all of the steps are completed, you'll notice a project created inside your chosen location.
- Let's have a look at the features featured in this project.
---------

## Features of Very Good CLI Starter Project 
-----------

### Folder Structure :

![folder.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648981717251/5TA2kE50e.png)

- The Folder Structure is the first thing that I liked the best in this Starter Project. The VGV team provided the folder structure, which they have used in the development of several production apps and is employed by firms like **Betterment**, **Policygenius**, **Good Money**, **Hamilton**, and others.
- This is the most critical factor I consider when selecting a starter project. Because as the project grows larger, maintaining the files and folders becomes increasingly difficult.
- The Feature Driven Approach has been selected for this project. This means that each app feature will be placed in its own folder, which will include both the business logic and the user interface for that feature.
- This is an excellent scalable application technique. The biggest benefit is that if you wish to eliminate a feature of the application, for an example`Settings`, you can just delete the settings feature folder and you're done. That's it.

------------

### Linting/ Analysis

![lint.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648982001684/LIyFbXhM7.png)
- Another feature the starter project includes is **Linting **. 
- Linting is a set of strict rules that a team follows in order to have a solid and unique way of coding. These rules help you to write better code, readability, and performance.
- Linter will warn you or give you an error if your code does not comply with the rules specified by linter and needs to be resolved for better code quality, readability, and performance.
%[https://dhruvnakum.xyz/using-linter-to-improve-code-quality]

------------

### State Management

![state mgmt.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648982063815/bQJy0nFrs.png)

- We all know that when it comes to developing complicated apps in Flutter, state management can be a pain. To make an app more maintainable, testable, and scalable, the VGV team has included the **Bloc** state management library in the starting project.
- If you're interested in learning more about Bloc state management, I've written a few articles on it. You can have a look at those.
%[https://dhruvnakum.xyz/flutter-bloc-v8-how-to-fetch-data-from-an-api-2022-guide]


------------

### Internationalization

![loca.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648982157225/qhK7VpHiy.png)
- Internationalization is necessary since individuals do not always speak the language in which you expect them to speak. This means you'll need an app with no strings attached and the flexibility to switch between languages quickly.
- This starter project benefits from multi-language support straight away.
- All languages are stored in the 'I10n' subdirectory. files in JSON.
%[https://dhruvnakum.xyz/internationalize-your-flutter-app-its-easy]
-----------

### Null Saftey

![null.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648982339789/QtGHAwxto.png)

- Sound Null Safety, which was formally introduced in a flutter, is another important feature. 
- That means you won't have to waste time worrying about new exceptions that may arise during runtime in your app, and you'll be able to create the entire project on a lot more reliable and quicker platform, all while adhering to solid null safety guidelines.

### Testing

![testing.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648982381637/RER0hIOg_.png)

- This is a starter project with complete coverage. This means that each and every line of code and functionality within the app is subjected to its own set of tests.
- We can just run the complete suite of tests whenever we add, delete, or refactor something to ensure that the application remains fully functioning.
%[https://dhruvnakum.xyz/testing-in-flutter-unit-test]
%[https://dhruvnakum.xyz/testing-in-flutter-widget-test]
%[https://dhruvnakum.xyz/testing-in-flutter-integration-test]
----------

### Continuous Integration

![ci.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648982445802/IzEOBzty4.png)

- If you're working on a large team with multiple developers at the same time, and one of them submits a pull request to merge new changes with the main branch.
- The project will automatically verify it by running specific sets of tests and formatting rules, ensuring that the entire team is aware of the change. 
- If something goes wrong during the implementation of the newly introduced modifications, you'll be able to comprehend flutter and dart errors much more quickly.

----------

### Logging

![log.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648982578152/99zGXSSVa.png)

- We all know that flutter isn't often very clear about what went wrong with the application. As a result, every new project will include built-in extendable logging capabilities to record every potential exception and provide a more detailed explanation of why and where it occurred.

---------

### Built Flavours

![builtflavor.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648982840624/id9Y8Ptk1.png)

- Another essential characteristic of the project's architecture that you may have noticed is that it includes multiple `main` files: one for `development`, one for `staging`, and one for `production`. 
- You may not have noticed this before, but there are three main stages to consider when developing an application professionally: first, you develop it in the development layer, then test and benchmark it in the staging layer, and finally, you release it to the public in the production layer. 
- It's critical to keep these layers separate.

---------

### Cross-Platform Support

![cross.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648982928432/otunEI6aZ.png)

- Cross-platform support is available for this starter project. This means you'll be able to launch your app successfully on iOS, Android, and the web straight away.

----------

## Wrapping Up
- **If you want to know more about Very Good Venture. [Visit](https://verygood.ventures/solution/very-good-start) their website.**
- **Or you can also check the packages that they've made for Flutter and Dart on their [pub.dev](https://pub.dev/publishers/verygood.ventures/packages) account. **
- **I hope you enjoyed and learned something from this article. If you have any feedback/queries, leave them in the comments.**
- **Thank you for spending time reading this article. See you in the next article. Until then...**

- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1648983188948/vJLd9Jhac.gif)

- Follow me on [LinkedIn](https://www.linkedin.com/in/dhruv-nakum-4b1054176/), [Twitter](https://twitter.com/dhruv_nakum), [Gihub](https://github.com/red-star25) for more updates.