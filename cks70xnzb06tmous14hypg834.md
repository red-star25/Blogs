---
title: "Flutter Widget In Detail: MaterialApp"
datePublished: Wed Aug 11 2021 05:00:20 GMT+0000 (Coordinated Universal Time)
cuid: cks70xnzb06tmous14hypg834
slug: flutter-widget-in-detail-materialapp
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1628597934441/_zquCuhiu.png
tags: dart, flutter, flutter-sdk, flutter-examples, flutter-widgets

---

### Introduction:
- **MaterialApp** is Futter's one of the most powerful widgets. if you create a basic Flutter app then the first widget you'll see is **MaterialApp**
- **MaterialApp** wraps a number of widgets that are commonly required for material design applications.
- By wrapping your application inside the **MaterialApp**, you're telling your app to use **Android's Material Design**, which is a design system created by Google to help teams build high-quality digital experiences for Android, iOS, Flutter, and the web. 
- 
![material-design.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1628317225123/64o1D8t4o.jpeg)
- [More about Material-Design](https://material.io/design/introduction)
- But if you want to follow **iOS** design patterns, then you have to wrap your app inside **CupertinoApp**. There are many widgets provided by flutter to design your app for **iOS** platform.
- 
![cup-final.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628318006917/s4Q6U6VEM.png)
- > Another thing I want to point out is that **MaterialApp** and **CupertinoApp** are built upon **WidgetApp**.
- Let's understand the **MaterialApp **widget and its properties in detail with some examples.

-------------------

### MaterialApp
- We can consider this as an application that uses **material design**.
- Before creating **MaterialApp** we have to import **material package**  which is provided by flutter SDK.
- To import **material** package :
- 
```
import 'package:flutter/material.dart';
```
- This package provides us all the widgets that we can use in our application. For example: `AppBar`, `Scaffold`, `BottomNavigationBar`, `Card`, `Chip`, `BottomSheet`, etc.
- **MaterialApp** must have at least one of `home`, `routes`, `onGenerateRoute`, or `builder` properties non-null. Without it you will get an error.
- 
```
import 'package:flutter/material.dart';
class MyApp extends StatelessWidget {
       @override
       Widget build(BuildContext context) {
            return MaterialApp();
       }
}
```
- Output :
- 
![errormaterial.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628323092355/LD6gLMrvw.png)
- Now let's take a deep dive into all the properties, and understand what each and every property does.

- ### `home`:
- This is a default `route` of an app.
- It means whatever is defined here is the first thing you will see on the screen.
- It takes `Widget` as an input.
- Usually, we define home, signIn, signUp, splash screens, but you can put any widget here.
- 
```
MaterialApp(
      home: MyFirstPage(),
);
```
- Output :
- ![home.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628323529575/-SpFaweCa.png)
------------------

- ### `title`:
- This takes `String` as value.
- If you put value in `title`, you will not see any changes in your app. It will still show an empty blank screen.
-  You will see this title when you press the **"recent apps"** button.
- Let's define `title` in **MaterialApp**
- 
```
MaterialApp(
     title: "Widget In Detail",
     home: MyFirstPage(),
);
```
------------------
- ### `debugShowCheckedModeBanner`:
- This is a banner that indicates that currently, our app is running in `debug mode.
- The **default ** value of this property is `true`.
- To remove this banner, simply put `false` inside it.
-  In release mode, this has no effect.
- 
```
MaterialApp(
      debugShowCheckedModeBanner: true,
      title: "Widget In Detail",
      home: MyFirstPage(),
);
```
- Output :
- 
![Debugbanner.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628324237450/wrpH-AlOll.png)

-----------------
- ### `builder` :
- A builder that builds a widget given to a child.
- `builder` function takes two parameter `context` and `widget.`
- The return type of `builder` is `Widget`.
```
MaterialApp(
        builder: (context,widget) {
            return widget;
          }
);
```
- By using `builder` property, we can override properties like `Navigator`, `MediaQuery`, or `internationalization` that is set by `MaterialApp`
- For example, If no routes are provided to the regular `MaterialApp` constructor using `home`, `routes`, `onGenerateRoute`, or `onUnknownRoute`, the child will be `null`, and it is the responsibility of the `builder` to provide the application's `routing machinery`.
- If `builder` is null, `routes` must be provided using one of the other properties (`home`, `routes`, `onGenerateRoute`, or `onUnknownRoute`,).
> Use cases : 
> 1. To insert widgets above the `Navigator`.
> 2. To insert widgets above the `Router` but below the other widgets created by the `WidgetsApp` widget
> 3. For replacing the `Navigator`/`Router` entirely.
- If `Navigator` is not provided in the builder we will not able to use `Navigator.push`, `Navigator.pop`, `Hero` etc.
- 
![TheNightmareGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628329352202/cDK2__Ayx.gif)
- Okay let me take an example. Consider the below code : 
- 
``` 
class MyApp extends StatelessWidget {
       @override
       Widget build(BuildContext context) {
           return MaterialApp(
              builder: (context, child) {
                 return MyHomePage();
            });
       }
}
```
```
class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: ElevatedButton(
          onPressed: () => Navigator.push(
            context,
            MaterialPageRoute(
              builder: (_) => SecondPage(),
            ),
          ),
          child: Text('To Second Screen'),
        ),
      ),
    );
  }
}
```
- 
![builder1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628329753615/vRFZV-Y0Y.png)
- Now if we press the button, nothing will happen. Why? Because we haven't passed `Navigator` in our app. You can see that in the above code, In `builder` we are simply returning  `MyHomePage()`.
- ![btnnotworking.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628330168626/YjEh6LM5A.gif)
- Let's wrap that child inside `Navigator` and pass the routing information accordingly.
```
MaterialApp(
      builder: (context, child) {
      return Navigator(
        // If you don't know about `initialRoute` and `onGenerateRoute`, I've explained these properties below. 
        initialRoute: "/",
        onGenerateRoute: (settings) {
        if (settings.name == '/') {
          return MaterialPageRoute(builder: (_) => MyHomePage());
        }
        return null; // Let `onUnknownRoute` handle this behavior.
      },
      );
});
```
- Output : 
- 
![btnworking.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628330444586/hcHnh1Luf.gif)
- So as you can see, now we are successfully navigating to Second Screen.
- Material-specific features such as `showDialog` and `showMenu`, and widgets such as `Tooltip`, `PopupMenuButton`, also require a `Navigator` to properly function.

-----------------------------

### `routes` :
- If you want to navigate via `namedRoutes`, you have to first define all the routes in the application's top-level routing table. i.e, in `MaterialApp`'s `routes` property.
- You can think of `routes` as a `table` where each `screen` is binded with a particular `path`. For example, `"/home"` is binded with `HomeScreen()` widget.
- It takes `Map<String, Widget Function(BuildContext)>` as an input. Where `key` is the actual `pathName` (ex: "/home","/signIn" ,etc), and `value` is actual Widget/Screen (ex: HomeScreen(), SignIn(), etc).
- Example :
```
MaterialApp(
      routes: {
        "/": (_)=> MyHomePage(),
        "/secondScreen": (_) => MySecondPage(),
      },
    );
```
- Now you can use `Navigator.pushNamed(context, "/secondScreen");` for navigation.
```
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: ElevatedButton(
          onPressed: () => Navigator.pushNamed(context, "/secondScreen"),
          child: Text('To Second Screen'),
        ),
      ),
    );
  }
}
```
- Output : 
- 
![btnworking.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628332366488/stSHIGB0y.gif)
- > Notice that I've not defined `home` property inside `MaterialApp`. As I've already defined `/` key in the `routes` property. The `MaterialApp` will automatically consider `/` key defined in the `routes` map as a `Starting Point of Application`. 
> This is not any kind of magic. Behind the scene, `Navigator.defaultRouteName` has  `/` value by default.
- If `home` is specified, then it implies an entry in this table for the `Navigator.defaultRouteName` route `/`. 
> Note: You cannot specify `home` and `/` key in `route` both at the same time. It will lead to an error.

----------------------

### `onGenerateRoute` :
- This is used when the app navigates to the `named route`.
- If this returns `null`, For example : 
```
MaterialApp(
      onGenerateRoute: (settings) {
        return null;
      },
      home: MyHomePage(),
);
```
- Then all the routes are `discarded` and Navigator.defaultRouteName is used instead (/). Which here is `MyHomePage()`.
- Let's see how we can generate route using `onGenerateRoute`.
- Example :
- 
```
MaterialApp(
      onGenerateRoute: (settings) {
        if (settings.name == "/secondScreen") {
          return MaterialPageRoute(builder: (_) => MySecondPage());
        }
      },
      home: MyHomePage(),
);
```
- As you can see in the above snippet, there is one `parameter` named `settings` , passed in the `onGenerateRoute`. This `settings` is called `RouteSettings`, which provides us two things. `name` and `arguments`.
- `name` is the name of a `routename`. For example: If we call `Navigator.pushNamed(context, "/secondScreen");`, then `name` gets a value as `/secondScreen`.
- `arguments` is the data which has been passed through the screen. For example:
- 
```
ElevatedButton(
              onPressed: () => Navigator.pushNamed(context, '/secondScreen',
                  arguments: 42), // Passing argument
              child: Text('Go to BarPage'),
),
```
- Here as you can see the `argument` property defined in `pushNamed` constructor, which later will be assigned to the `settings.arguments`
- Now you can use `Navigator.pushNamed(context, "/secondScreen");` for navigation.
- 
```
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: ElevatedButton(
          onPressed: () => Navigator.pushNamed(context, "/secondScreen"),
          child: Text('To Second Screen'),
        ),
      ),
    );
  }
}
```
- ![TheFreshPrinceOfBelAirWaitAMinuteGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628333748302/lMCKsCCvU.gif)
- Then what's the `difference` between `routes` and `onGenerateRoute`. Both are doing the same thing, right?. Well **YES**. Both are used when app navigate via a `namedRoute`.
- BUT, Both has its different use cases. Let's understand..
- `routes` is static. It means it doesn't offer a functionality of passing arguments between screen, or implementing different `PageRoute`.
- This is why `onGenerateRoute` property comes into the picture. 
- With `onGenerateRoute`, you can pass `arguments` between routes. Which is not possible in `routes`.
- Example
- 
```
MaterialApp(
      routes: {
        '/': (_) => HomePage(),
        '/secondScreen': (_) => SecondPage(),
      },
      onGenerateRoute: (settings) {
        if (settings.name == '/thirdScreen') {
          final value = settings.arguments as int; // Retrieve the value.
          return MaterialPageRoute(
              builder: (_) => ThirdPage(value)); // Passing the value
        }
        return null; 
      },
    ),
```
```
class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('HomePage')),
      body: Center(
        child: Column(
          children: [
            ElevatedButton(
              onPressed: () => Navigator.pushNamed(context, '/secondScreen'),
              child: Text('Go to Second Page'),
            ),
            SizedBox(height:10.0),
            ElevatedButton(
              onPressed: () => Navigator.pushNamed(context, '/thirdScreen',
                  arguments: 123),
              child: Text('Go to Third'),
            ),
          ],
        ),
      ),
    );
  }
}
```
```
class SecondPage extends StatelessWidget {
  @override
  Widget build(_) => Scaffold(
        appBar: AppBar(
          title: Text('SecondPage'),
        ),
      );
}
```
```
class ThirdPage extends StatelessWidget {
  final int value;
  ThirdPage(this.value);

  @override
  Widget build(_) => Scaffold(
        appBar: AppBar(
          title: Text('ThirdPage, value = $value'),
        ),
      );
}
```
- Output :
- 
![onGenerate.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628334713559/PB0WkEV0U.gif)

------------------------
### `onGenerateInitialRoutes `:
- The routes generator callback used for generating initial routes if `initialRoute` is provided.
- One use case can be , When you want to navigate user to `IntroPage` if he/she is not authorized and to `HomePage` if authorized.
- Example : 
- 
```
MaterialApp(
      onGenerateInitialRoutes: (route) {
              if (isAuthorized) {
                return <Route>[
                  MaterialPageRoute(builder: (context) => HomePage())
                ];
              } else {
                return <Route>[
                  MaterialPageRoute(builder: (context) => IntroPage())
                ];
              }
      },
      onGenerateRoute: (settings) {
        switch (settings.name) {
          case '/':
            return MaterialPageRoute(builder: (_) => IntroPage());
          case '/homePage':
            return MaterialPageRoute(builder: (_) => HomePage());
        }
      },
),
```
---------------------------
### `onUnknownRoute` :
- This will return a route when `onGenerateRoute` fails to generate a route.
- This callback is typically used for error handling. For example, this callback might always generate a "not found" page that describes the route that wasn't found.
- Example :
- 
```
MaterialApp(
      onUnknownRoute: (RouteSettings settings) {
        return MaterialPageRoute<void>(
          settings: settings,
          builder: (BuildContext context) =>
              Scaffold(body: Center(child: Text('Not Found'))),
        );
      },
      home: HomePage(),
    ),
```

-----------------------

### `darkTheme` :
- By applying the `ThemeData` in the `darkTheme` property, we are telling our app to use this particular `ThemeData` when the system requests for `DarkTheme`.
- For example : We have an app where we've provided toggle for `LightMode` and `DarkMode`. Whenever user toggles the theme to `DarkTheme`, entire app will use the `ThemeData` that is specified in the `darkTheme` property of `MaterialApp`.
- Example : 
```
 MaterialApp(
      darkTheme: ThemeData(
        brightness: Brightness.dark
      ),
    home: HomePage(),
    ),
  );
}
```
- Output :
- 
![darkTheme2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628346591780/jWZY7oKRv.png)
- Let's tweak the values of  `ThemeData`s' `primaryColor` when the app is in dark mode
- 
```
MaterialApp(
      darkTheme: ThemeData(
        brightness: Brightness.dark,
        primaryColor: Colors.red
      ),
      home: HomePage(),
),
```
- Output :
- 
![darkTheme3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628346732235/MVyEY21-Q.png)
- As we can see, the `primaryColor` applied successfully.

-----------------------

### `theme`:
- This is a `default` theme that will be applied to our app. This theme will be applied when the `themMode` value is `light`. i.e. `ThemeMode.light`
- If you want to edit the theme of an app when `themeMode` is `ThemeMode.dark`, you have to specify `ThemeData` in `darkMode` property as discussed above.
- Here we can define default `primaryColor`, `secondaryColor`, `buttonColor` ,etc of our app.
- It takes `ThemeData` as an input.
- Example : 
```
MaterialApp(
      themeMode: ThemeMode.light,
      theme: ThemeData(
        brightness: Brightness.light,
        primaryColor: Colors.green
      ),
      home: HomePage(),
),
```
- Output :
- 
![defaultTheme.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628349565073/Yac8C8-2o.png)

-------------------------

### `themeMode`: 
- This property determines which theme will be used by the application if both `theme` and `darkTheme` are provided.
- The `default` value of `themeMode` is `ThemeMode.system`, which means whatever the theme of the system will be applied by default by our app.
- `ThemeMode` has `3` enums. 
- `ThemeMode.dark`: Use the `theme` defined in `darkTheme` property. It will always use the dark mode (if available) regardless of system preference.
- `ThemeMode.light`: Use the `theme` defined in `theme` property. It will always use the light mode regardless of system preference.
- `ThemeMode.system`: Use either the light or dark theme based on what the user has selected in the system settings.
- Example :
```
MaterialApp(
      themeMode: ThemeMode.dark,
      theme: ThemeData(
        brightness: Brightness.light,
        primaryColor: Colors.green
      ),
      darkTheme: ThemeData(
        brightness: Brightness.dark,
        primaryColor: Colors.red
      ),
      home: HomePage(),
),
```
- As shown in the above example, the value of `themeMode` is `ThemeMode.dark`. Because of that, the `darkTheme` will be applied to our app. If the value is `ThemeMode.light` then `theme` will be applied to our app.
- You can switch between `darkMode` and `lightMode` by toggling the value of `themeMode` using some kind of `listener` that will `listen` to the toggle event and toggles the `themeMode` values accordingly as shown below.
- 
![toggleTheme.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628350681201/uWIg0HSyp.gif)

----------------------

### `highContrastDarkTheme`: 
- When a 'dark mode' and 'high contrast' is requested by the system the theme defined in `highContrastDarkTheme` will be applied.
- Some host platforms (for example, iOS) allow the users to increase contrast through an accessibility setting.
- You can check whether the user requested a high contrast between foreground and background content by `MediaQueryData.highContrast` boolean flag.
- This theme should have a `ThemeData.brightness` set to `Brightness.dark`.
- It will use `darkTheme` when null.

-----------------------

### `highContrastTheme`:
- When `high contrast is requested by the system we can use the `theme`defined in `highContrastTheme`.
- It will use the `theme` when null.

------------------------

### `initialRoute`: 
- The `initialRoute` property tells our app which is the initial page/widget to load.
- The value is a type of `String`. And `default` to `dart:ui.PlatformDispatcher.defaultRouteName`. Which we can override too.
- Example :
```
MaterialApp(
      initialRoute: "/",
      routes: {
        '/': (_) => HomePage(),
      },
),
```
- Here the app will consider `HomePage` as `initial route` as the `initialRoute` is `/`.
- You might think what is the difference between `initialRoute` , `home`, `onGenerateRoute`, and `onGenerateInitialRoute`.
![ExplainTheDifferenceClayJensenGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628352061287/IsgZq00_2.gif)
- There is the only a difference in code readability (but not limited to), see all of them are doing the same job but in different ways:
- `home`s' way to render initial widget:
- 
```
MaterialApp(
    home: HomePage(),
),
```
- `initialRoute`s' way to render initial widget:
- 
```
MaterialApp(
    initialRoute: '/',
    routes: {
      '/': (_) => HomePage(),
    },
),
```
- `onGenerateRoute`s' way to render initial widget :
- 
```
MaterialApp(
    initialRoute: '/',
    onGenerateRoute: (settings) {
      if (settings.name == '/') return MaterialPageRoute(builder: (_) => HomePage());
      return MaterialPageRoute(builder: (_) => UnknownPage());
    },
),
```
- `onGenerateInitialRoute`s' way to render initial widget :
- 
```
MaterialApp(
    onGenerateInitialRoutes: (route) {
      return [
        MaterialPageRoute(builder: (_) => HomePage())
      ];
    }
),
```
--------------
### `navigatorKey`:
- As we've seen above, we are writing our navigation business logic directly from our UI(in view (if we consider MVC)) page. And that's how we usually do. Because for `navigation` we need `BuildContext`. Without `context` we can't navigate to other screens.
- So Is there any way to write our business logic inside the `model` class? Is there any way to navigate without using `BuildContext`?
- 
![YeahMuitoBemGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628398092213/hKEAQU11d.gif)
- **YES**. In Flutter `GlobalKeys` can be used to access the state of a StatefulWidget and that's what we'll use to access the `NavigatorState` outside of the build context.
- We can create `NavigationService` class that contains the `global key`, we'll set that key on initialization and we'll expose a function on the service to navigate given a name.
- 
```
class NavigationService {
  final GlobalKey<NavigatorState> navigatorKey =
      new GlobalKey<NavigatorState>();
  Future<dynamic> navigateTo(String routeName) {
    return navigatorKey.currentState.pushNamed(routeName);
  }
}
```
- Then we register out NavigationService with the locator (here get_it is used for registering).
- 
```
void setupLocator() {
  locator.registerLazySingleton(() => NavigationService());
}
```
- In the main file, we then pass our `GlobalKey` as the `NavigatorKey` to our `MaterialApp`.
- 
```
MaterialApp(
        navigatorKey: locator<NavigationService>().navigatorKey,
        onGenerateRoute: (routeSettings) {
           switch (routeSettings.name) {
              case 'secondPage':
                 return MaterialPageRoute(builder: (context) => SecondPage());
            }
      },
        home: HomePage()
);
```
- Now we can navigate by calling the `navigateTo` function by passing `pathName` . 
- 
```
locator<NavigationService>().navigateTo('SecondPage');
```
---------------------------
### `navigatorObserver` :
- As you know in the flutter navigation is handled by `Navigator` and is also responsible for screen transitions. There are different options like `push`, `pop` screens.
- The list of `NavigatorObserver` can also be passed to `Navigator` to receive events related to `screen-transitions`.
- A custom `NavigatorObserver` can also be used but if the handling of it in the state is required then it is a better option to go with the `RouteObserver`.
- What is **RouterObserver**?
> `RouteObserver` informs subscribers whenever a route of type `R` is pushed on top of their own route of type `R` or popped from it. 
> This is for example useful to keep track of page transitions, e.g. a `RouteObserver<PageRoute>` will inform subscribed `RouteAwares` whenever the user navigates away from the current page route to another page route.
- Let's understand how to use RouteObserver in our app,
- We have to extend `RouteObserver` for using `3` methods, `didPush()`, `didReplace()`, `didPop()`, 
- 
```
class MyRouteObserver extends RouteObserver<PageRoute<dynamic>> {
  void _sendScreenView(PageRoute<dynamic> route) {
    var screenName = route.settings.name;
    print('screenName $screenName');
    // do something with it, ie. send it to your analytics service collector
  }
```
```
  @override
  void didPop(Route<dynamic> route, Route<dynamic>? previousRoute) {
    super.didPop(route, previousRoute);
    if (previousRoute is PageRoute && route is PageRoute) {
      _sendScreenView(previousRoute);
    }
  }
```
```
  @override
  void didPush(Route<dynamic> route, Route<dynamic>? previousRoute) {
    super.didPush(route, previousRoute);
    if (route is PageRoute) {
      _sendScreenView(route);
        }
    }
} // End of MyRouteObserver class
```
- After that, You need to call this class in main.dart & It will automatically notify all the screen transitions.
- 
```
final RouteObserver<PageRoute> routeObserver = RouteObserver<PageRoute>();
```
```
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      navigatorObservers: [MyRouteObserver()],
      routes: {
        'pageone': (context) => PageOne(),
        'pagetwo': (context) => PageTwo()
      },
      home: MyHomePage(),
    );
  }
}
```
-------------------

### `locale` :
- This property of the `MaterialApp` class allows us to immediately specify what locale we want our app to use.
- If the value of this is `null` then the system's locale will be applied to our app.
- This `locale` property allows us to force the locale of the app to the locale specified in `locale`, regardless of the locale of the device.
- It takes `Locale(String _languageCode, [String? _countryCode])` as an input.
- Example : 
```
MaterialApp(
  locale: Locale('hi', ''),
  home: HomeScreen()
);
```
- This is the easiest way to define `locale` of our app.

--------------------
### `localeResolutionCallback` :
- This callback is responsible for choosing the app's `locale` when the app is started, and when the user changes the device's `locale`.
- It is recommended to provide a `localeListResolutionCallback` instead of a `localeResolutionCallback` when possible, as `localeListResolutionCallback` is in the first priority.
- Example : 
```
MaterialApp(
      localeResolutionCallback: (deviceLocale, supportedLocales) {
        for (var locale in supportedLocales) {
          if (locale.languageCode == deviceLocale!.languageCode &&
              locale.countryCode == deviceLocale.countryCode) {
            return deviceLocale;
          }
        }
        return supportedLocales.first;
      },
      home: HomePage(),
    ),
```
- What this above code will do is, It will check if the current app supports the device locale or not. If not then, we can simply return the `locale` from the `supportedLocale`.

------------------------
### `localizationsDelegates` :
- If we see the `material` and `cupertino` widget, For ex: `calender`, `datePicker` etc, there are obviously texts/numbers written on it.
- 
![datepicker.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1628358168623/bS9pb3ICG.jpeg)
- Now what if we want to translate those texts?
- So this `localizationsDelegates` provides us three important in-built `delegates`:
`GlobalMaterialLocalizations.delegate`,
`GlobalWidgetsLocalizations.delegate`,
`GlobalCupertinoLocalizations.delegate`.
- These three `delegate`s are responsible for translating those `material` and `cupertino` widgets. 
- 
![datepickerar.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628358324604/VOB2WsS6g.png)
- We can also create our own `delegates` to translate our app's texts. I can't explain that here, as it is out of the scope of this blog. I'll explain this in a future blog.

---------------------
### `localeListResolutionCallback` :
- This callback is responsible for choosing the app's `locale` when the app is started, and when the user changes the device's locale.
- When a `localeListResolutionCallback` is provided, Flutter will first attempt to resolve the `locale` with the provided `localeListResolutionCallback`. If the callback or result is `null`, it will fallback to trying the `localeResolutionCallback`. If both `localeResolutionCallback` and `localeListResolutionCallback` are left `null` or fail to resolve (return `null`), the a basic fallback algorithm will be used.
- The `priority` of each available fallback is:
- `localeListResolutionCallback` is attempted first.
- `localeResolutionCallback` is attempted second.
- Flutter's basic resolution algorithm, as described in `supportedLocales`, is attempted last.
- This callback function takes two arguments.
- `locale`: List of locales.
- `supportedLocale`: supportedLocale
- Example :
```
MaterialApp(
      localeListResolutionCallback: (locales, supportedLocales) {
        print(locales);
        print(supportedLocales);
        return null;
      },
      home: HomePage(),
),
```
- Output : 
- 
![localeList.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628353860885/AQejUb4ni.png)
- I'm executing this code on `dartad.dev` (Windows).

------------------------
### `restorationScopeId` :
- As a developer, we need to take care of the app's user interface by preserving it. By doing this, It creates an illusion that your app is always running.
- Sometimes interruptions can occur on devices and might cause the system to terminate your app to free up resources.
- But the users do not know all these behind the scene activities. They only expect your app to be in the same state as when they left.
- For that `State Preservation` and `Restoration` concepts are used. It ensures that the app returns to its previous state when it launches again.
- Flutter has the `RestorationManager` which is responsible for handling all the state restoration work. We don't usually use it directly.
- `RestorationBucket` is used to hold the piece of the restoration data that our app needs to restore its state later.
- `RestorationScope` is used to provide a scoped `RestorationBucket` to its descendants.
- If the `restorationScopeId` parameter is `null` then, the restoration is disabled for its descendants.
- **`RestorationMixin`** is the one that is used by our widget's state. It provides use an API to save and restore our state.
- And finally, we have to use `restorable properties`, which are used to represent the data to be stored in the buckets.
- 
![LetsTakeAnExampleForInstanceGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628402196741/KGBcw2hRU.gif)
- First of all we have to provide a `restorationScopeId` to our `MaterialApp`.
- 
```
MaterialApp(
      restorationScopeId: 'root',  //default value if null.
      home: HomePage(),
);
```
- Then use `RestorationMixin` mixed-in with `HomePage`
- 
```
class _HomePageState extends State<HomePage> with RestorationMixin {
    // .....
}
```
- After that create `restorable` properties that we want to restore if something went wrong.
- 
```
final RestorableInt _index = RestorableInt(0);
```
- The final step is to resgister our restorable properties for restoration.
- 
```
@override
  // The restoration bucket id for current page
  String get restorationId => 'home_page';

  @override
  void restoreState(RestorationBucket? oldBucket, bool initialRestore) {
    // Register our property to be saved every time it changes,
    // and to be restored every time our app is killed by the OS!
    registerForRestoration(_index, 'nav_bar_index');
  }
```
- If you want to test this code. First enable the `Don't keep activities` from the mobile's `Developer Options`.
- Now lets see the output : 
- 
![restoration1.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628402725756/_1hm2EecR.gif)
- As you can see that the selected setting option is still selected.
- But if you try this without `restoration` you will notice that the index will always come back to `Home`.
- 
![restoration2.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628402868163/XmdD62JVz.gif)

-----------------
### `shortcuts`: 
- We can add shortcut keys to perform certain tasks by using the `shortcut` property.
- It takes `Map` of type `LogicalKeyState`.
- `LogicalKeyState` is a set of `LogicalKeyboardKeys` that can be used as the keys in a map.
- Example : 
```
class AddIntent extends Intent {}
```
```
MaterialApp(
      shortcuts: {
        LogicalKeySet(LogicalKeyboardKey.arrowUp): AddIntent(),
      },
      home: MyHomePage(),
);
```
- Now we have to wrap the widget tree inside `Actions`. This will dispatch the actions when you press the shortcut key provided in `shortcut` property.
- 
```
class _MyHomePageState extends State<MyHomePage> {
  int _number = 0;
  changeNumber() {
    setState((){
      _number += 1;
    });
  }
```
```
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Actions(
        actions: {
          AddIntent: CallbackAction<AddIntent>(
            onInvoke: (intent) => changeNumber(),
          ),
        },
        child: Center(
          child: Container(
          height:100,
          width:100,
          color:Colors.red,
          child: Focus(
            autofocus: true,
            child: Center(
            child: Text("$_number")
          ),
          )
        ),
        )
      ),
    );
  }
}
```
- Output :
- 
![shortcut.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628404812962/JXoLAGAqz.gif)

----------------
### `scaffoldMessengerKey` :
- A key to use when building the ScaffoldMessenger.
- If a scaffoldMessengerKey is specified, the ScaffoldMessenger can be directly manipulated without first obtaining it from a BuildContext via ScaffoldMessenger.of: from the scaffoldMessengerKey, use the GlobalKey.currentState getter.

-----------------

## THAT'S IT
- That's all you need to know about the `MaterialApp` widget.
- I know that, it's a lot of properties and a lot of stuff is going on. But if you try and practice it, you will remember it easily.


![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628405110285/WnbEJqbyN.gif)

> Previous Widget In Detail : [AlertDialog](https://dhruvnakum.xyz/flutter-widget-in-detail-alertdialog)