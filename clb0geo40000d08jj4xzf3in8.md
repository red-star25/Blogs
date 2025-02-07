---
title: "Flutter Riverpod: A Guide to Provider"
datePublished: Mon Nov 28 2022 07:13:30 GMT+0000 (Coordinated Universal Time)
cuid: clb0geo40000d08jj4xzf3in8
slug: flutter-riverpod-a-guide-to-provider
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1669566198361/aRJKzhMfY.png
tags: programming-blogs, dart, flutter, beginners, state-management

---

## Getting Started

![1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669480191054/Wgh3E8HRv.png align="left")

<center> **Welcome to my blog 🙏🏻!** <center/>

I'm so glad you're here. I know it can be overwhelming when you first start learning about state management, and I want to help you get started as quickly as possible.

In this post, we'll start with an introduction to the concept of state management and Provider. In the upcoming blog, We'll then go over different types of Providers that Riverpod has to offer to us and will see how it works and how it makes our lives easier.

After that, we'll create a real-world example using Riverpod. This will help you get a better understanding of how all of these providers work together to make our lives easier.

So without further ado, Let's get started.

---------
## Intro to Riverpod
* Flutter Riverpod is a modern, lightweight state management library for Flutter. 
* It is designed to make managing and accessing application state easy, while offering powerful features like state immutability, state isolation, and dependency injection. 
* With Flutter Riverpod, you can easily manage your application state using StateProviders, StateNotifiers, StateNotifierProviders, FutureProviders, and StreamProviders. 
* These tools make it easier to handle complex application state, as well as to make state more accessible and easily shareable across widgets. 
* With Flutter Riverpod, you can easily manage your application’s state, and make sure that your application is running efficiently.

---------

## Installation

![2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669480287229/iGAsRovdF.png align="left")

- In order to install Riverpod package inside your Flutter application, head over to [Pub.dev](https://pub.dev/), and add [flutter_riverpod](https://pub.dev/packages/flutter_riverpod) package inside `pubspec.yaml`.

```
dependencies:
  flutter_riverpod:
```
- After adding it, run `flutter pub get` in your terminal. And now you are ready to do. 

----------

## Providers

![3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669480404379/hW5YPrFZN.png align="left")

- Before we dive into Riverpod, it is very necessary to talk about Providers.
- By far, the most important part of a Riverpod is the provider. 

![4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669480545991/OnYwl1qo_.png align="left")
- It means when you return any data from a provider, you are not only exposing the data but also can listen to the changes happening to it.
- By using different Providers you can listen to the data from multiple locations, you don't need to manually inject anything by yourself, the provider does that for you.

--------

## How to create a Provider?

![5.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669480703545/BYGuzU28f.png align="left")

 
```dart
final myNumberProvider = Provider<int>((ref) => 100);
```
 - As you can see, we've created a simple provider that, as you might expect, returns an integer value.
 - This is the most fundamental type of Provider. This provider just allows you to only **read **its data. It does not allow you to change the data. So remember that.
 - Also, if you create a Provider, make sure it is marked as `final`.
 - Now, the next thing that comes into our mind, is how can we use `myNumberProvider` inside my flutter application. Yoo hold up... you forgot to explain about `ref` parameter. 
 - Yes, I did it on purpose since you will learn more about it in the following sections. So don't worry about it for the time being.

--------

## ProviderScope

![6.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669480773751/HvCWZ5wKO.png align="left")

 - This is the heart of Riverpod; without it, no Provider can function.
 - Basically, we need to wrap the **Root** widget around the ProviderScope. 
 - This gives all of the Providers that you've defined within your application.

```dart
void main() {
  runApp(ProviderScope(child: MyApp()));
}
```
 > I always forgot to do this 😅 and end up in an error like this: **Bad state: No ProviderScope found**

----------- 

## Reading a Provider
 - Okay, so now that we've created a Provider and also declared a ProviderScope, it's time to use this provider inside our application.
 - There are two ways to get the value of our provider:
  1. By using the `Consumer` widget directly.
  2. By extending `ConsumerWidget` instead of StatelessWidget


![7.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669480960692/Gg1WsYH6q.png align="left")

-----------

 ### Using the` Consumer` widget:

```dart
final myValueProvider = Provider<int>((ref) {
  return 100;
});

class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Consumer(       // <==
        builder: (context, ref, child) {
          final value = ref.watch(myValueProvider);
          return Text(value.toString());
        },
      ),
    );
  }
}
```
 - As you can see, We've wrapped our Text widget around the `Consumer` widget. 
 - This widget has one required parameter `builder`. which expose 3 values: `context`, `ref` (Explained in further reading), and `child`.
 - So what this widget actually does is, Whenever any widget is wrapped around this widget, and if the value of the provider used inside it ( `myValueProvider` in our case ) changes then, **only ** the widget wrapped inside it ( `Text()` in our case ) will get re-build, but the rest of the widgets will remain the same.
 - As you can see this is very useful in the case of making an app performance faster.

### By extending `ConsumerWidget`
- Riverpod makes it very easy to access providers with its ConsumerWidget. We just need to replace our classic `StatlessWidget` with the `ConsumerWidger`.

```dart
final myValueProvider = Provider<int>((ref) {
  return 100;
});

class HomePage extends ConsumerWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final value = ref.watch(myValueProvider);
    return Scaffold(
      appBar: AppBar(
        title: const Text('Riverpod'),
      ),
      body: Center(
        child: Text(
          value.toString(),
          style: Theme.of(context).textTheme.headline2,
        ),
      ),
    );
  }
}
```
 - `ConsumerWidget` is identical in use to `StatelessWidget`, with the only difference being that it has an extra parameter on its build method: the `ref` object.
- The difference here is if any provider value changes the whole widget tree will get rebuilt.

---------

Remember, I told you just a few minutes ago that I will explain to you what `Ref` is. I think now it's time to talk about the `ref` object. 

### Ref

![8.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669481229211/5SkMP7YkK.png align="left")

There are mainly 3 use cases of Ref. <br/>

### `ref.read`

![93.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669481412622/RkmHVb7Cc.png align="left")

- Using this, you can directly read the value of the provider without listening to its value. 
- This is usually used inside functions triggered by user interactions. For example, on button press.
-  Example

```dart
class HomePage extends ConsumerWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Riverpod'),
      ),
      body: Center(
        child: GestureDetector(
          onTap: () {
            ref.read(loginRepository.notifier).login();
          },
          child: Text(
            value.toString(),
            style: Theme.of(context).textTheme.headline2,
          ),
        ),
      ),
    );
  }
}
```

### `ref.watch`

![10.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669481504544/mW8dov8-x.png align="left")

- Ref can be used to obtain other providers. 
- For example, if you are creating a provider and that provider depends on the value of some other provider, then you should use this `ref.watch` in order to obtain/listen to that other provider. Here is a simple example:

```dart
// first provider
final helloStringProvider = StateProvider<String>((ref) {
  return 'Hello';
});

// second provider
final worldStringProvider = StateProvider<String>((ref) {
  return 'World';
});

final helloWorldStringProvider = Provider<String>((ref) {
 final hello = ref.watch(helloStringProvider); // obtaining the helloStringProvider value inside this provider.
 final world= ref.watch(worldStringProvider); // obtaining the worldStringProvider value inside this provider.
 return '$hello$world';
});

class HomePage extends ConsumerWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final value = ref.watch(helloWorldStringProvider);
    return Scaffold(
      appBar: AppBar(
        title: const Text('Riverpod'),
      ),
      body: Center(
        child: Text(
          value,
          style: Theme.of(context).textTheme.headline2,
        ),
      ),
    );
  }
}
```
 Now here is what will happen, Whenever anything changes in the provider that you are **watching ** ( i.e `helloStringProvider` and `wordStringProvider` in our case ) inside your current provider ( i.e `helloWorldStringProvider` ), It will rebuild the widget or provider that subscribed to the value (i.e `Text(value)` in our case ).

> FYI: I've used `StateProvider` in the above example. We will look at what it actually does in the upcoming articles. For the time being, only know that we can use it to update the state.

### `ref.listen`

![11.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669481592018/53Qy9E1m3.png align="left")

- You can add a listener to your provider using `ref.listen` and then perform an action such as navigating to a new page or showing a modal, showing a snack bar whenever that provider changes.
- The only difference between `ref.watch` and `ref.listen` is that, rather than rebuilding the widget/provider if the listened-to provider changes, using ref.listen will instead perform some operation/ call a function.
- Example: 

```dart
final numberProvider = StateProvider<num>((ref) {
  return 1;
});

class HomePage extends ConsumerWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final value = ref.watch(numberProvider);

    ref.listen(helloStringProvider, (previousValue, newValue) {
      log('Number Changed: $newValue');
    });

    return Scaffold(
      appBar: AppBar(
        title: const Text('Riverpod'),
      ),
      body: Center(
        child: Text(
          value.toString(),
          style: Theme.of(context).textTheme.headline2,
        ),
      ),
    );
  }
}
```

## When to use `read`, `watch` and `listen`?
- `ref.read`: 
 - `ref.read` usually used in the cases like, on button press, getting the value from other provider, etc.
 - Using `ref.read` should be avoided as much as possible because it is not reactive. It exists for cases where using `watch` or `listen` would cause issues.
- `ref.watch`:
 - Whenever possible, prefer using `ref.watch` over `ref.read` or `ref.listen` to implement a feature. By relying on `ref.watch`, your application becomes both reactive and declarative, which makes it more maintainable.
 - The `ref.watch` method should not be called asynchronously, like inside an `onPressed` of an ElevatedButton. Nor should it be used inside `initState` and other State life-cycles.
- `ref.listen`:
 - `ref.listen` is usually used in cases where you want to perform something when any state changes. For example, Open a snack bar, Navigate to another screen, etc.
 - The `ref.listen` should not be called asynchronously, like inside an `onPressed` of an ElevatedButton. Nor should it be used inside `initState` and other State life cycles.
------------

## Wrapping Up
- **That's all you need to know about Providers and Refs as of now. We are going to use these a lot in further Riverpod series, so you better understand it properly before proceeding to the next one.**
- **I hope you enjoyed and learned something from this article. If you have any feedback/queries, leave them in the comments.**
- **Thank you for spending time reading this article. See you in the next article. Until then....**


![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1669465445453/V1fYVgVzf.gif align="left")

- Connect with me on [Twitter](https://twitter.com/dhruv_nakum), [LinkedIn](https://www.linkedin.com/in/dhruv-nakum-4b1054176/), and [Github](https://github.com/red-star25).
