---
title: "Animation In Flutter: AnimatedContainer"
datePublished: Mon Oct 04 2021 04:46:16 GMT+0000 (Coordinated Universal Time)
cuid: ckuc67k8i0c2g0gs1b4tu9bpt
slug: animation-in-flutter-animatedcontainer
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1633322483849/h9pQNsCS6.gif
tags: programming-blogs, dart, flutter, animation

---

- We've seen how to make Explicit animation with the `Animation` class, `Tween` animation, and `CurvedAnimation` in previous tutorials.
- We've also tweaked the bouncing effect in our bouncing ball example to make it look more realistic.
- **Previous Article Animation** : 
- 
![finalBouncingWithCurve.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1633097932321/b8u1SaD3b.gif)
- **AnimatedContainer** is another Implicit animated widget that we'll learn about in this tutorial.
- 
![LetsDiveRightIntoItNikNocturnalGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1633097381685/0rK3l0WJp.gif)

----------
## AnimatedContainer
- If I had to explain **AnimatedContainer ** in a single sentence, I would say:
> AnimatedContainer is an animated version of a traditional Container
- Using **AnimatedContainer**, we can animate almost every feature of the **Container** widget.
- Because AnimatedContainer is an implicit animation, no controller is required to control the animation.
- We can animate `height`, `width`, `color`, `border`, `borderRadius`, `shadow`, and so on.
- Let's pick up where we left off in the previous example. I am going to make just one change in that particular example, which is shown below : 
- 
%[https://gist.github.com/red-star25/9b02b81f1b226a0f1b13dfe7189528d9]
- As you can see I've added one `Container` below the `Ball` which is bouncing. And Also wrapped that container inside the `GestureDetector` which will be used to animate the container.
- The UI will look like below, If you run the app.
![animatedContainerUI.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1633099164844/qpU7F6rsa.png)
- Now to animate the container we first need to convert the `Container` to `AnimatedContainer`. So let's do that first :
- 
```
GestureDetector(
    onTap: () => {},
    child: AnimatedContainer(
      height: 20,
      width: 60,
      color: Colors.blueGrey,
   )
)
```
- The `AnimatedContainer` has one required property which is `duration`. It's nothing more than a timer that determines how long the animation will run for.
- Let's use 2 seconds as an example.
- 
```
GestureDetector(
    onTap: () => {},
    child: AnimatedContainer(
      duration: const Duration(seconds:2),
      height: 20,
      width: 60,
      color: Colors.blueGrey,
   )
)
```
- Now, to animate the properties of the **Container** we need to create some kind of notifier that tells the container when it should start the animation.
- You can directly start the animation when the page loads. But In this example, I'll trigger the animation by tapping into it. 
- Let's start by defining a `boolean`. Which is used to start an animation when the user taps it.
- 
```
  bool isAnimating = false;
```
- When the user taps inside the container, the value of the `isAnimating` variable will be changed.
- To accomplish so, we must update it in the `onTap` function of the `GestureDetector`.
- 
```
GestureDetector(
    onTap: () => {
        setState(() {
           isAnimating = !isAnimating;
        });
    },
    child: AnimatedContainer(
      duration: const Duration(seconds:2),
      height: 20,
      width: 60,
      color: Colors.blueGrey,
   )
)
```
- Now it's time to animate the **Container**.
- 
![UpThumbsUpGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1633099897520/SR3X7zHOg.gif)

-------
## `width` and `height` Animation:
- Initially, the width and height of our Container are `60` and `20`. Let's change the width when the user taps the Container:
- 
```
GestureDetector(
    onTap: () => {
        setState(() {
           isAnimating = !isAnimating;
        });
    },
    child: AnimatedContainer(
      duration: const Duration(seconds:2),
      height: isAnimating ? 200 : 20,
      width: isAnimating
                        ? MediaQuery.of(context).size.width * .8
                        : 60,
      color: Colors.blueGrey,
         )
)
```
![widthandheightContainerAnimation.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1633100698325/8EI0t0-4g.gif)
- As you can see the AnimatedContainer is automatically changing and also animating the Container's `width` and `height` smoothly.
---------
## `color` Animation:
- 
```
AnimatedContainer(
      duration: const Duration(seconds:2),
      height: isAnimating ? 200 : 20,
      width: isAnimating
                        ? MediaQuery.of(context).size.width * .8
                        : 60,
      color: isAnimating ? Colors.deepOrange : Colors.blueGrey,
)
```
- 
![colorAnimationContainer.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1633101100747/77tMkqKtf.gif)

----------

## `border` and `borderRadius` Animation:
- 
```
AnimatedContainer(
      duration: const Duration(seconds:2),
      height: isAnimating ? 200 : 20,
      width: isAnimating
                        ? MediaQuery.of(context).size.width * .8
                        : 60,
      decoration: BoxDecoration(
             color: isAnimating ? Colors.deepOrange : Colors.blueGrey,
             borderRadius: isAnimating
                          ? const BorderRadius.only(
                              topLeft: Radius.circular(80),
                              topRight: Radius.circular(80),
                            )
                          : const BorderRadius.all(
                              Radius.circular(0),
                            ),
              border: Border.all(
                        color: isAnimating ? Colors.blue : Colors.teal,
                        width: isAnimating ? 10 : 2,
              ),
       ),
)
```
- **Make sure to move `color` in the `BoxDecoration`, otherwise, you'll get an error.**
- 
![animatedContainerborder-radius.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1633168059856/kD-tdEc9C.gif)

---------

## Adding `Curves`
- You can also tweak the animation's curves by adding them inside the `curve` properties.
- You will find different Curves [Here](https://api.flutter.dev/flutter/animation/Curves-class.html)
- 
```
AnimatedContainer(
      duration: const Duration(seconds:2),
      height: isAnimating ? 200 : 20,
      width: isAnimating
                        ? MediaQuery.of(context).size.width * .8
                        : 60,
      curve: isAnimating ? Curves.bounceIn : Curves.bounceOut,
      decoration: BoxDecoration(
             color: isAnimating ? Colors.deepOrange : Colors.blueGrey,
             borderRadius: isAnimating
                          ? const BorderRadius.only(
                              topLeft: Radius.circular(80),
                              topRight: Radius.circular(80),
                            )
                          : const BorderRadius.all(
                              Radius.circular(0),
                            ),
              border: Border.all(
                        color: isAnimating ? Colors.blue : Colors.teal,
                        width: isAnimating ? 10 : 2,
              ),
       ),
)
```
- 
![animatedContainerCurves.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1633168407672/0UpW3XnGl.gif)

---------
## `onEnd` Function
- If you want to do something when the animation completes. You can do that inside the `onEnd` function of the `AnimatedContainer`.
- 
```
AnimatedContainer(
     //....
    onEnd: () {
           setState(() {
               animationEnd = true;
           });
      },
),
```

---------
- You may animate any AnimatedContainer `child` in the same way as the other properties. 
- There are many additional properties that we can animate in the same way, such as alignment, transform, margin, and padding.

----------

## Final Words
- **Thank you for taking the time to read this article. If you found it useful, please share it with others. Also, if you have any suggestions, please leave them in the comments section.**
- **See you soon. Until then....**
- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1633169155604/EkRJELNjC.gif)
