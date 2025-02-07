---
title: "Keys In Flutter - UniqueKey, ValueKey, ObjectKey, PageStorageKey, GlobalKey"
datePublished: Tue Aug 17 2021 02:35:54 GMT+0000 (Coordinated Universal Time)
cuid: cksfgf0xf0vvzt2s11f113pse
slug: keys-in-flutter-uniquekey-valuekey-objectkey-pagestoragekey-globalkey
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1629014759103/LByoG3US0.png
tags: programming-blogs, dart, flutter, flutter-examples

---

## Introduction
- Flutter has many widgets in its library, and if you take a look at every widget's properties you'll most probably find the `key` parameter in all of those widgets.
- Most of the beginners who started learning Flutter don't know about `Keys`. And if they do, they don't know how to use them or where to put them.
- It's because `Keys` has very **few use cases** or you can say their use is **less common**.
- In this blog, I will try to explain the concept of `Keys`, and different types of `Keys`, Where to use `Keys`, and How to use them.
- 
![LetUsBeginLetsStartGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628783547945/I5PmC2SYw.gif)

------------------------------

## What is `Key`??
- If we take a look at the definition of `Keys` written in Flutter's Official Documentation,  It says :
> A Key is an identifier for Widgets, Elements, and SemanticsNodes.
- It simply means is Flutter basically identifies the widgets and where it is placed in widget tree by `Keys`. But it's more than that.
- `Keys` preserves the `state` when you move around the widget tree.
> If you find yourself adding, removing, or reordering a collection of widgets of the same type that hold some state, using keys is likely in your future.
- Let's take a look at different types of keys one by one.
-------------------------------

## UniqueKey :
- The `UniqueKey` in Flutter is used to identify every widget of your app uniquely.
- `UniqueKey` also preserves the state when widgets move around in your widget tree.
- `UniqueKey` can be used in cases like when you are reordering the widget in the list or adding or removing the widgets from a list.
- It is helpful when you have multiple widgets in your widget tree with the same values and same type and you want to identify each of them uniquely.
- It is also helpful when a unique id is not defined in your DB collection to identify all the list of items uniquely. You can use `UniqueKey` which will assign a unique key to that particular widget.
- Let's take one example 
- I'm going to create an emoji swapper program, where there are going to be two emojis displayed on the screen, and a button underneath them, which will swap the position of the emojis when triggered.
- 
```
class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}
```
- 
```
class _HomePageState extends State<HomePage> {
  List<Widget> emojis = [
    GetEmoji(emoji: "😎"),
    GetEmoji(emoji: "🤠")
  ];

  swapEmoji() {
    setState(() {
      emojis.insert(1, emojis.removeAt(0));
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        body: SizedBox.expand(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            crossAxisAlignment: CrossAxisAlignment.center,
            children: emojis,
          ),
          SizedBox(
            height: 20,
          ),
          ElevatedButton(
            onPressed: swapEmoji,
            child: Text("Swap"),
          )
        ],
      ),
    ));
  }
}
```
- 
```
class GetEmoji extends StatelessWidget {
  GetEmoji({required this.emoji});
  String emoji;
  @override
  Widget build(BuildContext context) {
    return Text(
      emoji,
      style: TextStyle(
        fontSize: 100,
      ),
    );
  }
}
```
- And as you can expect, the emojis will swap their position when we click the swap button
- 
![normalswapwithstateless.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628844648696/vV0FZbDsz.gif)

- But the problem will come if we try to convert the `Stateless` widget into `Stateful` widget and store the value in a `state`.
- Let's see what will happen if we convert it.
- 
```
class GetEmoji extends StatefulWidget {
  GetEmoji({required this.emg});
  String emg;
  @override
  _GetEmojiState createState() => _GetEmojiState();
}
```
- 
```
class _GetEmojiState extends State<GetEmoji> {
  late String emoji;
  @override
  void initState() {
    super.initState();
    emoji = widget.emg;
  }

  @override
  Widget build(BuildContext context) {
    return Text(
      emoji,
      style: TextStyle(
        fontSize: 100,
      ),
    );
  }
}
```
- 
![withstatefull.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628844933135/4V4SC_Qm6.gif)
- Now nothing is happening. The emojis are no longer changing their positions.
- 
![ConfusedWhitePersianGuardianGIF (2).gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628845077830/Zlyho1QkH.gif)
- It's because under the hood Flutter distinguishes widget by the `type` of the widget (`runtimeType`) and by the `keys`.
- We've two `Stateful` widgets in our list (one for 😎, and one for 🤠). when we swap the emojis positions, by pressing the `swap` button, flutter will then check in the `ElementTree` that, Is the `type` of the changed widget is the same as the `type` of the `ElementTree`'s element or not?.
- If you don't know about `ElementTree`, The `ElementTree` only holds the information about the type of each widget and a reference to children's elements. You can think of the ElementTree as a skeleton of your Flutter app. It shows the structure of your app.
- 

![1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628847947953/msbcUB9ms.png)
- After swapping it will check the runtime type.
- 
![2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628847957535/SEfMJpjKb.png)
- When I've swapped the order of the two widgets, Flutter walks the `ElementTree`, checks the type of the `RowWidget`, and updates the reference. After that, it checks if the type of `😎 Text Element` of the **ElementTree** is same as `🤠 Text Widget`'s `type`? **and it is**, so it updates the reference. And nothing will update.
- But..but If we name those two `Stateful` widgets differently. Then there will be no problem. Because both will then have different IDs/keys assigned.
- To update the widget which has the same type inside the list, we have to pass the `UniqueKey` to all the widget
- 
```
class GetEmoji extends StatefulWidget {
  GetEmoji({required this.emg, required Key key}) : super(key: key);
  String emg;
  @override
  _GetEmojiState createState() => _GetEmojiState();
}
```
- 
```
  List<Widget> emojis = [
    GetEmoji(
      emg: "😎",
      key: UniqueKey(),
    ),
    GetEmoji(
      emg: "🤠",
      key: UniqueKey(),
    ),
  ];
```
- 
![workingwithstateful.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628848991280/3HimX9nSf.gif)
- Here what is happening is when flutter tries to match the `type`, its gets matched. But when it is trying to match keys it will not match. And in the element tree, as `keys` are not matching, it will change the references and update the app.
- **Swapping widget**
![key1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628849582048/y2wYb96Y7.png)

- **Keys not matched**
![key2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628849591277/o2rEmypdW.png)
- **Change references**
![key3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628849851917/94dkuW6Vw.png)
- **Swap of Elements in ElementTree **
![key4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628849860108/3VfPCVUR8.png)

-----------------------------
## Where to put `Keys`
- **NOTE** one thing, That if you need to add keys to your app, you should add them at the `top` of the widget subtree. Otherwise, you'll get some weird results.
- Let me explain with an example.
- Here I've used the previous example only. Just added a background color which is generated randomly.
- Everything is running.
- 
![withbg.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628850646147/Fc2EMQVcg.gif)
- Now let's wrap our `GetEmoji` widget with `Container` widget. Now observe here `UniqueKey` is not at the `top` of its widget tree.
- 
```
  List<Widget> emojis = [
    Container(
      child: GetEmoji(
        emg: "😎",
        key: UniqueKey(),
      ),
    ),
    Container(
      child: GetEmoji(
        emg: "🤠",
        key: UniqueKey(),
      ),
    ),
  ];
```
- And now let's run the app again
- 
![withbgerror.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628850801621/agUUM0V9x.gif)
- Here the Widgets are swapping, that's okay but the new color is generating again and again when the swap button is triggered. 
- In fact, It is not only the new color that is generating again and again but also a new `Text Widget` is generating again and again in the widget tree, we are not able to see that because we're using two static emojis only. 
- We've already assigned the `Keys` to the widget **RIGHT**? But it's not about the keys which are creating a problem it's about the `position` of the keys.
- So what is going on?.
- **Here is the structure of the Widget and Element Tree**
![random1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628853426908/2iq14vqBQ.png)

- Here when we perform the swap operation, Flutter’s element-to-widget-matching algorithm looks at only one level in the tree at a time. At that first level of children with the Padding elements, everything matches up correctly.
- At the second level, Flutter notices that the key of the `😎 Container Element ` doesn’t match the key of the widget, so it deactivates that `😎 Container Element`, dropping those connections. 
- 
![random2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628853437095/CbVWbC6OV.png)
- The keys we’re using in this example are `LocalKeys`. That means that when matching up widgets to elements, Flutter only looks for key matches within a particular level in the tree.
- Since it can’t find a `Container Element` at that level with that `key` value, it creates a new one, and initializes a new state, in this case, making the widget with the random background color.
- 
![random3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628921828239/50tHEXIiA.png)
- This we can solve by adding the `key` in the `Padding` widget.
- So moral of the story is **YOU HAVE TO DEFINE THE KEY AT THE TOP OF THE WIDGET TREE.**

----------------------------------------

## `ValueKey` :
- A key that uses a `value` of a particular type to `identify` itself.
- The `ValueKey` is useful if we want to preserve the state of the Stateful widgets when they move around the widget tree.
- We can use the `ValueKey` when we want to remove `Widget` from the widget tree, or reordering the list.
- Consider the below code, where there are 2 `Textfield` widget. And we want to remove the last `Textfield` from the widget tree.
- 
```
bool showFavouriteFramework= true;
//...
Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            if (showFavouriteFramework)
              TextField(
                decoration: InputDecoration(
                    border: OutlineInputBorder(),
                    labelText: "Favourite Framework"),
              ),
            TextField(
              decoration: InputDecoration(
                  border: OutlineInputBorder(),
                  labelText: "Favourite Language"),
            ),
            SizedBox(height: 10),
            ElevatedButton(
              onPressed: () {
                setState(() {
                  showFavouriteFramework = false;
                });
              },
              child: Text("Remove Favourite Framework field"),
            )
          ],
),
```
- 
![valuekeyex.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628861939861/QTV7bc0us.png)
- When we press the `Remove Favourite Framework field` button.
- 
![valuekeynotwokingex.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628922503125/77LJGRTXK.gif)
- If you observe, we got the `Text` of Favourite Framework's Textfield i.e `Flutter` in the Textfield of Favourite language's Textfield instead of `Dart`.
- **NOTE** this will only happen if you use the multiple Stateful widgets of the same type.
- What's happening here is, when we're removing the first Textfield, Flutter is not able to identify which TextField it has to remove, because both are of the same type.
- We've to provide those widgets unique values that can help flutter to identify that they are different.
- We can provide Unique values with the help of `ValueKey`.
- 
```
TextField(
                key: ValueKey("Framework"),
                decoration: InputDecoration(
                    border: OutlineInputBorder(),
                    labelText: "Favourite Framework"
         ),
),
TextField(
              key: ValueKey("Language"),
              decoration: InputDecoration(
                  border: OutlineInputBorder(),
                  labelText: "Favourite Language"
         ),
),
```
- 
![valuekeywokingex.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628923209337/SsAoWc9sO.gif)
- Now as we can see Favourite Language got its actual value as expected.
- Here Flutter will first check the type of those two widgets and check if it is the same or not, **and it is**. Then after it'll check if the `keys` are of the same type or not, and **it's not**. So flutter will update the state and references accordingly.
- Here in the `ValueKey` you can provide any type of unique values, like, `String`, `int`, `double`, `Objects`, etc.
- > But all the widgets must have unique values. That you should keep in mind. Otherwise, it'll not work.
- > One important thing is when we have a list of widgets inside `Listview`, `Column`, `Row`, try to avoid giving the `index` value coming from the list as the `key`. 


------------------------------

## `ObjectKey`
- A key that uses a reference of a particular type to identify itself.
- The `ObjectKey` is useful if we want to preserve the state of the Stateful widgets when they move around the widget tree.
- `ObjectKey` can be used in cases like when you are reordering the widget in the list or adding or removing the widgets from a list.
- Let's take an example.
- I've created a List of SuperHero objects from the class SuperHero.
- 
```
  late List<SuperHero> superHeroList;

  @override
  void initState() {
    superHeroList = [
      SuperHero(movie: "Iron Man", name: "Tony Stark"),
      SuperHero(movie: "Hulk", name: "Bruce Banner"),
      SuperHero(movie: "Thor:Ragnarok ", name: "Thor"),
    ];
    super.initState();
  }
```
- 
```
Scaffold(
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          setState(() {
            superHeroList.insert(0, superHeroList.removeAt(1));
          });
        },
        child: Icon(Icons.swap_calls),
      ),
      body: Center(
        child: Column(
          children: superHeroList
              .map<Widget>((hero) => HeroWidget(hero: hero))
              .toList(),
        ),
      ),
);
```
- This program will swap the first two item's position in the `superHeroList`.
- But if we try to swap these two items, something is going wrong, here if you see the element's text is interchanging but the colors are not. It should also change, right? because the color is also connected with that list item.
![objectkeynotworkingex.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628939022092/-R47VyyE1.gif)
- As we've discussed in the unique key, that flutter is not able to distinguish the widget because of the same type.
- Then what's the solution?
- You might think, we can use `ValueKey`, **Right?**. And yes you're right we can use `ValueKey` to distinguish the list widgets. But there will be an issue. Let's see what happen if we consider the `ValueKey` in this situation.
- Giving the `ValueKey` to `key` parameter.
- 
```
Center(
        child: Column(
          children: superHeroList
              .map<Widget>(
                (hero) => HeroWidget(
                  key: ValueKey(hero),
                  hero: hero,
                ),
              )
              .toList(),
        ),
),
```
- And we'll get the result as expected. The items are swapping with color now.
- 
![valuekeyinobjectkeyex.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628939788305/mUjfFOxzq.gif)
-**BUT...but**, Now add the same `Object` in the list.
- 
```
superHeroList = [
      SuperHero(movie: "Iron Man", name: "Tony Stark"),
      SuperHero(movie: "Iron Man", name: "Tony Stark"),
      SuperHero(movie: "Hulk", name: "Bruce Banner"),
      SuperHero(movie: "Thor:Ragnarok ", name: "Thor"),
];
```
- And the output is........
- 
![valuekeyerror2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628940044429/jA7Xj6kKq.png)
- 
![BunniesWhatGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628940067601/NCs_l1MYE.gif)
- Flutter will throw an error something like this :
- 
![valuekeyerror.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628940113374/pTfsC_hlq.png)
- And it's correct because what we've seen in the `ValueKey` explanation is that the **`widget is identified by its value when we use ValueKey**
- Here, in this case, we've added two same objects with the same value. That's why Flutter is throwing an error that **Hey, I found duplicate keys**.
- In such cases, we have to use `ObjectKey`.
- As we've seen in the definition of the `ObjectKey`, that `ObjectKey` will distinguish the item based on the **references**.
- So let's try to add `ObjectKey` in the `key` parameter.
- 
```
HeroWidget(
                  key: ObjectKey(hero),
                  hero: hero,
),
```
- And as soon as we add the `ObjectKey` we can see the output. And all the things are working fine now.
- 
![withobjectkey.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628940483888/PP5ohqnq6D.gif)

----------------------------

## PageStorageKey 
- The `PageStorageKey` is basically used to store the scroll position of the scrollable widgets like `ListView`, `GridView` etc.
- In some cases, we want to provide the functionality of storing the position of the scrolling list item and when users came back later to that scroll view they can start scrolling where they left.
- In this case, we can use `PageStorageKey` to preserve the state of the scrolling position.
- Let's take an example to understand how we can use `PageStorageKey` in our app.
- 
```
Scaffold(
      body: ListView.builder(
        itemCount: 100,
        itemBuilder: (context, index) {
          return Padding(
            padding: const EdgeInsets.all(8.0),
            child: Text(
              "Item : $index",
              style: TextStyle(fontSize: 22),
            ),
          );
        },
      ),
);
```
- Here I've created a simple Listview
![pagestorage.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628941334694/EjZ2asbhY.gif)
- Now let's go to another tab while leaving the scroll position in the middle.
- 
![pagestoragelistview.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628949482016/NaPtsFQp0.gif)
- See? It's not preserving the position of the listview.
- Let's try to solve this issue by adding `PageStorageKey` in the ListView's `key` parameter
- 
```
ListView.builder(
        key: PageStorageKey<String>("listViewKey"),
        itemCount: 100,
        itemBuilder: (context, index) => ListTile(
          title: Text(
            'List item ${index + 1}',
            style: TextStyle(fontSize: 24),
          ),
        ),
);
```
- 
![pagestoragelistviewworking.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628949595239/vxuHjF6MF.gif)
- **THAT'S**!! That's all you have to do to store the scroll location. Flutter will handle all of the complicated things under the hood.
- **BUT**, what if you've popped that screen from the widget tree and then again visit this page? Because in the above case we're only going to another tab without popping the current page.
- In popped screen case, you'll not be able to get the previous position of the scroll view, because when you pop the screen flutter will also remove the `PageStorageKey` attached to it.
- 
![popscreen.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628950235263/hTBcBVETi.gif)
- To solve this issue we need to wrap `PageStorage` inside the parent widget of the widget tree. In our case, we can wrap it inside the `Scaffold` because the `route ` is created before the build
- 
```
final globalBucket = PageStorageBucket(); '''Don't declare it inside any class. Declare it on global level.''' 
```
```
Widget build(BuildContext context) {
    return PageStorage(
      bucket: globalBucket,
      child: Scaffold(
        bottomNavigationBar: BottomNavigationBar(
          backgroundColor: Theme.of(context).primaryColor,
          selectedItemColor: Colors.white,
          unselectedItemColor: Colors.white70,
          currentIndex: index,
          items: [
            BottomNavigationBarItem(
              icon: Icon(Icons.list),
              title: Text('ListView'),
            ),
            BottomNavigationBarItem(
              icon: Icon(Icons.person),
              title: Text('Blah blah'),
            ),
          ],
          onTap: (int index) => setState(() => this.index = index),
        ),
        appBar: AppBar(),
        body: buildPages(),
      ),
    );
}
```
- Now it is working
![pageStorageWorking.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628951083295/vBvbTssTe.gif)


---------------------------------------

## GlobalKey 
- This is the most used Key in Flutter compare to the above Keys.
- The `GlobalKey` can be used to change the parents anywhere in your app without losing state
- It can be used to access information about another widget when we are on a completely different location of the widget tree.
- The common use case of the `GlobalKey` is validating a `Form` or displaying the `Snackbar` in the app etc.
- Let's take an example.
- 
```
final _counterState = GlobalKey<_CounterState>();  //Declaring the GlobalKey of CounterState
```

```
Scaffold(
      appBar: AppBar(),
      body: SizedBox.expand(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Counter(
              key: _counterState,
            ),
          ],
        ),
      ),
);
```
- 
```
class Counter extends StatefulWidget {
  const Counter({
    Key? key,
  }) : super(key: key);

  @override
  _CounterState createState() => _CounterState();
}
```
```
class _CounterState extends State<Counter> {
  late int count;

  @override
  void initState() {
    super.initState();
    count = 0;
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: <Widget>[
        Text(
          count.toString(),
          style: TextStyle(fontSize: 30),
        ),
        ElevatedButton(
            onPressed: () {
              setState(() {
                count++;
              });
            },
            child: Text("Add"))
      ],
    );
  }
}
```
- **Output**
- 
![globalkey1.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628957682187/jH9iKXHLz.gif)
- Now we can access the `count` value of `CounterWidget` in any page by passing the `GlobalKey`
- 
```
class SecondPage extends StatefulWidget {
  final GlobalKey<_CounterState> counterKey;
  SecondPage(this.counterKey);
  @override
  _SecondPageState createState() => _SecondPageState();
}
```
```
class _SecondPageState extends State<SecondPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(),
      body: Center(
        child: Row(
          children: <Widget>[
            IconButton(
              icon: Icon(Icons.add),
              onPressed: () {
                setState(() {
                  widget.counterKey.currentState!.count++; //here
                  print(widget.counterKey.currentState!.count);
                });
              },
            ),
            Text(
              widget.counterKey.currentState!.count.toString(),
              style: TextStyle(fontSize: 50),
            ),
          ],
        ),
      ),
    );
  }
}
```
- 
![globalkey2.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628958133219/LXnt6O6ob.gif)
- So as we can see GlobalKey can be used to access information about another widget when we are on a completely different location of the widget tree.


-------------------------------

## THAT'S IT
- That's all you need to know about **Keys**.
- Hope you liked it. Thanks for reading
- Feedback and Comments are welcomed 🙂

- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628960249026/AAcm5Y3qL.gif)
