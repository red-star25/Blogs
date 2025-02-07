---
title: "Animation In Flutter: AnimatedCrossFade"
datePublished: Sun Sep 26 2021 05:02:15 GMT+0000 (Coordinated Universal Time)
cuid: cku0r9b8o0c54wqs1bthb7a9l
slug: animation-in-flutter-animatedcrossfade
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1632470909433/_P-5LLLi2.png
tags: programming-blogs, dart, flutter, flutter-examples, flutter-widgets

---

## AnimatedCrossFade
- Consider a scenario, where you want to replace a current widget with a new widget. 
- For example, you have an app where there are different types of posts. And you want to blur/just place a widget on top of that post saying "This post is sensitive". Just Like **Instagram**
- Let's make something like this in our Flutter App
- 
![noCrossFade.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632475161791/uZ8_is4MM.gif)
- As you can see It's working fine. But the problem is the visibility of the original post when we click on the `Show Me` button is very quick. It's not smooth.
- So to do a fade animation when we replace our Spoiler Alert widget with the original post widget, we can use the **AnimatedCrossFade** widget.

-------
## Using AnimatedCrossFade

- First Lets define the `AnimatedCrossFade` widget in the `body`
- 
```
Scaffold(
      backgroundColor: Colors.blueGrey,
      appBar: AppBar(
        title: const Text("AnimatedCrossFade"),
      ),
      body: Center(
        child: AnimatedCrossFade(
             // ....
        )
    )
```
- **AnimatedCrossFade** takes two `children` widgets that as you might have guessed, `firstChild` and `secondChild`.
- So let's give the `Spoiler Alert` widget to the `firstChild` property because it's the first child we're showing to the user.
- 
```
AnimatedCrossFade(
         firstChild: GestureDetector(
         onTap: () {
           setState(() {
               isVisible = true;
             });
          },
         child: Container(
            width: 300,
            height: 400,
            color: Colors.black,
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                const Text(
                  "Spoiler Alert",
                  style: TextStyle(fontSize: 18, color: Colors.white),
                ),
                const SizedBox(
                  height: 20,
                ),
                OutlinedButton(
                    onPressed: () {
                      setState(() {
                        isVisible = true;
                      });
                    },
                    child: const Text("Show me"))
              ],
            ),
          ),
        ),
       )
    )
```
- And now, also give the original post widget to the `secondChild` property.
- 
```
secondChild: GestureDetector(
          onTap: () {
            setState(() {
              isVisible = false;
            });
          },
          child: Container(
              width: 300,
              height: 400,
              color: Colors.blueGrey,
              child: Image.network(
                  "https://memegenerator.net/img/instances/60138700.jpg")
          ),
),
```
- Still, it will not do anything. We have two more `required` properties i.e -
### `duration`
- You also have to provide the `duration` to the `AnimatedCrossFade` widget. Which is used to define for how long the animation will fade from first to a second child.
- Let's put `1` second 
- 
```
AnimatedCrossFade(
   duration: const Duration(seconds: 1),
   firstChild : //...
   secondChild: //....
)
```
### `crossFadeState`
- The last `required` property is `crossFadeState`. It is as you might have guessed, the `state`, which determines whether to show `firstChild` or `secondChild`

- If it is`CrossFadeState.showFirst` then, when the animation completes the `firstChild` will be shown and vice versa
- The child that is shown will fade in, while the other will fade out.
- Now let's conditionally render our two children. For that let's first define a `boolean`.
- 
```
  bool showPost = false;
```
- And in the `crossFadeState` property add the below code :
- 
```
crossFadeState:
            !showPost ? CrossFadeState.showFirst : CrossFadeState.showSecond,
```
- And **THAT'S IT !!**
------------
## Final Output 
- 
![withAnimationCrossFade.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632476751282/u-4a_NS4H.gif)
## Final Code
%[https://gist.github.com/red-star25/676b0b1ef7622898fe26eb253a79484f]

------------
## `layoutBuilder` : 
- To understand why this property is needed, Let's change the `width` and `height` of the Post Image.
- 
```
        secondChild: GestureDetector(
          onTap: () {
            setState(() {
              showPost = false;
            });
          },
          child: Container(
              width: 200,   // <- here
              height: 300,  // <- here
              color: Colors.blueGrey,
              child: Image.network(
                  "https://memegenerator.net/img/instances/60138700.jpg"
                    ),
              ),
        ),
```
- Now if you run the app, you'll see a weird jump when we go from the `firstChild` state to `secondChild` state.
- 
![crossFadeWithLayoutBuilder.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632574098448/XlrB9EHjUV.gif)
- To fix these types of issues where both the widget have different `height` and `width`. We have to use `layoutbuilder` of the **AnimatedCrossFade ** widget.
- This has `4` parameters i.e :
- `topChild`, `topChildKey`, `bottomChild`, `bottomChildKey`. 
- This `layoutbuilder` will return a `Stack` widget with two `Positioned` widgets. The first Positioned widget will take the `bottomChild` widget and the second Positioned widget takes the `topChild` widget.
- Also don't forget to add `alignment` **center** and `clipBehaviour` to **Clip.none**. Otherwise, you'll not get the expected result. 
- 
```
AnimatedCrossFade(
            layoutBuilder:
                    (topChild, topChildKey, bottomChild, bottomChildKey) =>
                        Stack(
                  clipBehavior: Clip.none, 
                  alignment: Alignment.center,
                  children: [
                    Positioned(
                      key: bottomChildKey,
                      child: bottomChild,
                      top: 0.0,
                    ),
                    Positioned(
                      key: topChildKey,
                      child: topChild,
                    ),
                  ],
                ),
     //....
)
```
- **OUTPUT** :
- 
![crossFadeWithLayoutBuilder2.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632574864405/S3XRObMJF.gif)
- **SEE!!**
![SmoothCoreyVidalGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632574921443/yzQid67W9.gif)

----------

- **Thank you for reading. If you found this article useful then, don't forget to share it with others 🙂.**
- **Feedback and comments are welcomed ✍️**
- **See you in the next article. Till then...**
- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632575059653/bHQItG2E8.gif)
