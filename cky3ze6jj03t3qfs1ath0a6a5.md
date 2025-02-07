---
title: "Flutter BLoC (v8): How to Fetch Data From an API? - 2022 Guide"
datePublished: Fri Jan 07 2022 05:52:07 GMT+0000 (Coordinated Universal Time)
cuid: cky3ze6jj03t3qfs1ath0a6a5
slug: flutter-bloc-v8-how-to-fetch-data-from-an-api-2022-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1641534675227/1n3U2reKB.png
tags: programming-blogs, dart, flutter, apis, flutter-examples

---

## Introduction
- In this blog, we will see how to make an API call by using BLoC Architecture. If you remember all the way back to my article on [Flutter BLoC: A Complete Guide](https://dhruvnakum.xyz/flutter-bloc-a-complete-guide), we went over what BLoC stands for and how it works.
- So, if you haven't checked it out make sure you check it out first. Or if you have a basic understanding of BLoC you can start right away.

----------
## The Idea
- So, first and foremost, I'm going to use a [Joke API](https://v2.jokeapi.dev/). It is a REST API that offers jokes in a consistent and well-formatted manner.
- Every time we call this API, it returns a random Joke. So, first and foremost, let's design a user interface.
- The UI is fairly basic; I used the ExpansionTile widget since the joke comes in two varieties: **Setup and Delivery** and **Simple one-liner**.
- Below it is a button labeled **Load New Joke**, which is used to load new jokes.
----------
## Folder Structure
![folder structure.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641482182846/UUnm5BXmG.png)
- As you can see in the **lib** folder, there is :
1. **bloc** folder: Responsible for managing the business logic
2. **data** folder: It has two folders **model** (Responsible for creating data model classes) and **repositories** (Responsible for making and manipulating the data).
3. **presentation** folder: Responsible for UI design
--------
## UI design
- The UI is very simple as I've explained above. So head over to `home.dart` file and paste the below code.
```
class Home extends StatelessWidget {
  const Home({Key? key}) : super(key: key);
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: const Text('The Joke App'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              const ExpansionTile(
                title: Text(
                  "Joke",
                  textAlign: TextAlign.center,
                ),
                children: [
                  Padding(
                    padding: EdgeInsets.all(8.0),
                    child: Text(
                      "",
                      style: TextStyle(
                        fontSize: 20,
                      ),
                      textAlign: TextAlign.center,
                    ),
                  ),
                ],
              ),
              ElevatedButton(
                onPressed: () {
                  //TODO Load New Joke
                },
                child: const Text('Load New Joke'),
              ),
            ],
          ),
        ),
      );
    }
}
```
![UI design.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641482840403/ZkrUBLqP1Y.png)
- I've used the dark theme here. The code for it is written in `main.dart`.
```
class MyApp extends StatelessWidget {
    const MyApp({Key? key}) : super(key: key);
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        theme: ThemeData(
          brightness: Brightness.dark,
          primaryColor: Colors.grey[900],
          backgroundColor: Colors.grey[900],
          scaffoldBackgroundColor: Colors.grey[900],
          buttonTheme: ButtonThemeData(
            buttonColor: Colors.grey[900],
            textTheme: ButtonTextTheme.primary,
          ),
        ),
        home: const Home(),
      );
    }
}
```
---------
## Dependencies Installation
- We need three packages:
- **flutter_bloc**, **http**, and **equatable**. Let's add them to the dependencies.
```
dependencies:
     flutter_bloc: ^8.0.1
     http: ^0.13.4
     equatable: ^2.0.3 
```
--------
## Creating Model Class
- We are using [this](https://v2.jokeapi.dev/joke/Any) api to get the jokes.
- From this, we need to extract only three things: **setup**, **delivery**, and **joke** parameter. Below is an example of an API response.
![mixed response.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641483646587/6nE82WVZa.png)
- As you can see, this API provides two sorts of jokes: one with only one linear joke and  The setup-delivery joke.
- So let's build a model that will transform this JSON data to our JokeModel.
- Head over to `lib/data/model/joke_model.dart` and paste the following code.
%[https://gist.github.com/red-star25/e1252565070a23f3cc4d042f46b32679]
--------
## Fetching Jokes From API
- We'll use the `http` package to get the API from the internet.
- And this will take place in the **Repository** folder.
- Create a file called `joke_repository.dart` in the **lib/data/repository** folder and paste the code below into it.
```
class JokeRepository {
    final String _baseUrl = "https://v2.jokeapi.dev/joke/Any";

    Future<JokeModel> getJoke() async {
      final response = await http.get(Uri.parse(_baseUrl));
      if (response.statusCode == 200) {
        return jokeModelFromJson(response.body);
      } else {
        throw Exception("Failed to load joke");
      }
    }
}
```
- As you can see, I've constructed a single method that retrieves Joke Data from the API and returns a JokeModel.
- So, the data retrieval phase is now complete. This is what we normally do in any project when we need to get data from an API. - The real part now begins, which is figuring out how to connect this to the BLoC and transmit the data to the user interface.

--------
## Building BLoC

### States
- There will be just three states in our case: **JokeLoadingState**, **JokeLoadedState**, and **JokeErrorState**.
- When the joke is presently being fetched, the **JokeLoadingState ** is utilized to display the Progress Indicator.
- A state with the JokeModel is the **JokeLoadedState**. It will provide the joke data to the user interface.
- If any errors happen during the fetching, the **JokeErrorState** will return an Error message.
- Let's implement it in **lib/bloc/joke_bloc/joke_state.dart**.
%[https://gist.github.com/red-star25/af95663ac7fcfb2dd7477d6618694c9a]

### Events
- Events are nothing but different actions (button click, submit, etc) triggered by the user from UI. It contains information about the action and gives it to the Bloc to handle.
- In our case, we only have one button click, which is **Load New Joke**
- So let's define it inside **lib/bloc/joke_bloc/joke_event.dart**
%[https://gist.github.com/red-star25/29ec3636a4bb3282343f5455bf117aca]

### Bloc
- It acts as a middle man between UI and Data layer, Bloc takes an event triggered by the user (ex: LoadNewJoke button press, Submit form button press, etc) as an input, and responds back to the UI with the relevant state.
%[https://gist.github.com/red-star25/d6a53417ac5b9fc1ef4f4cad742feeed]
- As you can see, I started by creating a JokeRepository. Which I've supplied as a parameter to the constructor.
- And **JokeLoadingState** is the first state I've passed.
- The **mapEventToState** function is no longer required in **Version 8** of the Bloc. We just need to declare different the event body of the constructor.
- When the **LoadJokeEvent** is first invoked, I emit the **JokeLoadingState()**, as you can see.
- After that, I went to the repository and got the Joke. Then there's the fact that I've emitted **JokeLoadedState**.
- Additionally, if an error occurs, the **JokeErrorState** is emitted. It's that simple.

--------
## Providing the Repository
- To provide the JokeRepository globally we have to wrap the **Home()** page around **RepositoryProvider** in the `main.dart` file.
```
class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: (....),
      home: RepositoryProvider(
        create: (context) => JokeRepository(),
        child: const Home(),
      ),
    );
  }
}
```
---------
## Prodiving Bloc
- BlocProvider widget provides a bloc to its children (i.e Widgets).
- BlocProvider is used as a dependency injection (DI) widget so that a single instance of a bloc can be provided to multiple widgets within a subtree.
- Let's wrap our Home page's **Scaffold** around **BlocProvider**.
```
@override
    Widget build(BuildContext context) {
      return BlocProvider(
        create: (context) => JokeBloc(
          RepositoryProvider.of<JokeRepository>(context),
        )..add(LoadJokeEvent()),
        child: Scaffold(
          ....
       )
    )
}
```
- As you can see, I used cascading to add the **LoadJokeEvent**. The initial state will be **LoadJokeEvent**, and the joke data will be displayed on the screen as soon as the screen loads.
- The **JokeBloc**, as you can see, also requires the **JokeRepository**. As a result, we must give it. To retrieve the JokeRepository, we can simply use the **RepositoryProvider.of(context)** method.
----------
## Rendering Widgets Based on the State - BlocBuilder
- Now it's time to render the widget in accordance with the Bloc's state.
- To do this, we must wrap our Home page body around **BlocBuilder**.
- Now we need to show the **CircularProgressIndicator** if the joke is still loading, or the actual joke after it has been obtained. Finally, the error that happened during data retrieval.
- So, let's render all of the widgets based on their state.
%[https://gist.github.com/red-star25/b50a7e6e2ee260422a012ddabd8a5f4f]
--------
## Final Result
![ezgif-5-764995df3a.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641488962615/g7RtPZbDk.gif)
---------
## Wrapping Up
- **I hope you found this article to be beneficial. If you have any feedback/queries, leave them in the comments.**
- **Thank you for spending time reading this article. See you in the next article. So, until then...**

![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641489936804/FQF2GclWd.gif)
