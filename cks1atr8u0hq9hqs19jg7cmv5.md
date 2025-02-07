---
title: "Flutter Widget In Detail : AbsorbPointer & IgnorePointer"
datePublished: Sat Aug 07 2021 04:50:37 GMT+0000 (Coordinated Universal Time)
cuid: cks1atr8u0hq9hqs19jg7cmv5
slug: flutter-widget-in-detail-absorbpointer-and-ignorepointer
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1628311803957/aVaUOKs1L.gif
tags: flutter-sdk, flutter-widgets

---

## Introduction :
- Have you ever been in a situation in your app where there are multiple buttons, listview, list tiles, cards, containers, etc, and you want to stop interaction/touches from the user from all of those widgets at once?
- Of course, you can pass `null` to the buttons `onPressed` property. But when there are too many buttons in your row/column or any other widget, it is very frustrating to pass this property one by one.
- Consider the below example where there are 5 buttons inside `Column`. Now we want to disable all the buttons for some reason. For that, the common way is to go and write `null` to every button's `onPressed` property. 
```
Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        ElevatedButton(child:Text("1"),onPressed:null),
        SizedBox(height:5.0),
        ElevatedButton(child:Text("2"),onPressed:null),
        SizedBox(height:5.0),
        ElevatedButton(child:Text("3"),onPressed:null),
        SizedBox(height:5.0),
        ElevatedButton(child:Text("4"),onPressed:null),
        SizedBox(height:5.0),
        ElevatedButton(child:Text("5"),onPressed:null),
      ]
)
```
- Isn't it a very boring way to do this? Yes **IT IS**. And what if we want to disable all the interactions from our app at once 😧? 
- ![WorriedKermitGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628183221866/OGkebME6b.gif)
- So what's the solution to this problem? 🤔
- Well Flutter provided two very useful widgets to solve this problem. The solution is to wrap your widget inside **AbsorbPointer / IgnorePointer**. 
- 
![KermitFrogGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628183263282/bab-Ht3cu.gif)
- You can disable the user's whole app interaction by simply wrapping your main widget from the widget tree inside the AbsorbPointer.
- Let's see both the widget one by one and understand what they are doing and what is the difference between them. 

-------------------

## AbsorbPointer :
- As the name screaming, AbsorbPointer absorbs the click event. In other words, It prevents click events from the child widget.
- Not only it prevents `click` events, but it also prevents `scroll`, `drag`, `hover` events.
- #### Properties : 
- `absorbing`: When `true`, The widget prevents its subtree from receiving all kinds of events. When `false`, The widget will allow its subtree to receive the events.
- `child`: Pass widget/widgets from which you want to disable events.
- `ignoringSemantics`: This takes boolean as a parameter. `true` means widget should be ignored by screen readers when compiling the semantic tree.
- Example :
```
Stack(
      alignment: AlignmentDirectional.center,
      children: <Widget>[
        SizedBox(
          width: 200.0,
          height: 100.0,
          child: ElevatedButton(
            onPressed: () {},
            child: null,
          ),
        ),
        SizedBox(
          width: 100.0,
          height: 200.0,
          child: AbsorbPointer(
            absorbing: true,
            child: ElevatedButton(
              style: ElevatedButton.styleFrom(
                primary: Colors.red.shade200,
              ),
              onPressed: () {},
              child: null,
            ),
          ),
        ),
      ],
    );
```
- 
Output :
- ![absorb.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628228845370/wgmw9xT6d.gif)
- Here we can clearly see that the red Box is completely disabled. If you observe the `onPressed` property of the red button, it is not null, but still, it is not receiving any kind of event because we've wrapped our button inside the **AbsorbPointer** 
- This is a very small example. But imagine if have too many widgets on your screen like below,
- 
![manywidget.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628228920916/DhX8sX80y.png)
- Then **AbsorbPointer** is the right and best way to disable everything at once.


## IgnorePointer :
- As the name screaming, IgnorePointer ignores/prevents their children's widget from pointer-events as well as the whole widget tree interaction.
- Like **AbsorbPointer**, **IgnorePointer** can ignore pointer-events like tapping, dragging, scrolling, and hover.
- #### Properties : 
- `ignoring`: If `true` it will ignore the pointer event.
- `child`: Pass widget/widgets from which you want to disable events.
- `ignoringSemantics`: If `true` the widget will be ignored when compiling the semantics tree. And will be ignored by the screen readers
- Example :
```
Center(
        child: IgnorePointer(
          ignoring: ignoring,
          child: Column(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: <Widget>[
              Text('Ignoring: $ignoring'),
              ElevatedButton(
                onPressed: () {},
                child: const Text('Click me!'),
              ),
            ],
          ),
        ),
      ),
```
- Output :

![ignore.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628189042747/HSahb-GyN.gif)
- As you can see that when we change the value of the `ignoring` from `false` to `true` , the button is no longer clickable.
 
-----------------------

- Hh 🤔 !! So what's the difference between **AbsorbPointer** and **IgnorePointer**? Both are doing the same thing right !!  But **NO** there are some differences. Let's see.
- So let's understand the core difference between both of them by taking an example.

## Difference Between AbsorbPointer and IgnorePointer :

#### Example - 1 :

- Consider two boxes `red` box and the `blue` box. The red box is on top of the blue box.

```
 Stack(
      alignment: Alignment.topCenter,
      children: [
               BlueBox(
                      onClicked: () {print("Blue box clicked")}.
                      child: Container(width: 200, height: 150),
                      color: Colors.blue,
               ),
               RedBox(
                      onClicked: () {print("Red box clicked")}.
                      child: Container(width: 100, height: 100),
                      color: Colors.red,
               ),
        ]
)
```
- All is working as aspected. Both buttons are working with their individual `onClicked` property.

![simpleclick.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628190612580/ZaX5lvB7v.gif)

- Now we are going to wrap the `red` box inside the `IgnorePointer`. Let's see what happens
- ```
       IgnorePointer(
          child: RaisedButton(
                    onPressed: (){print("Red box clicked")},
                    child:Container(
                    child: Container(width: 100, height: 100),
                    color: Colors.red,
               ),
            )
          )
```
- Output :
![afterIgnore.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628190728965/wBDc4mDpS.gif)

- As we can observe that now the `red` box is not clickable anymore. Even if we click on  the `red` box the `blue` box will be clicked.

- Now let's wrap the same `red` box with the **AbsorbPointer** and see what happens.
- 
```
       AbsorbPointer(
          child: RaisedButton(
                    onPressed: (){print("Red box clicked")},
                    child:Container(
                    child: Container(width: 100, height: 100),
                    color: Colors.red,
               ),
            )
          )
```
- 
![afterabsorbclick.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628191031123/45W3kynrm.gif)

- Now you can see that the `red` box is not even showing that click event/hand cursor.
- So basically **AbsorbPointer** is ignoring the interaction of the child widget by also ignoring the widget below it, which here is some part of the `blue` box below the `red` box.
- **IgnorePointer** is also ignoring the interaction of the child widget. But it will not ignore the widget below it. 

- > **Simply put**, In **AbsorbPointer** what is happening is that The `red` box contains some part of the `blue` box below it, that's why it is also absorbing/ignoring that part and disable it.
- > But **IgnorePointer** will not absorb/ignore that below part and it will make the whole box clickable by not considering the `red` box click event


#### Example - 2 :
- Consider a Button. which is also wrapped inside `GestureDetector` widget.
```
  GestureDetector(
           onTap: (){
              print("Gesture Detector");
            },
           child:ElevatedButton(
           style: ElevatedButton.styleFrom(primary: Colors.transparent),
           onPressed: (){
                 print("Red Button Pressed");
           },
          child:Container(width: 100, height: 100,color:Colors.red),
     )
)
```
- ![ex2simpleclick.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628228300398/aa9A1-AAk.gif)
- When you click on this box, it will print `Red Button Pressed` as expected. Notice that it will not call the `onTap` function of the `GestureDetector` widget.
- Now let's wrap the `ElevatedButton` inside our `IgnorePointer`.
```
GestureDetector(
            onTap: (){
              print("Gesture Detector");
            },
            child: IgnorePointer(
                 child: ElevatedButton(
                 style: ElevatedButton.styleFrom(primary: Colors.transparent),
                 onPressed: (){
                       print("Red Button Pressed");
                   },
                 child:Container(width: 100, height: 100,color:Colors.red),
                 )
         )
)
```
- Now what do you think .... what will happen if we click on the red box again 🤔??
- Will it print the statement of `GestureDetector` or `ElevatedButton` ??
- **It will not print any of the statements!!!**. Why ?? Because as we've discussed above that `IgnorePointer` will ignore its child as well as **its whole widget tree.**. It means it will also ignore the `GestureDetector` because it is also a part of the `IgnorePointer`s widget tree.
- ![ex2ignore.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628228071787/f4iGltj6O.gif)

- Now let's wrap our button inside **AbsrobPointer**.
```
GestureDetector(
            onTap: (){
              print("Gesture Detector");
            },
            child: AbsorbPointer(
                 child: ElevatedButton(
                 style: ElevatedButton.styleFrom(primary: Colors.transparent),
                 onPressed: (){
                       print("Red Button Pressed");
                   },
                 child:Container(width: 100, height: 100,color:Colors.red),
                 )
         )
)
```
- ![ex2aborv.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628227932924/tKIgvP4i4.gif)
- As we can see the event of our `ElevatedButton` is ignored but the `onTap` of the `GestureDetector` is working. Because the `AbsorbPointer` will only absorb the child of it. Not the whole widget tree.
----------------------

- That's **IT**. That's all you need to about **AbsorbPointer** and **IgnorePointer**. Hope you understood. 😊

 > Previous Blog : Widget In Detail - [Container](https://dhruv25.hashnode.dev/widgets-in-detail-container) 