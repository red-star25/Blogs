---
title: "BlocObserver: Debug and Observe your Bloc Easily"
datePublished: Mon Apr 11 2022 06:08:21 GMT+0000 (Coordinated Universal Time)
cuid: cl1ubd43e0am5svnv3hc1dbne
slug: blocobserver-debug-and-observe-your-bloc-easily
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1649574874486/ljFr1X36m.png
tags: programming-blogs, programming, dart, flutter, debugging

---

## Introduction
- **What is up Flutter Dev 👋🏻!!!** In this blog, we'll learn about a unique feature that **Bloc **has to offer.
- I've previously written a few articles about **BLoC** in the past, covering topics such as what it stands for and how it works, how to get data from an API, how to store bloc locally, and so on.
%[https://dhruvnakum.xyz/flutter-bloc-v8-how-to-fetch-data-from-an-api-2022-guide]
%[https://dhruvnakum.xyz/hydrated-bloc-persist-and-restore-your-bloc-statedata]
%[https://dhruvnakum.xyz/flutter-bloc-a-complete-guide]
%[https://dhruvnakum.xyz/flutter-bloc-v8-google-sign-in-and-firebase-authentication-2022-guide]
- So, if you haven't checked it out make sure you check it out first. Or if you have a basic understanding of BLoC you can start right away.
- So, without further ado, let's get started.

----------

## BlocObserver
- **BlocObserver** is a **abstract** class for monitoring BloC instances behavior. This means we can track anytime an event is triggered or a state is emitted. And in the instance of Debugging the BloC, I believe this is incredible.

 - ### `onChange()`
   - You must **override** the **onChange** method inside your bloc in order to see the change when a new state is emitted.
  ```
   class ExampleBloc extends Bloc<ExampleEvent, ExampleState> {
        // Your events here
        on<ExampleEvent>(....)

       @override
         void onChange(Change<ExampleState> change) {
            super.onChange(change);
                debugPrint(change.toString());
                debugPrint(change.currentState.toString());
                debugPrint(change.nextState.toString());
           } 
}
  ```
   - As you can see, the onChange function has one argument which is of type `Change`
   - A `Change` represents the change from **one** State to **another**. 
   - A `Change` consists of the **currentState** and **nextState**.
   - Now whenever a new state is emitted a `Change` occurs, which is why **onChange** is a great spot to add logging/analytics for a specific `cubit`.
   > One thing to remember here is you need to always call `super.onChange` first before performing any operation.

  - ### `onTransition`
   - If you want to observe a bloc whenever a new **event** is added and a new **state** is added, you can override **onTransition** method. 
   - A transition occurs when a new event is added and a new state is emitted from a corresponding EventHandler executed. 
   - onTransition is called before a Bloc's state has been updated. 
   - Which is why it is a great spot to add logging/analytics at the individual Bloc level.

   ```
   class ExampleBloc extends Bloc<ExampleEvent, ExampleState> {
        // Your events here
        on<ExampleEvent>(....)

         @override
            void onTransition(Transition<JokeEvent, JokeState> transition) {
               super.onTransition(transition);
              debugPrint(transition.toString());
        }
}
  ```
   - onTransition is invoked before onChange
   > `super.onTransition` should always be called first.

  - ### `onError`
   - To track a bloc's error whenever it happens, just override the `onError` function within your bloc.
   - onError is called whenever an `error` occurs and notifies `BlocObserver.onError`.
   ```
   class ExampleBloc extends Bloc<ExampleEvent, ExampleState> {
        // Your events here
        on<ExampleEvent>(....)

       @override
         void onError(Object error, StackTrace stackTrace) {
            super.onError(error, stackTrace);
            debugPrint(error.toString());
        }
}
   ```
   > `super.onError` should always be called first.

  - ### `onEvent`
   - As the name suggests whenever an event is added to the Bloc this method is triggered.
   - It is also a great spot to add logging/analytics at the individual Bloc level.

   ```
   class ExampleBloc extends Bloc<ExampleEvent, ExampleState> {
        // Your events here
        on<ExampleEvent>(....)

        @override
          void onEvent(JokeEvent event) {
           super.onEvent(event);
           debugPrint(event.toString());
       }
}
   ```

--------

### Live Example
- To show you the working of the BlocObserver I've taken an example that I've taken inside [this](https://dhruvnakum.xyz/flutter-bloc-v8-how-to-fetch-data-from-an-api-2022-guide) bloc article.

```
class JokeBloc extends Bloc<JokeEvent, JokeState> {
  final JokeRepository _jokeRepository;

  JokeBloc(this._jokeRepository) : super(JokeLoadingState()) {
    on<LoadJokeEvent>(
      (event, emit) async {
        emit(JokeLoadingState());
        try {
          final joke = await _jokeRepository.getJoke();
          emit(JokeLoadedState(joke));
        } catch (e) {
          addError(Exception(e.toString()), StackTrace.current);
          emit(JokeErrorState(e.toString()));
        }
      },
    );
    on<ExtraLoadJokeEvent>(
      (event, emit) async {
        emit(JokeLoadingState());
        try {
          await Future.delayed(const Duration(seconds: 3));
          final joke = await _jokeRepository.getJoke();
          emit(JokeLoadedState(joke));
        } catch (e) {
          addError(Exception(e.toString()), StackTrace.current);
          emit(JokeErrorState(e.toString()));
        }
      },
    );
  }

  @override
  void onTransition(Transition<JokeEvent, JokeState> transition) {
    super.onTransition(transition);
    debugPrint(transition.toString());
  }

  @override
  void onChange(Change<JokeState> change) {
    super.onChange(change);
    debugPrint(change.toString());
    debugPrint(change.currentState.toString());
    debugPrint(change.nextState.toString());
  }

  @override
  void onError(Object error, StackTrace stackTrace) {
    super.onError(error, stackTrace);
    debugPrint(error.toString());
  }

  @override
  void onEvent(JokeEvent event) {
    super.onEvent(event);
    debugPrint(event.toString());
  }
}
```
- Let's now run the app and observe the bloc and the flow of all the overridden methods.

![bloc observer.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1649571951678/sh7mUuhvY.gif)

### Flow of Overriden Observers
- As you can in the above example when the app is loaded the first time, I've added an event called `LoadJokeEvent()`. 
- In our overridden method first of all the `onEvent` method will be triggered. Which you can confirm in the log.
- After that, `onTransition` gets called. As I've said earlier, the `onTransition` will get called before the `onChange`. Which contains the `currentState`, triggered `event` and `nextState`.
- After the completion of `onTransition`, the `onChange` method is called. When the joke data is loading the `JokeLoadingState` passes, after the successful fetch of the data, as you can see in the log we got the `JokeLoadedState` with the instance `JokeModel`.
> So the flow is : `onEvent` > `onTransition` > `onChange` > `onError`
- Let's quickly change the api to random endpoint for showing the error in order to check if our onError method is working or not.

![onError.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1649572707863/MU984MWP-.gif)


-------------

## Creating a Global BlocObserver
- In the above example we are simply, listening to a particular bloc.
- Now, let's see how you can observe all the blocs that you've created globally.
- Create a new file, and then create a class and extends it with the `BlocObserver`.
- That's it, now you can override all the methods here as we did in the above example.
```
class MyGlobalObserver extends BlocObserver {
  @override
  void onEvent(Bloc bloc, Object? event) {
    super.onEvent(bloc, event);
    debugPrint('${bloc.runtimeType} $event');
  }

  @override
  void onChange(BlocBase bloc, Change change) {
    super.onChange(bloc, change);
    debugPrint('${bloc.runtimeType} $change');
  }

  @override
  void onTransition(Bloc bloc, Transition transition) {
    super.onTransition(bloc, transition);
    debugPrint('${bloc.runtimeType} $transition');
  }

  @override
  void onError(BlocBase bloc, Object error, StackTrace stackTrace) {
    debugPrint('${bloc.runtimeType} $error $stackTrace');
    super.onError(bloc, error, stackTrace);
  }
}
``` 
- It will not work now as we've not attached this class anywhere.
- Head over to `main.dart` file and wrap your `runApp` function around `BlocOverrides.runZoned()`. And then pass the `blocObserver` parameter.
```
void main() {
  BlocOverrides.runZoned(
      () {
        runApp(const MyApp());
      },
      blocObserver: MyGlobalObserver(),
    );
}
```
- You're ready to go now. Now, if a new event is introduced, a new state is emitted, or a bloc error occurs, you can see it immediately within your console and manage it quickly.

---------
