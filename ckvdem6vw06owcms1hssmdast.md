---
title: "Code Generation In Flutter"
datePublished: Sat Oct 30 2021 06:09:04 GMT+0000 (Coordinated Universal Time)
cuid: ckvdem6vw06owcms1hssmdast
slug: code-generation-in-flutter
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1635526266362/9_AthhMUi.png
tags: programming-blogs, dart, flutter, flutter-examples

---

## What is Code Generation 🛠️?
- When developing an application/software, we want our code to be **clean**,**readable **, and **reusable**. The **DRY** principle is followed in software development. **DRY ** stands for **'Do not repeat yourself.'** It is the idea of **reducing repetition in code**.
- We may achieve the same result with less and more legible code if we use **Code generation**. The generator just has to be written once, and it may be reused as many times as you need.
- Let's now understand the use of code generation in development.
- 
![UpThumbsUpGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1635519527400/uH28ozn5O.gif)
-------

## Use cases of Code Generator 🤔
- When you create a Data class in *Dart*, you manually have to define the `toJson` and `fromJson` methods for serializing. For example :
- `User.dart`
```
class User {
    User({
        required this.name,
        required this.city,
        required this.age,
    });

    String name;
    String city;
    int age;

    factory User.fromJson(Map<String, dynamic> json) => User(
        name: json["name"],
        city: json["city"],
        age: json["age"],
    );

    Map<String, dynamic> toJson() => {
        "name": name,
        "city": city,
        "age": age,
    };
}
```
- This looks good. Right? Yea, I agree. But think about it this way, In general, we have an application where it has tons of data coming from the APIs. 
- Now if you're thinking to write the Data class for more than `50` or `100` properties, then.....
- 
![MaybeYouShouldSeeADoctorKyleBroflovskiGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1635519584540/IXAJdyE-8.gif)
- 😅. Because it will take a long time to write all the properties in the class and then initialize it in the factory function constructor and `toJson` method. It will also raise the number of lines of code while also increasing the complexity.
- This is one of the reasons why, when developing medium/large-scale apps, you should consider using a code generator.
- **Another example could be: **
- If you want to compare two objects you have to override `==` and `hashCode` methods. If we consider the above example,
- 
```
void main() {
  final user1 = User(name:"Abc",city: "zzz",age: 12);
  final user2 = User(name:"Abc",city: "zzz",age: 12);
  
  print( user1 == user2);  // false
}
```
- When you compare `user1` and `user2`, you will get `false` as output. It's because you have to override the `==` and `hashCode` methods.
- 
```
class User {
  User({
    required this.name,
    required this.city,
    required this.age,
  });

  String name;
  String city;
  int age;
   
  // ....

  @override
  bool operator ==(Object other) =>
      identical(this, other) ||
      other is User &&
          runtimeType == other.runtimeType &&
          name == other.name &&
          city == other.city &&
          age == other.age;

  @override
  int get hashCode => name.hashCode ^ city.hashCode ^ age.hashCode;
}
```
- This appears to be suitable for small-scale applications once again. However, in medium/large size applications, modifying all of these attributes will result in an increase in complexity and code readability.
- These are the two scenarios I've chosen. However, code creation may be used for a variety of purposes.
- So, how do you use a code generator in a Flutter/Dart app? Let's see next.
-------
## What is [build_runner](https://pub.dev/packages/build_runner) ⚙️?
- `build_runner` is a Dart package that provides a concrete way of generating files using Dart code.
- This package is essential for generating a code inside a dart file. It has a different built-in command which is used to generate code.
- We generally use the `build` and `watch` commands. 
- The `build` command builds the file only once. And after that, it exists. 
- Whereas, the `watch` command continuously watches for the change in the files. If any changes occur then it build that file again.
- To use this package, we have to put it under the `dev_dependencies` inside the `pubspec.yaml` file.
- 
```
dev_dependencies:
      build_runner: <latest_version>
```
- Sometimes, when you build a file, It gives an error that it found conflict in the file. To solve it, add `--delete-conflicting-outputs` argument after the build command.
- Now as we've added the `build_runner` which is responsible for generating the code. We can now use different code generation packages like, `json_serializable`, `freezed`, etc.
--------

## Serializing JSON using `json_serializable`
- This package automatically generates the code for converting `toJson` and `fromJson` by annotating Dart classes.
- We've seen above that writing `toJson` and `fromJson` by self is a tedious and lengthy process. So let's use this package to generate those two functions using this package.
### Install Pacakge
- 
```
dependencies:
      json_annotation: <latest_version>
```
```
dev_dependencies:
      build_runner: <latest_version>
      json_serializable: <latest_version>
```
- If you see in the above code I've also added `json_annotation` package dependencies. It is used to annotate the classes. You'll see the use of it further. Let's now go to the `User.dart` file.
### Importing required packages and Part the User class
- Inside `User.dart` file.
- 
```
class User {
    User({
        required this.name,
        required this.city,
        required this.age,
    });

    String name;
    String city;
    int age;
}
```
- Let's now import the `json_annotation` package.
- 
```
import 'package:json_annotation/json_annotation.dart';
```
- Now if you don't know about the `part` in Dart. Basically, with `part` you can split one library into several files and private members are accessible for all code within these files.
- So as our generated file have to access all the code within the `User.dart` file we have to use `part` like below.
- 
```
part 'User.g.dart';
```
### Annotating the Class
- After this, the use of this `json_annotation` comes into the picture. To tell the generator that this User class needs the JSON serialization logic to be generated. We need to annotate it by simply annotating the User class by `@JsonSerializable()`.
- 
```
@JsonSerializable()
class User {
    User({
        required this.name,
        required this.city,
        required this.age,
    });

    String name;
    String city;
    int age;
}
```
### Implementing `toJson` and `fromJson`
- To generate the `fromJson` and `toJson` for all the properties available in the class. We simply need to write the following code inside the class.
- 
```
@JsonSerializable()
class User {
    User({
        required this.name,
        required this.city,
        required this.age,
    });

    String name;
    String city;
    int age;
  
    // Responsible for creating a instance from the json.
    factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);

    // Responsible for converting the map to json.
    Map<String, dynamic> toJson() => _$UserToJson(this);
}
```
- That's all you have to do in order to create `fromJson` and `toJson`. You will see some error saying this class is not defined, etc. To resolve this, you have run build_runner commands in the terminal. So let's do it.
### Generating the Code
- As discussed earlier, we can generate the code in two ways, either generate the file once or continuously watch the file and then generate.
- Let's first generate it using the first option. To do that open your terminal and run the below command.
- 
```
flutter pub run build_runner build
```
- This triggers a one-time build that goes through the source files, picks the relevant ones, and generates the necessary serialization code for them.
- 
![build_runner terminal.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1635573790907/96gKfJfXj.png)
<center>**Or**</center>
- 
```
flutter pub run build_runner watch
```
- This will continuously watch for changes. It is safe to start the watcher once and leave it running in the background.
- After running it you will now see the generated file inside the folder.
- 
![generated_file.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1635573975567/tPPWaXR1k.png)
- And it will look something like below
- 
![part_file.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1635574002166/dSEszpvbA.png)
- 
### Using User model Class
- Now to use the `fromJson` and `toJson`, you can simply first decode the `jsonString` with the help of the `jsonDecode` function. And then you can pass it inside the `fromJson` constructor.
- 
```
final userData = jsonDecode(response.body);
final user = User.fromJson(userData);
```
- If you want to know what other things `json_serializable` provides. You can goto the below link:
- %[https://pub.dev/packages/json_serializable]
---------

## Disadvantages of Code Generation 😕
1. When you utilize a code generator, your code becomes reliant on it. A code generation tool must be kept up to date. 
If you created it, you must keep upgrading it; if you are simply using an existing one, you must either hope that someone maintains it or take over yourself.
2. Generated code is almost certainly less optimal than hand-written code. Sometimes the difference is minor and insignificant, but if your application requires every bit of performance, code generation may not be the best option for you.
3. When you use code generation, the number of files rises and they become dependent on one another.
4. If you make any changes to the main class, you must either execute the build command again or use the watch command, which is always running in the background.
------------
## Wrapping up
- **That's it !! Thank you for taking the time to read this article. 🙏. If you found it useful, please share it with others.**
- **Also, if you have any suggestions, please leave them in the comments section✍️. **
- **See you in the next article. Until then....**
- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1635521427792/tuy4VVSc3.gif)
