---
title: "Flutter Widget In Detail: Scaffold"
datePublished: Fri Aug 13 2021 04:38:51 GMT+0000 (Coordinated Universal Time)
cuid: cks9v1qqp07k5wvs1buf5e9ej
slug: flutter-widget-in-detail-scaffold
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1628776447047/-MggebksH.png
tags: dart, flutter, flutter-sdk, flutter-examples, flutter-widgets

---

## Introduction
- Before we design anything in Flutter, we need something in the base which can hold the basic layout structure and provide us some common widgets that help us building design easily.
- For example, If you observe any application in your mobile app, almost all have some similarities, like they have some kind of **AppBar**, **BottomNavigationBar**, **Drawer**, **BottomSheets**,  etc. **Right**? 
- Because these are some common things that every app has, Flutter helps developers by providing these basics building blocks in-built in Flutter SDK so that they can easily integrate them into their app, without any problem.
- So what do we have to do or which widget helps us get those things? 
- Allow me to introduce one of the awesome widget of Flutter **SCAFFOLD**.
- 
![ExcitedMinionsGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628599079413/lDIRkaIVU.gif)
- **Scaffold** implements the basic material design layout structure.
- **Scaffold** provides us `AppBar`, `BottomNavigationBar`, `Drawer`, `FloatingActionButton`, `BottomSheet`, that we can use in our app.
- 
![WowOmgGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628599268290/lmKISB1WQ.gif)
- Ideally, in **MaterialApp ** every page/Screen will consist of the parent widget as a **Scaffold**. If we don't give **Scaffold ** as a parent widget there will be no **material ** look and feel in **Material App**.
- If you don't use **Scaffold** as a child of a **MaterialApp** :
- 
```
class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
        child: Text("😢 I'dont have Scaffold")
      );
  }
}
```
- 
![noScaffold.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628599859266/878uZOIm0.png)
- **See??**. It looks horrible.
- But when you provide a **Scaffold** :
- 

```
class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Text("😎 I am inside Scaffold")
      )
    );
  }
}
```
- 

![withScaffold.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628600475407/-cDe8u8pq.png)
- You can clearly see the difference .**Scaffold** gives a material design-like feel.
- So now let's see all the properties of the **Scaffold** widget one by one.

------------------------
## `body` :
- This property takes `Widget` as an input.
- The `body` has the primary content that has to be shown on the screen.
- The widget in the body is positioned at the top-left corner of the **Scaffold** initially.
- 
![topLeft.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628600689439/67f2N5qQu.png)
- To center this widget, consider putting it inside `Center` widget.
- 
```
Scaffold(
      body: Center(
        child: Text("🙃 Center of the Scaffold")
      )
);
```
- 
![centerScaffold.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628600704539/GFV8mGyFa.png)
- If we wrap this centered `Text` inside the **Container**, it will only take the height and width of its child widget :
- 
```
Scaffold(
      body: Center(
        child: Container(
          color: Colors.green,
          child: Text(" 🤠 Expand me")
        )
      )
);
```
- 
![containerabovetext.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628601003980/Vg2p38gz6-.png)
- If you want to **expand** the Container widget to take full width and height of **Scaffold**, consider putting it in **SizedBox.expand**.
- 
```
Scaffold(
      body: SizedBox.expand(
        child: Container(
          alignment: Alignment.center,
          color: Colors.green,
          child: Text("🥳 Yay!! I'm Expanded")
        ),
      )
);
```
- 
![expanded.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628601262886/Gr7HH33y5.png)
- If you have some kind of big list wrapped inside the `Column` widgets, normally it should fit on the screen. But content may overflow from the Column.
- 
![overflow.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628601729816/eU5zW5pL2.png)
- In such cases, we want some kind of scrolling, to make sure users can scroll the content. To make overflowed content scrollable, consider using a **ListView** as the body of the **Scaffold**. This is also a good choice for the case where your body is a scrollable list.
- 
```
Scaffold(
      body: ListView(
        children: [
          Container(
            width: 200,
            height: 150,
            color: Colors.green,
          ),
          // other widgets
        ],
      )
);
```
![scrollable.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628601952193/AEaUr7MKh.gif)

----------------------

## `backgroundColor` : 
- We can give a **Scaffold** a background color by giving `Color` value inside the `backgroundColor` property.
- Default color is `ThemeData.scaffoldBackgroundColor`.
- 
```
Scaffold(
      backgroundColor: Colors.purple,
      body: // widget
);
``` 

-  
![bgColor.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628602350473/1FOzc0kyQ.png)

-------------------------

## `floatingActionButton` :
- This is a simple circular button placed on the top of the **body** of the Scaffold, or we can say it is `floating` above the **body**, In the bottom-right corner
- 
```
Scaffold(
      floatingActionButton: FloatingActionButton(
               child: Icon(Icons.add),
               onPressed: (){},
          ),
      body: // widget
);
```
- 
![floatingbutton.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628602803059/28Kig9Twy.png)
- Here `child` property of `FloatingActionButton` is used to give any kind of widget as a child of `FloatingActionButton`.
- `onPressed` property provides a callback that is called when the button is pressed.

-----------------------

## `floatingActionButtonLocation` :
- It is responsible for determining where the `floatingActionButton` should go.
- By default the `floatingActionButton ` is place at bottom-right corner.
- There are many default constructors available for positioning the `floatingActionButton`.
- 
![floatingpositionlist.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628603330168/R74EiFwcrI.png)
- Example :
- 
```
Scaffold(
   floatingActionButtonLocation:  FloatingActionButtonLocation.centerFloat,
   body: // widget
)
```
- Here I've displayed some of the possible positions
![floatingposition.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628604148426/Iz7FAIp6Ma.png)

--------------------
## `floatingActionButtonAnimator` :
- This is used to animate the `floatingActionButton` from one `floatingActionButtonLocation` to another.
- The `FloatingActionButtonAnimator`defines :
- `Offset` of the `FloatingActionButton` between old and new `floatingActionButtonLocation`.
- An `Animation` to scale the `FloatingActionButton` during the transition.
- An `Animation` to rotate the `FloatingActionButton` during the transition.
- Where to start a new animation from if an animation is interrupted.
- The `FloatingActionButtonAnimator` has one constant called `scaling` which moves the `FloatingActionButton` by scaling `out` and then `in` at a new `FloatingActionButtonLocation`.

------------------

## `appBar` :
- It is a typical **AppBar** that is displayed at the top of **Scaffold**.
- We can create an **AppBar** by passing `AppBar()` as an input.
- The **AppBar** has various properties like `title`, `actions`, `elevation`, `backgroundColor` etc.
- We can also create our own custom **AppBar** by implementing **PreferredSizeWidget** our class.
- Example :
- 
```
Scaffold(
      appBar: AppBar(
        title: Text("Widget In Detail"),
        backgroundColor: Colors.deepOrangeAccent,
      ),
      body: // widget
);
```
- 
![appbar.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628616453764/zZ7JjdoNe.png)

------------------------------

## `bottomNavigationBar` :
- In a typical application user interface there is one navigation panel through which users can navigate through a different part of an app.
- Most of the app uses `BottomNavigationBar` for navigation, positioned at the bottom of the **Scaffold** body.
- We can create our own custom `bottomNavigationBar`, but Flutter provides us a built-in `BottomNavigationBar`.
- 
```
Scaffold(
      body: Container(),
      bottomNavigationBar: BottomNavigationBar(
      currentIndex: _currentIndex,
      fixedColor: Colors.deepOrange,
      items: [
        BottomNavigationBarItem(
          title: Text("Home"),
          icon: Icon(Icons.home),
        ),
        BottomNavigationBarItem(
          title: Text("Search"),
          icon: Icon(Icons.search),
        ),
        BottomNavigationBarItem(
          title: Text("Add"),
          icon: Icon(Icons.add_box),
        ),
      ],
      onTap: (int index){
         setState(() {
          _currentIndex = index;
        });
      },
     ),
);
```
- 
![bottombar.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628617573910/QuMdXEbm-.gif)
 
------------------------------

## `bottomSheet`:
- It is a kind of we can say overlay that is shown at the bottom of the app.
- There can be two types of `bottomSheet` : 
- **Persistent Bottom Sheet** : By using the **Persistent Bottom Sheet** we can interact with our app content as well as the sheet content. Which we can't do with the **Model Bottom Sheet**.
- **Model Bottom Sheet** : It is a kind of pop-up, with some menus. If a user clicks outside of that sheet area, the sheet will be dismissed immediately. It means we cannot interact with our app content and with the Sheet content at the same time.
- The `BottomSheet` widget itself is rarely used directly. Because we can't open or close it by swiping up or down. It's static.
```
Scaffold(
      bottomSheet: BottomSheet(
        onClosing: (){},
        builder: (_){
          return Container(
            width: MediaQuery.of(context).size.width,
            height:150,
            color:Colors.green,
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Text("Count in BottomSheet $_bottomSheetCounter"),
                RaisedButton(
                  child: Icon(Icons.add),
                  onPressed:(){
                    setState((){
                      _bottomSheetCounter++;
                    });
                  }
                )
              ],
            )
);
```
- 
![bottomsheetstatic.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628690008061/vo_1VbTOs.gif)
- If you want to use make it dismissible, or open it when some event is triggered, Instead, prefer to create a persistent bottom sheet with `ScaffoldState.showBottomSheet` or `Scaffold.bottomSheet`, and a modal bottom sheet with `showModalBottomSheet`.

### `persistentBottomSheet` : 
- Create a `GlobalKey` of type `ScaffoldState`. And pass it to the Scaffold's `key` property
```
final _scaffoldKey = new GlobalKey<ScaffoldState>();
```
```
Scaffold(
     key: _scaffoldKey
)
```
- Add a button inside the body for triggering bottomSheet.
```
Scaffold(
    key:_scaffoldKey,
    body: Center(
        child: RaisedButton(
               onPressed: _showPersistentBottomSheet,
               child: Text("Persistent"),
            ),
   )
)
```
- Declare `VoidCallback` of `_showPersistentBottomSheet` and assign it to the actual function that will trigger the bottomSheet.
- 
```
VoidCallback? _showPersBottomSheetCallBack;
@override
  void initState() {
    super.initState();
    _showPersBottomSheetCallBack = _showBottomSheet;
}
void _showBottomSheet() { // }
```
- Now implement the `_showBottomSheet` function.
- 
```
 void _showBottomSheet() {
    setState(() {
      _showPersBottomSheetCallBack = null;   // We don't want to press button again if the sheet already opened That's why we are disabling the button.
    });

    _scaffoldKey.currentState
        !.showBottomSheet((context) {
          return Container(
            height: 200.0,
            color: Colors.deepOrange,
            child: Center(
              child: Text("I'm Persistent"),
            ),
          );
        })
        .closed
        .whenComplete(() {
          if (mounted) {
            // If our sheet is not visible then we are again attaching the `_showBottomSheet` function to `_showPersBottomSheetCallBack ` as we did in `initState`
            setState(() {
              _showPersBottomSheetCallBack = _showBottomSheet;
            });
          }
        });
  }
```
- 
![persBottomSheet.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628691543201/99C3a6HT1.gif)


### `showModelBottomSheet` : 
- It's very simple, just implement `showModelBottomSheet` function which is in-built in flutter and attach with any button, you are ready to go.
-
```
  void _showModalSheet() {
    showModalBottomSheet(
        context: context,
        builder: (builder) {
          return Container(
            color: Colors.greenAccent,
            child: new Center(
              child: Text("I'm ModalSheet"),
            ),
          );
        });
}
```
- 
![modelSheet.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628692534218/Refi1h81N.gif)


--------------------------

## `drawer` :
- A drawer is a `Panel` displayed on the left or right side of the body.
- It is mostly hidden on mobile devices.
- To open it the user has to swipe left-to-right or right-to-left.
- `drawer` takes `Drawer` widget as input.
- You can create your own custom `Drawer` too.
- It is usually used to show user profile info, navigation links, about information etc.
- Example :
- 
```
Scaffold(
      appBar: AppBar(),
      drawer: Drawer(
        elevation: 16.0,
          child: Column(
            children: <Widget>[
              UserAccountsDrawerHeader(
                accountName: Text("Dhruv"),
                accountEmail: Text("nakumdhruv123@gmail.com"),
                currentAccountPicture: CircleAvatar(
                  backgroundImage: NetworkImage("https://media-exp1.licdn.com/dms/image/C4D03AQHDlYNK0WgLFA/profile-displayphoto-shrink_400_400/0/1621524948952?e=1634169600&v=beta&t=_fPR4KDunI_mvH0YCaa9T_aj1Fo0A19DlTbF7n_IdBM"),
                ),
              ),
            ListTile(
              title: new Text("All Inboxes"),
              leading: new Icon(Icons.mail),
            ),
            Divider(
              height: 0.1,
            ),
            ListTile(
              title: new Text("Primary"),
              leading: new Icon(Icons.inbox),
            ),
            ListTile(
              title: new Text("Social"),
              leading: new Icon(Icons.people),
            ),
            ListTile(
              title: new Text("Promotions"),
              leading: new Icon(Icons.local_offer),
            )
        ],
    ),
),
      body: Container()
);
```
- 
![drawer.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628693488726/nBBGxaX5x.gif)


---------------------

## `drawerEdgeDragWidth`:
- This is the width of the area within which drawer opens.
- By default, the value used is 20.0
- Lets set it to `0.0` and see what happen
- 
```
Scaffold(
    drawerEdgeDragWidth: 0,
)
```
- 
![zeopdragwidth.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628696503106/bOPSw1nY5s.gif)
- As you can see the drawer is no longer opening, It is because of the area where the drag behavior stars is now zero.
- And if we now set it to some higher value 
- 
```
Scaffold(
    drawerEdgeDragWidth: 150,
)
```
- 
![dragwidth150.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628696759945/hp7yNwvLN.gif)

-----------------------

## `drawerScrimColor` :
- It is the color that is used to obscure/hide the primary content of the app.
- Default value is `Colors.black54`
- Example :
```
Scaffold(
    drawerScrimColor: Colors.red.shade300,
)
```
- 
![scrimcolor.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628697152123/bopADai0F.gif)

------------------------

## `drawerEnableOpenDragGesture` :
- This is responsible for opening the `drawer` by dragging.
- If set to `false`, the `drawer` will no longer open when the user will swipe from left-to-right or right-to-left.
- Default value is `true`.
- Example :
- 
```
Scaffold(
     drawerEnableOpenDragGesture: false,
)
```
- 
![stopedrag.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628697510635/pvKWOzowa.gif)

-------------------------
## `onDrawerChanged ` :
- It expects callback function as an input.
- And it is called when the `Drawer` is `opened` or `closed`
- Example :
```
Scaffold(
     onDrawerChanged: (_){
        print("Drawer $_");
      },
)
```
- 
![drawercallback.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628701190135/VV8hS9mpd.gif)

-------------------------

## `endDrawer` :
- Same as `drawer`, but instead the panel/drawer is on the right side of the app.
- Swipe right-to-left to open/close drawer.
- 
```
Scaffold(
      endDrawer: Drawer(
      elevation: 16.0,
          child: Column(
            children: <Widget>[
              UserAccountsDrawerHeader(
                accountName: Text("Dhruv"),
                accountEmail: Text("nakumdhruv123@gmail.com"),
                currentAccountPicture: CircleAvatar(
                  backgroundImage: NetworkImage(url),
                ),
              ),
              // Drawer content
        ],
    ),
      ),
)
```
- 
![enddrawer.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628697890380/x61wHuQ-A.gif)

-----------------

## `endDrawerEnableOpenDragGesture`:
- Same as `drawerEnableOpenDragGesture` but for the `endDrawer`
- If set to `false`, the `drawer` will no longer open when the user will swipe from right-to-left or left-to-right.
- Default value is `true`.

-----------------------------
## `onEndDrawerChanged` :
- Same as `onDrawerChanged`, except it is for `endDrawer`
- Example :
```
Scaffold(
     onEndDrawerChanged: (_){
        print("Drawer $_");
      },
)
```
-------------------

## `extendBody` :
- If `true`, and `bottomNavigationBar` is specified, then the `body` `extends` to the bottom of the `Scaffold`.  Instead of only extending to the top `bottomNavigationBar`.
- If `false`, and `bottomNavigationBar` is specified, then the `body` will not `extend` to the bottom of the `Scaffold`. And only extends to the top `bottomNavigationBar`.
- Default is `false`
- With `extendBody: true`
```
Scaffold(
      extendBody: true,
      bottomNavigationBar: BottomNavigationBar(
       // navigation items
      )
      body: // items
)
```
- 
![extenttrue.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628700040112/v3luSTq5J.png)
- With `extendBody: false (Default)`
```
Scaffold(
      extendBody: false,
      bottomNavigationBar: BottomNavigationBar(
       // navigation items
      )
      body: // items
)
```
- 
![extentfalse.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628700069297/8VmVNVFqW.png)

-------------------
## `extendBodyBehindAppBar` :
- This is used when we want to place our body behind the `AppBar`.
- For this `AppBar` should have `transparent` `backgroundColor`
- This property is false by default. It must not be null.
- With `extendBodyBehindAppBar : true`
```
Scaffold(
      extendBodyBehindAppBar: true,
      appBar: AppBar(backgroundColor: Colors.transparent,)
      body: // items
)
```
- 
![appextenttrue.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628700586514/Qyadl9NrAw.png)
- With `extendBodyBehindAppBar : false`
```
Scaffold(
      extendBodyBehindAppBar: false,
      appBar: AppBar(backgroundColor: Colors.transparent,)
      body: // items
)
```
- 
![appextentfalse.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628700624824/lPKJuq_xH.png)
- > If you are using `ListView` or `GridView` make sure to have `padding: EdgeInsets.only(top: 0)`, to see expected results.


----------------------------

## `persistentFooterButtons` :
- A set of buttons that are displayed at the bottom of the `Scaffold`.
- Typically this is a list of TextButton widgets. 
- These buttons are persistently visible, even if the body of the scaffold scrolls.
- The `persistentFooterButtons` are rendered above the `bottomNavigationBar` but below the `body`.
- Example :
- 
```
Scaffold(
  body: Container(
    color: Colors.white,
    child: Center(child: Text("Persistent Footer Buttons"),),
  ),
  persistentFooterButtons: <Widget>[
    Row(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: <Widget>[
        FlatButton(
          onPressed: () {},
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: <Widget>[
              new Icon(Icons.home),
              new Text('Home'),
            ],
          ),
        ),
        FlatButton(
          onPressed: () {},
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: <Widget>[
              new Icon(Icons.search),
              new Text('Search'),
            ],
          ),
        ),
        FlatButton(
          onPressed: () {},
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: <Widget>[
              new Icon(Icons.person),
              new Text('Profile'),
            ],
          ),
        ),
      ],
    ),
  ],
);
```
- 
![persistentfooter.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628701694894/k-Y_TuV0Q.png)


---------------------------

## `resizeToAvoidBottomInset` :
-  If `true` the `body` and the scaffold's floating widgets should size themselves to avoid the onscreen keyboard.
- For example, if there is an onscreen keyboard displayed above the `scaffold`, the body can be resized to avoid overlapping the keyboard, which prevents widgets inside the body from being obscured by the keyboard.
- Example :
- With `resizeToAvoidBottomInset : false` : 
- 
```
Scaffold(
    resizeToAvoidBottomInset: false,
    body: // Content
)
```
- 
![resizefalse.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628704914887/lf-1vBs3T.png)
- With `resizeToAvoidBottomInset : true` : 
- 
```
Scaffold(
    resizeToAvoidBottomInset: true,
    body: // Content
)
```
- 
![resizetrue.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628704951417/GdMJ-duSGm.png)


---------------------------

## `primary` :
- Whether this `scaffold` is being displayed at the top of the screen.
- If true then the height of the `appBar` will be extended by the height of the screen's status bar, i.e. the top padding for MediaQuery.
- The default value of this property, like the default value of `AppBar.primary`, is `true`.
- With `primary: false`
- 
![primaryfalse.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628705377762/_YI_wqpI9.png)
- With `primary: true`
- 
![primarytrue.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628705397911/CfMuyOgmL.png)

---------------------

## `restorationId` : 
- I've explained the whole concept of `Flutter State Restoration` in [MaterialApp's Blog](https://dhruvnakum.xyz/flutter-widget-in-detail-materialapp)

-------------------

## THAT'S IT
- That's all you need to know about the **Scaffold** widget.
- Thank you for reading

- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628705592770/q0ZeJA2w5.gif)

- Previous Widget: [MaterialApp](https://dhruvnakum.xyz/flutter-widget-in-detail-materialapp)