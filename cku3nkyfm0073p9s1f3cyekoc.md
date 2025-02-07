---
title: "Animation In Flutter: AnimationController"
datePublished: Tue Sep 28 2021 05:42:39 GMT+0000 (Coordinated Universal Time)
cuid: cku3nkyfm0073p9s1f3cyekoc
slug: animation-in-flutter-animationcontroller
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1632737471176/aRXa9ix86.png
tags: programming-blogs, dart, flutter, flutter-examples, flutter-widgets

---

- In Flutter, we have basically two types of animation: **Implicit**, and **Explicit**.
- The **Implicit** animations are the pre-built animations available in the Fluter SDK.
- The **Explicit** animations need a `controller` to perform an animation.
- The previous two articles in this series we have seen `AnimatedAlign` and `AnimationCrossFade`, which are nothing but an **Implicit** animation as they don't require any type of controller.
- There are different **Implicit** animations available in the Flutter For example, `AnimatedContainer`, `AnimatiedOpacity`, `AnimatedIcon`, etc.
- On the other hand, In **Explicit** animation `AnimationController` is required. The `AnimationController` represents an interpolated range of values that define all possible frames for a particular animation. Let's take a look at the `AnimationController` in detail.

--------

## AnimationController
- The **AnimationController**, as its name implies, is in charge of the animation. It gives you the values that are interpolated between `upperBound` and `lowerBound`. 
- The `upperBound` and `lowerBound` parameters are set to `0.0` and `1.0` by default.
- We may use this controller to play `animation` in either a **forward **or **backward **motion.
- The interpolated values between the `lowerBound` and `upperBound` are generated in every new frame as the animation starts.
- A `SingleTickerProviderStateMixin` is required to function with `AnimationController`. After extending your state, use `SingleTickerProviderStateMixin` to accomplish this:
- 
```
class _MyHomePageState extends State<MyHomePage> with 
SingleTickerProviderStateMixin {
    //....
}
```
- Now, Let's define one AnimationController :
- 
```
class _MyHomePageState extends State<MyHomePage> with 
TickerProviderStateMixin {
    late AnimationController _controller;
}
```
- Let's override the `initState` method to create this _controller. `AnimationController` can be instantiated using a variety of lifecycle methods, although `initState` is the most frequent ().
- 
```
@override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(milliseconds: 500),
      vsync: this,
    );
  }
```
- As shown in the code above, we instantiated the controller class by passing two parameters, namely,
- `duration`: This is the total length of time this animation should last.
- `vsync`:  A `TickerProvider` is required. As a result, we must employ `SingleTickerProviderMixin`. The value this in this case means nothing but refers to the class's current `context`. 
- Offscreen animations are prevented from spending unnecessary resources thanks to the presence of `vsync`.
> Remember to dispose of the `_controller` in the `dispose()` method. Because it eliminates memory leaks by disposing of the `AnimationController` when it is no longer required.
- 
```
@override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
```
- Now to use this `_controller` let's first design a simple UI.
%[https://gist.github.com/red-star25/7e5708e4d72cf70964e0b796900d0537]
- 
![animationControllerUI.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1632666405695/xbPvrTaJY.png)
- As you can see it's a simple UI with two images defined in the Stack widget. The first one is the basketball area and the second one is the basketball, which we are going to animate.
- Now to move the basketball from top to bottom and bottom to top we need to update the `y` offset of the ball. So let's give the `_controller` value to the Offset `y`.
%[https://gist.github.com/red-star25/3937866ac53396e52f7eef6fae2107ba]
- Still, there will be no change in the UI. It's because we didn't tell the `_controller` when to start the animation.
- To update the UI when the `_controller` value changes, We first need to listen to that update. For that, `_controller` has one method `addListener` which as the name suggests listens to the controller values when it changes.
- Let's call that method in the `initState` : 
- 
```
  @override
  void initState() {
    super.initState();
    // .....
    _controller.addListener(() {
      setState(() {});
    });
  }
```
- The `setState` is used to update the UI when `_controller` values changes.
- Now to run the animation  `AnimationController` provides many methods :
- `forward`: The animation will go from `lowerBound` to `upperBound`.
- `reverse`: The animation will go from `upperBound` to `lowerBound`.
-  `repeat`: The animation will repeat itself from `lowerBound` to `upperBound` and from `upperBound` to `loweBound`.
- `stop`: The animation will stop running.
- `reset`: The animation will go to the initial condition.
- In our case, we want to make our ball bounce. To do that we need to call `repeat` method. So let's call it in the `initState`.
- 
```
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(milliseconds: 500),
      vsync: this,
      upperBound: 650.0,
      lowerBound: 400.0,
    );
    _controller.addListener(() {
      setState(() {});
    });
    _controller.repeat(reverse: true);
  }
```
- And Voila!!!
![animationControllerBouncing.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632668533977/PoYyOUthw.gif)

-------
## Wrapping Up
- The above animation appears strange because it lacks a smooth bouncing effect. In the next post, we'll look at how to use the Animation class to give the above animation a smooth bouncing motion.
- **Thank you for taking the time to read this. If you find it beneficial, please share it with others**.
- **See you in the upcoming article. Until then...**
- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632737344988/DowPMWcqI.gif)
