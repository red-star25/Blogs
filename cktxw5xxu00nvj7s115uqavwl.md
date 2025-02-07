---
title: "Animation In Flutter : AnimatedAlign"
datePublished: Fri Sep 24 2021 04:56:18 GMT+0000 (Coordinated Universal Time)
cuid: cktxw5xxu00nvj7s115uqavwl
slug: animation-in-flutter-animatedalign
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1632388251720/6qMVg6y5L.png
tags: programming-blogs, dart, flutter, flutter-examples, flutter-widgets

---

- As a developer, animation becomes an important part of your app development workflow. To make your app memorable, you might want to create cool animations in your application.
- **Animation **makes a huge difference in user engagement. It is a powerful tool for grabbing user's attention and making the app's UI more friendly to use.
- **Animation ** is the process of creating a visual illusion of motion, with the help of elements such as images or videos. It is such a wonderful technique that allows you to convey your message with emotion and feeling. 
- **Animation ** is one of the integral parts that make **Flutter ** such a powerful framework. It helps us to create apps that not only look fantastic but **feel natural** and **seamless ** as well.
- In this series, I'm going to explain different in-built animation widgets like AnimatedAlign, AnimatedContainer, AnimatedOpacity, AnimatedWidget, AnimatedModalBarrier, etc.
- In this article, I've explained the **AnimatedAlign** widget. Which is used to animate the position.
- 
![Let'SGetStartedGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632379369422/pkFrmK6Bxr.gif)
---------
## AnimatedAlign
- This is an animated version of the **Align** widget.
- With this, you can animate the position of your widget in a given amount of duration.
- You can animate through different alignments like left-right, top-bottom, center-left, etc.
- To animate any widget's alignment simply wrap that widget inside the **AnimatedAlign** widget.
- 
```
AnimatedAlign(
   child: Container(...)
)
```
- After that provide the `starting` alignment and `ending` alignment to the `alignment` property of the `AnimatedWidget`.
- 
```
AnimatedAlign(
   alignment: animatePosition ? resultAlignment : currentAlignment,
   child: Container(...)
)
```
- Now give the `duration` to the `duration` property, which determines for how long the animation should run.
- 
```
AnimatedAlign(
   alignment: alignment: animatePosition ? resultAlignment : currentAlignment,
   duration: const Duration(seconds: 1),
   child: Container(...)
)
```
- You can also provide different curves to get different animation behavior.
- 
```
AnimatedAlign(
   alignment: alignment: animatePosition ? resultAlignment : currentAlignment,
   duration: const Duration(seconds: 1),
   curve: Curves.fastOutSlowIn,
   child: Container(...)
)
```
- And **That's it!!**. In the below example I've covered all the possible alignments.
%[https://gist.github.com/red-star25/27bf71cfe9df54b37e4420a64daa34a2]
- 
![animatedAlign.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632386299781/IeuuhwppF.gif)
- In the above example, I've taken one **boolean** named `animatePosition`, which is used to notify the **AnimatedAlign ** widget that the user has clicked on the button to animate the position of the widget, So animate that widget's position from `currentPosition` to `resultantPosition`.
- You can do more fun stuff with this, For example, you can use **GestureDetector** and then use the swipe gestures to move the box position towards the swiped direction. Like below,
%[https://gist.github.com/red-star25/f67bd4a8fcd7d21fe0bc999764ab0ac0]
- 
![animateGestureAlign.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632392526269/K225fKrwxk.gif)

- One more thing is, as you can see in the first example, **As soon as I trigger other animation while the previous animation is still running, the previous animation stopped and continue its animation with a new animation value. How cool is that !!!**
- This is all about **AnimatedAlign** widget. 
----------

- **Thank you for reading. If you learned something, then make sure to share this knowledge with others.**
- **Feedback and comments are welcomed ✍️**
- **See you in the next article. Till then...**
- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632389206199/tpmtqtW99.gif)
