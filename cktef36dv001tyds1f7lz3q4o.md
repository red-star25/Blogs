---
title: "Slivers in Flutter - Part (1)"
datePublished: Fri Sep 10 2021 13:50:38 GMT+0000 (Coordinated Universal Time)
cuid: cktef36dv001tyds1f7lz3q4o
slug: slivers-in-flutter-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1631422823311/RwtT3Q61uB.gif
tags: programming-blogs, dart, flutter, flutter-examples, flutter-widgets

---

## Sliver
- `Slivers` are basically a **scrollable area**, that can be customized. Slivers help us to make the scrolling fancier instead of a normal boring scroll.
- `Slivers` are useful for placing multiple scrollable widgets (**ListView**, **GridView**) inside it. It means we can handle nested scroll view. Like below -
- 
![nested_scroll_view.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631198760034/H7FTAnRJf.gif)
- In-fact, scrollable widgets like `ListView`, `GridView`, `SingleChildScrollView`, etc are implementing `slivers` under the hood. 
-------
## CustomScrollView
- If you want to use different `Slivers`, you need a special widget called **CustomScrollView**. All the `slivers` are placed inside it.
- `CustomScrollView` is the Widget that allows different types of scrollable widgets and lists. And these scrollable lists and widgets are called `slivers`.
- There are several types of `slivers` available. For example - `SliverAppBar`, `SliverGridList`, and `SliverList`, etc.
> One thing to note here is **CustomScrollView ** only takes **Slivers Widgets** as a child. Normal widgets like `Container`, `ListTile`, etc will not work.
- Example : 
- 
```
Scaffold(
  body: CustomScrollView(
    slivers: [
        SliverAppBar(/**/), 
        SliverGridList(/**/),
        SliverList(/**/),
        //......
      ]
    ),
);
```
- The `CustomScrollView` has many properties and one of them is `slivers`. Which takes list `slivers` as an input.
- Let's first understand different `slivers` one by one with an example. And then we can define those `slivers` inside the `CustomScrollView`.

------

## SliverList
- The `SliverList` is a widget that takes lists of items as child, same as `ListView` and `GridView`.
- This is useful, If you have a `ListView` and `GridView` and you want to scroll it together. Like below - 
- 
![list_grid_scroll.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631205233619/QkiPAX4Tx.gif)
- `SliverList`, has one parameter called `delegate`. There are two types of `delegate` - 
- **SliverChildListDelegate**: Takes a list of widgets that we want to display. Widgets defined in this list will be rendered at once. There will not be any lazy loading.
- **SliverChildBuilderDelegate**: Take a list of widgets that will be created lazily. It means as the user scrolls items get rendered.
- 
```
Scaffold(
      body: CustomScrollView(
      slivers: [
        SliverList(
          delegate: SliverChildBuilderDelegate(
            (context, index) {
              return Container(
                height: 50,
                alignment: Alignment.center,
                color: index.isEven ? Colors.grey : Colors.amberAccent,
                child: Text('List item :  $index'),
              );
            },
            childCount: 12,
          ),
        ),
      ],
));
```
-------
## SliverAppBar
- This is the same as the `AppBar` widget, the difference is that it works with `CutomScrollView`. 
- It means it has all the properties like - `title`, `actions`, `leading`, `flexibleSpace` etc.
- But it has some additional parameters like `pinned`, `floating`, `snap`, `expandedHeight` which customizes the behavior of the AppBar. Let's see how these properties affect the scroll behavior, in the below example.
- Creating `SliverAppBar` with `title` and `action`
```
Scaffold(
      body: CustomScrollView(
      slivers: [
        SliverAppBar(
          title: Text('Hello Sliver'),
          actions: <Widget>[
            IconButton(
              icon: const Icon(Icons.settings),
              onPressed: () {/* ... */},
            ),
          ],
        )
      ],
   )
);
```
- Output:
- 
![sliver_app_bar.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631203790055/znAhkAYB8.png)
- As you can see this looks like a traditional material app AppBar.
- Let's understand the different properties of `SliverAppBar`:
### `expandedHeight`:
- This defines the size of the `AppBar` when fully expanded.
- Example:
- 
```
SliverAppBar(
          expandedHeight: 200,
          title: Text('Hello Sliver'), 
          actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.settings),
            onPressed: () {/* ... */},
          ),
]),
```
- The height will get shrink as the user scrolls down, like below -
- 
![list_grid_scroll.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631206523914/-ghobzJc5.gif)
- But if you see, The **AppBar** hides when the user scrolls down. Let's pin the AppBar. 

### `pinnned`:
- This will determine, whether the **AppBar** remains visible on the screen when the user scrolls down or not.
- If `true`: AppBar will not hide on scroll
- 
```
SliverAppBar(
          expandedHeight: 200,
          pinned: true,
          title: Text('Hello Sliver'), 
          actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.settings),
            onPressed: () {/* ... */},
          ),
]),
```
- 
![pinned_example.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631206979632/7Ue6Cq2SR.gif)

## `floating`:
- If `true`, then the **AppBar** will get visible as soon as the user scrolls towards the **AppBar**.
- If `false` then the user has to scroll all the way to the top in order to access **AppBar**
- 
```
SliverAppBar(
          expandedHeight: 200,
          floating:true
          title: Text('Hello Sliver'), 
          actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.settings),
            onPressed: () {/* ... */},
          ),
]),
```
- 
![floating_true.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631208231507/DAwPjIX0-.gif)


### `snap`:
- If `true`, Then the whole AppBar will be visible whenever a user tries to scroll toward the AppBar. 
- The `floating` value must have `true` in order to run `snap`.
```
SliverAppBar(
          expandedHeight: 200,
          floating:true,
          snap: true,
          title: Text('Hello Sliver'), 
          actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.settings),
            onPressed: () {/* ... */},
          ),
]),
```
- 
![snap_true.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631208511965/Gt1QbUj-4.gif)
- Difference between `snap` and `floating` is, `snap` shows the AppBar at once, whereas the `floating` shows AppBar as the user scrolls up.
- 
![floating_snap_difference.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631208966752/gzUMbRVNk.gif)

> You can try different combinations of `floating`, `pinned`, and `snap` to get various results.

### `flexibleSpace`
- It is used to give a `background` and various `collapseModes` to the AppBar.
- There is `title` property also. It is placed at the bottom. When the user scrolls up, it will transform its position with the transition.
- For example - 
- 
```
SliverAppBar(
           flexibleSpace: FlexibleSpaceBar(
                      title: Text("Welcome to Space"),
                      background: Image.network("url",fit: BoxFit.cover),
           ),
          expandedHeight: 200,
          pinned: true,
          actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.settings),
            onPressed: () {/* ... */},
          ),
]),
```
- 
![flexible.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631269353246/-uRsajLu0.gif)
- Isn't it looking awesome? When we scroll up we are getting **parallax** effect. And it's because of the `collapseMode` property.
- The `collapseMode` has 3 mode - **parallax**, **pin**, **none**
- If you put **CollapseMode.pin** then you will not get a parallax effect of the image. The image will simply change it's a position with AppBar and fades out, like below - 
- 
```
SliverAppBar(
           flexibleSpace: FlexibleSpaceBar(
                      collapseMode: CollapseMode.pin,
                      title: Text("Welcome to Space"),
                      background: Image.network("url",fit: BoxFit.cover),
           ),
          expandedHeight: 200,
          pinned: true,
          actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.settings),
            onPressed: () {/* ... */},
          ),
]),
```
- 
![collapsemode_pin.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631269982069/RINaHWr-s.gif)

### `stretch`
- Default value is `false`.
- If you scroll down when you're at the top then you will see the empty space, like below -
- 
![stretch_false.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631270839469/SWO6bnj1L.gif)
- To fill the overflowing space when the user scrolls down, give `stretch` a value `true`.
- 
```
SliverAppBar(
           stretch: true,
           flexibleSpace: FlexibleSpaceBar(
                      collapseMode: CollapseMode.pin,
                      title: Text("Welcome to Space"),
                      background: Image.network("url",fit: BoxFit.cover),
           ),
          expandedHeight: 200,
          pinned: true,
          actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.settings),
            onPressed: () {/* ... */},
          ),
]),
```
- 
![stretch.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631271308016/iEJwwzQ5s.gif)
- You can also trigger a function when the user stretches by implementing  `onStretchTrigger` function of `SliverAppBar`.
> Note: You have to provide `scrollBehavior` to the `MaterialApp` for the `bouncing` scrolling effect.

### `stretchModes`
- If you want to `blur`, or `fade` the image on the overflowing scroll instead of `zooming`, then you can provide different `stretchModes` inside the `FlexibleSpaceBar`.
- It has 3 main modes - **blurBackground**, **fadeTitle ** and **zoomBackground (default)**
- Let's try the remaining 2 modes :
- 
```
SliverAppBar(
           stretch: true,
           flexibleSpace: FlexibleSpaceBar(
                      collapseMode: CollapseMode.pin,
                      title: Text("Welcome to Space"),
                      background: Image.network("url",fit: BoxFit.cover),
                      stretchModes: [
                          StretchMode.fadeTitle,  // fades out the title 
                          StretchMode.blurBackground, // blur out the background
                          StretchMode.zoomBackground // zoom the background
                  ],
           ),
          expandedHeight: 200,
          pinned: true,
          actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.settings),
            onPressed: () {/* ... */},
          ),
]),
``` 
- 
![stretchMode.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631272083107/dGyEMBWK_.gif)

------------
## Wrapping Up
- This is the** Part - 1** of **Advance Scrolling in Flutter**.
- In **Part-2** we will see different types of **Sliver** and how to use them.
- If you liked this article, **share it** with your developer friends and communities.
- **Comments **and **Feedback **are welcomed 😃
- See you in the next article. Until then.....
- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631281752796/smRTyQUmy.gif)
