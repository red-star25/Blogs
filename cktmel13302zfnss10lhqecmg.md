---
title: "Slivers in Flutter - Part (4)"
datePublished: Thu Sep 16 2021 03:58:41 GMT+0000 (Coordinated Universal Time)
cuid: cktmel13302zfnss10lhqecmg
slug: slivers-in-flutter-part-4
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1631764842542/U_5BHGQko.gif
tags: programming-blogs, flutter, flutter-examples, flutter-widgets

---

- This is Part - 4 of **Slivers in Flutter** series. Make sure you check the first 3 parts.
- In this article, I'm going to explain some of the useful `Sliver` widgets, which are -
**SliverOpacity**, 
**SliverAnimatedOpacity**, 
**SliverFadeTransition**, 
**SliverVisibility**, 
**SliverIgnorePointer**, 
**SliverSafeArea**.
--------

## SliverOpacity
- The `SliverOpacity` makes `sliver` widget transparent.
- This works the same as the `Opacity` widget works for `Box` widgets. The difference is this only works on the `Sliver` widgets.
- It usually takes values between `0.0` to `1.0`.
- For the value 0.0, the sliver child is simply not painted at all. For the value 1.0, the sliver child is painted immediately.
- For values of `opacity` other than `0.0` and `1.0`, this class is relatively expensive because it requires painting the sliver child into an intermediate buffer.
- Example :
- 
%[https://gist.github.com/red-star25/5f6abc853c457ca6f1593d1d597c36d8]
- **Output**
- 
![sliveropacity.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631511628358/ZbW7ULEPM.gif)

--------

## SliverAnimatedOpacity
- If you see in the output of the above example, The opacity is directly jumping from `no visibility` to `full visiblity`. It's not looking smooth.
- To do the smooth transition between `0.0` to `1.0` values we have to use `SliverAnimatedOpacity`.
- `SliverAnimatedOpacity` is an animated version of `SliverOpacity` which automatically transitions the sliver child's opacity over a given `duration` whenever the given opacity changes.
- **Example**
%[https://gist.github.com/red-star25/7f3f61a4964155b33c5b347b90458639]
**Output**
- 
![sliveranimatedopacity.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631512086597/p6bv2qi12.gif)

--------

## SliverFadeTransition
- This also animates the `opacity` of the `sliver` widget. The only difference is it takes `Animation<double>` value instead of `double` values.
- **Example**
%[https://gist.github.com/red-star25/d9b9c4dd269075872fde30d3410da965]
**Output** :
- 
![sliverfadetransition.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631512944811/2skdCOpjw.gif)
- Here I've used `Curves.fastOutSlowIn` animation. You can use any one of the curves defined in the below class:
%[https://api.flutter.dev/flutter/animation/Curves-class.html]

-------

## SliverVisibility
- `SliverVisibility` is the same as the `Visibility` widget except it takes `sliver` as a child.
- It is used to show or hide a sliver child. When the `sliver` is not visible the `replacementSliver` is included instead.
- `replacementSliver` is used when the `sliver` child is not visible, assuming that none of the `maintain` flags (in particular, `maintainState`) are set.
- `SliverVisibility` has different parameters like :
- **maintainAnimation** : It is used to determine whether to maintain `animations` within the sliver subtree when it is not visible.
- **maintainInteractivity**: It is used to determine whether to allow the sliver to be interactive when hidden.
- **maintainSemantics**:  It is used to determine whether to maintain the semantics for the sliver when it is hidden (e.g. for accessibility).
- **maintainSize**: It is used to determine whether to maintain space for where the sliver would have been.
- **maintainState**: It is used to determine whether to maintain the State objects of the sliver subtree when it is not visible.
- **replacementSliver**: Widget defined here is visible when sliver is not visible.
- **Example**:
%[https://gist.github.com/red-star25/7219bf7c97da7957f4642bd3f7d9e334]
**Output**:
- 
![slivervisibility.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631514339144/42zPjzM5r.gif)

--------

## SliverIgnorePointer
- When you want your sliver to ignore the tapping or any kind of interaction then simply wrap your `sliver` widget inside `SliverIgnorePointer`.
- It will disable the interaction of that widget.
- When `ignoring` property is `true`, the widget is not interactable. And when `ignoringSemantics` property is true, the subtree will be invisible to the semantics layer
- **Example**:
%[https://gist.github.com/red-star25/182a2aba682c2760f5146c403430f67c]
**Output**:
- 
![sliverignorepointer.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631514897990/D-V7AgMl-.gif)

---------

## SliverSafeArea
- If you've used `SafeArea` then, `SliverSafeArea` is also doing the same thing except it takes `sliver` as a child instead of `Box` widget.
- For example, this will indent the sliver by enough to avoid the status bar at the top of the screen.
- It will also indent the sliver by the amount necessary to avoid The Notch on the iPhone X or other similar creative physical features of the display.
%[https://gist.github.com/red-star25/7351745653b8d15d220360fec4337c84]
**Output**:
- 
![sliversafeareafinal.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631516566947/hTuaihDUV.gif)

-------
### Wrapping Up
- **This is the 4th part of the `Slivers In Flutter` series. Check previous articles for more information about Slivers.**
- **If you liked this article make sure to give a thumbs up 👍. Also share it with others if you found this helpful💙.**
- **See you in the next article. Until then..**
- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631430762292/EYsL_9AXK.gif)