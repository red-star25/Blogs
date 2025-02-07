---
title: "Using Linter to Improve Code Quality"
datePublished: Wed Sep 08 2021 05:38:27 GMT+0000 (Coordinated Universal Time)
cuid: cktb2mitn09qq6gs13gye2bgd
slug: using-linter-to-improve-code-quality
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1631029473478/SRHOdFERUF.png
tags: programming-blogs, dart, flutter, best-practices, programming-tips

---

## Why Linting:
- Linting in Flutter is a linting tool that gives information regarding the quality of the code. A Lint or a Linter is a program that supports linting (verifying code quality) according to your coding rules. It will also report any issues it finds with existing code.
- Using lint tools can help you accelerate development and reduce costs by finding errors earlier.
- As a developer, we are most of the time dealing with problems like bugs, errors, etc. And even after solving it and rolling out our application, we might found out bugs that lead to application crashes.
- 
![ScrollingThroughErrorsGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631019217221/zGCJUc3ih.gif)
- To reduce the occurrence of this type of error and improve the code quality and readability we can use **linter**.
- The definition of **linting** according to Wikipedia - 
> It is a tool that analyzes source code to flag programming errors, bugs, stylistic errors, and suspicious constructs.
- In simple terms, Linter will **warn ** you or will give you the **error ** if your code does not satisfy the rules specified by linter and needs to be resolved for better code quality, readability, and performance-boosting.
- **In Flutter**, we can implement linting by adding [Lint](https://pub.dev/packages/lint) package to our application.
- It is a hand-picked, open-source, community-driven collection of lint rules for Dart and Flutter projects
- If you want to know more about, how to write effective code in Dart then you can check :
- %[https://dart.dev/guides/language/effective-dart/style]
- Here Dart team has provided a bunch of coding styles for writing good and healthy code.
- So let's now implement **linting** in the Flutter application.

-------

## Linting In Flutter
- ### Step 1: Adding package
- %[https://pub.dev/packages/lint]
- Go to `pubspec.yaml` and inside `dev_dependencies` paste the below code :
- 
```
dev_dependencies:
  lint: ^1.6.0
  flutter_test:
    sdk: flutter
```

-----
- ### Step 2: Create `analysis_options.yaml` file
- Go to the root of your application directory, and create one file called `analysis_options.yaml`
- 
![analysis file.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631020204111/e85Uz-rE7.png)

-----
- ### Step 3: Include Rules
- Add following code inside `analysis_options.yaml`
- 
```
include: package:lint/analysis_options.yaml
```
-----
- Now if you open the **PROBLEMS** panel of **VSCode** then you'll see warnings and errors if your code will not satisfy the **rules defined in lint**.
- 
![problems.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631021886326/AQ-gfzUCX.png)
------
- If you don't want to go and see the warning and errors again and again in the Problem panel, then I prefer using **Error Lens** extension available in VSCode
- %[https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens]
- This will highlight the line if it contains any warnings or errors, like below -
- 
![warning.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631022119286/o3qmLFuO_.png)
-----
## Customizing Lint Rules
- You can also add your own rule inside `analysis.options.yaml` or modify existing rules.
- Let's take one example :
- Here I've created one function which does not return anything. As you can see linter is giving me the warning that **Hey, The method `helloLint` should have a return type but doesn't. Try adding a return type to the method.**
- 
![funwar.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631022399173/hyGBsRbgx.png)
- Now if we want to remove this warning then we can simply add the below rules inside `analysis_options.yaml`
- 
```
linter:
  rules:
    type_annotate_public_apis: false
    always_declare_return_types: false
```
- As you can see below in the screenshot we are no longer getting that warning
- 
![removewarning.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631022610927/u_D1kbIIL.png)
- You can see the rules by hovering over the lines in **VSCode**.
- 
![rules.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631022726761/P4yTnzLdh.png)
- You can also **exclude files** from the linter. You just have to define those files inside `analyzer -> exclude:` like below:
- 
```
analyzer:
    exclude:
    - "**/main.dart"
```
- Now you'll no longer get warnings in `main.dart` file.

-------

## Creating Custom Rules
- You can also create your own linting rules for your projects. 
- To do that, Create one `all_lint_rules.yaml` in the root directory.
- Add your rules to this file.
- 
```
# all_lint_rules.yaml
linter:
    rules:
      type_annotate_public_apis: true
      always_declare_return_types: true
```
- Now update the `include` path inside `analysis_options.yaml` file.
- 
```
include: all_lint_rules.yaml
```
- And Voila🎉. You have created your own linting rules.
> Note: Make sure you remove `lint` package before you define your custom linting rule. 
-------
- One other thing I want to mention is to make sure you add comments before your `lint` rules. 
- This will help others to understand why you've enabled or disabled, or modified rules.
- For example:
- 
```
# I think It's easier to read If they are grouped together
sort_pub_dependencies: true
# Single quotes are easier to type and don't compromise on readability
prefer_single_quotes: true
```
------
## Wrapping Up
- **If you like this article 💙, then make sure you share it with others and also provide feedback in comments✍️**
- **Thanks for reading**. **See you in the next article**. **Until then....**
- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631024207530/eq3QkWYr7.gif)
