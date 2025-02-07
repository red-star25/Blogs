---
title: "Flutter Widget In Detail: AlertDialog"
datePublished: Mon Aug 09 2021 06:08:34 GMT+0000 (Coordinated Universal Time)
cuid: cks48hp0r108zhqs1f9zdgijn
slug: flutter-widget-in-detail-alertdialog
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1628255581305/ke8eDiBmC.png
tags: dart, flutter, flutter-sdk, flutter-examples, flutter-widgets

---

### Introduction : 
- Sometimes it is necessary to notify our users of important information, with some kind of alert. Or we can give choices to our users to choose certain actions. 
- For example: If the user clicks on the logout button, then a pop-up appears with confirmation like "Are you sure you want to exit ? " with actions buttons like `Yes` or `No`, or If the user clicks on the delete account, we can display a pop up with a password field to make sure that the actual user with his/her password wants to delete his/her account, etc.
- We can also take users' permission by opening a dialog with permission information to make sure that the user has no issue with the permission the app is using. There are many other use cases where we can use AlertDialog.
- There are many types of dialog available in Flutter SDK.
- For example , there are `AlertDialog`, `SimpleDialog`, `AboutDialog`. But in this blog, I'm going to explain about the **AlertDialog** only.
- Let's see how to implement Alertdialogs in our Flutter application


---------

### AlertDialog :
- AlertDialog is used to display important information by opening a popup menu on the top of the application such as password confirmation/verification, application notification, etc.
- 
![logout.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628240337310/5GPp3T_ak.png)
![appnotification.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628240351774/GvpDFzPxm.png)
- There are many properties available, by which we can easily style our dialog in our own way. 
- Let's see what each and every property does.
- > But before that, I want to point out one thing, that we have to call the function called `showDialog` which is **required ** to open the dialog.
> which goes something like this: 
> 
```
showDialog(
   context: context,
   builder: (BuildContext context) {
       return AlertDialog()
   }
)
```
> We can call this `showDialog` function in a button's callback function. For example:
> ```
ElevatedButton(
   child: Text("Show AlertDialog"),
   onPressed: () {
       showDialog(
         // ..... 
       )
   }
)
```
- Now let's see all the available properties in AlertDialog.

---------------------

### `title`: 
- This property takes `widget` as an input. Usually, we give `Text()` widget to display the title of the alert dialog.
- It's not compulsory to give `Text`, we can also provide an `Image`, `Icon`, etc.
- Example
- 
```
showDialog(
            context: context,
            builder: (context) {
              return AlertDialog(
                title: Text("Hello AlertDialog"), // Icon(Icons.home) or any kind of widget...
              );
       }
);  
```
- Output :
- 
![title.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628245196829/NWALxck6F.png)

----------------------

### `titleStyle`:
- By using this property we can style our `title` as per our requirement.
- It takes `TextStyle()` as an input.
- Example :
- 
```
AlertDialog(
                titleTextStyle: TextStyle(color:Colors.red),                
                title: Text("Hello AlertDialog")
);
```
- Output : 
- 
![textstyle.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628245123800/-b15nktAE.png)

---------------------------

### `titlePadding`:
- This will give padding to the title from the inside.
- It takes `EdgeInsets`'s constructors as an input.
- By default, `titlePadding`gives padding of 24 pixels at the top, the left, and the right of the title. It also offers 20 pixels of padding at the bottom of the title if the content is null.
- Example :
- 
```
AlertDialog(
                titleTextStyle: TextStyle(color:Colors.red),
                titlePadding: EdgeInsets.all(20.0),                
                title: Text("Hello AlertDialog")
);
```
-------------------------

### `shape`:
- When we want to give borderRadius or curves to our dialog we can use this property.
- It takes subclasses of `ShapeBorder`. There are many subclasses available : `CircleBoder`, `RoundedRectangleBorder`, `ContinuousRectangleBorder`, `BeveledRectangleBorder`, `Border`, `BorderDirectional`, `BeveledRectangleBorder`, `ContinuousRectangleBorder`, `StadiumBorder`, `OutlineInputBorder`, `UnderlineInputBorder`.
- Example :
- 
```
AlertDialog(
                shape: RoundedRectangleBorder(
                  borderRadius: BorderRadius.circular(25.0),
                  side: BorderSide(width: 16.0, color: Colors.red.shade200),
                 ),
                title: Text("Hello AlertDialog")
);
```
- Output : 
- 
![shaperes.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628245081409/xh5d6CZdQ.png)

-----------------------------------

### `semanticLabel`:
- The semantic label of the dialog used by accessibility frameworks to announce screen transitions when the dialog is opened and closed.
- The system will read this description to the user if the accessibility mode is enabled.
- It takes `String` as an input.
- Example :
- 
```
AlertDialog(
                semanticLabel: "AlertDialog",
                title: Text("Hello AlertDialog")
);
```

-----------------------------------------

### `content`:
- This is an optional property. When used, The widgets will be displayed in the center of the dialog.
- Usually, this contains dialog messages.
- Example :
```
AlertDialog(
                title: Text("Hello"),
                content: Container(
                  width: 300.0,
                  height: 200.0,
                  color: Colors.greenAccent,
                  child: Center(child: Text("I am content"))
          )
);
```
- Output :
- 
![content.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628243394141/NRXTaeSPa.png)
- If your content overflows, 
- 
![contentoverflow.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628243941565/-iVfDthQD.png)
- Then you have to use `SingleChildScrollView` to make it scrollable.
```
AlertDialog(
                title: Text("Hello"),
                scrollable: true,
                content: Container(
                  width: 300.0,
                  height: 150.0,
                  color: Colors.greenAccent,
                  child: SingleChildScrollView(
                    child: Column(
                    children: [
                      // multiple childrens
                    ],
                  )
            )
      )
);
```
- Output : 
- 
![conentscroll.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628245409715/GA4Qodx57.gif)

-----------------------------------------

### `insetPadding`:
- This property is useful when we want to add extra padding from outside of our dialog box. 
- This defines the minimum space between the screen's edges and the dialog
- Defaults value is EdgeInsets.symmetric(horizontal: 40.0, vertical: 24.0).
- Example :
```
AlertDialog(
                insetPadding: EdgeInsets.all(10.0),
                title: Text("Hello"),
                content: Container(
                  width: MediaQuery.of(context).size.width,
                  height: 200.0,
                  color: Colors.greenAccent,
                  child: Column(
                    children: [
                      Text("Message body"),
                    ],
                  )
         )
);
```
- Output :
- 
![insetPadding.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628422697188/X7ZpIU_Nm.png)
- You can see the padding from left and right side of the dialog

-------------------------------------------

### `elevation`:
- We can give elevation to our dialog by specifying a value in `elevation` property.
- The default value is `24.0`.
- Example :
```
AlertDialog(
                elevation: 0.0,
                title: Text("Hello AlertDialog"),
);
```
- Output :
- 
![zeroelevation.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628245638761/dyj7mojKO.png)

-----------------------------

### `contentTextStyle`:
- We can style our `content`s' `Text` widgets by using `contentTextStyle`
- Example :
```
AlertDialog(
                contentTextStyle: 
                   TextStyle(color:Colors.green,fontWeight:FontWeight.bold),
                title: Text("Title"),
                content: Text("Message body"),
);
```
- Output:
- 
![contentStyle.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628245951765/YBaUy06xa.png)

-----------------------------------------

### `contentPadding`:
- This will provide padding around the `content` widgets.
- By default, contentPadding provides 20 pixels on the top of the content and 24 pixels on the left, the right, and the bottom of the content.
- Example :
```
AlertDialog(
                contentPadding: EdgeInsets.all(50.0),
                title: Text("Title"),
                content: Text("Message body"),
);
```
- Output:
- 
![contentpadding.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628246218620/trtkGAAN-.png)

-------------------------------------------------

### `buttonPadding`:
- This will provide padding around the buttons of `actions`s' widgets.
- By default, 8.0 logical pixels on the left and right.
- Example :
```
AlertDialog(
                buttonPadding: EdgeInsets.all(50.0),
                actions: [
                  ElevatedButton(child:Text("Action Btn"),onPressed:(){}),
                  ElevatedButton(child:Text("Action Btn 2"),onPressed:(){})
                ],
                title: Text("Title"),
                content: Text("Message body"),
);
```
- Output:
![actionbtnpadding.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628246534025/AGZZ9iR9Y.png)
- Without `buttonPadding`, output will be  :
- 
![actionbtnpadding2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628246602506/m5vbRW5Se.png)

---------------------------------------

### `backgroundColor`:
- This will give dialog surface a background color.
- Default value is  `ThemeData.dialogBackgroundColor`
- Example :
```
AlertDialog(
                backgroundColor: Colors.greenAccent,
                title: Text("Title"),
                content: Text("Message body"),
);
```
- Output :
- 
![bgcolor.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628246779193/H6fvMJOyL.png)

-------------------------------


### `actions`:
- This is an optional property. It is used to display a set of actions at the bottom of the dialog.
- Usually, it contains TextButton/ElevatedButton type of widget. For example: `Yes`, `No`, `Submit` type of buttons.
- It has a default padding of 8 pixels on each side.
- Example : 
```
AlertDialog(
                title: const Text('Are you sure ?'),
                actions: <Widget>[
                  ElevatedButton(onPressed: () {}, child: const Text('Yes')),
                  ElevatedButton(onPressed: () {}, child: const Text('No')),
                ],
);
```
- Output : 
- 
![actions.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628247335918/OhbTThgxi.png)

-------------------------------

### `actionsPadding`: 
- This property is used to add padding around the ButtonBar of the AlertDialog. 
- If actions are null, actionsPadding will not be used. 
- The default value of actionsPadding is EdgeInsets.zero (0,0,0,0).
- Example :
```
AlertDialog(
                title: const Text('Title'),
                content: Container(width: 100, height: 100, color: Colors.green),
                actions: <Widget>[
                  ElevatedButton(onPressed: () {}, child: const Text('Button 1')),
                  ElevatedButton(onPressed: () {}, child: const Text('Button 2')),
                ],
                actionsPadding: const EdgeInsets.symmetric(horizontal: 8.0),
);
```
- Output: 
- 
![actionpadding.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628247550897/t_TIv66gt.png)

-------------------------------------------

### `actionsOverflowButtonSpacing `:
- Sometimes` actions` overflows horizontally.
- If the widgets in `actions` do not fit into a single row, they are arranged into a column.
- And this property defines the spacing between those button widgets when it overflow.
- Example 
```
AlertDialog(
                actionsOverflowButtonSpacing: 10.0,
                title: const Text('Title'),
                actions: <Widget>[
                  ElevatedButton(onPressed: () {}, child: const Text('Button 1')),
                  ElevatedButton(onPressed: () {}, child: const Text('Button 2')),
                  ElevatedButton(onPressed: () {}, child: const Text('Button 3')),
                  ElevatedButton(onPressed: () {}, child: const Text('Button 4')),
                  ElevatedButton(onPressed: () {}, child: const Text('Button 5')),
                ],
                content:Container(width:300.0,height:200.0,color:Colors.greenAccent)
);
```
- Output :
- 
![actionverticlespacing.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628248991989/Nz_OgDl1K.png)

-------------------------------------------------

### `actionsOverflowDirection`:
- This defines how our buttons will be place vertically. 
- It has two options : 
1. `actionsOverflowDirection: VerticalDirection.up`: Which arranges the actions in an upward direction.
2. `actionsOverflowDirection: VerticalDirection.down` (default): Which arranges the actions in downward direction.
- Example 
```
AlertDialog(
                actionsOverflowDirection: VerticalDirection.up,
                actionsOverflowButtonSpacing: 10.0,
                title: const Text('Title'),
                actions: <Widget>[
                  ElevatedButton(onPressed: () {}, child: const Text('Button 1')),
                  ElevatedButton(onPressed: () {}, child: const Text('Button 2')),
                  ElevatedButton(onPressed: () {}, child: const Text('Button 3')),
                  ElevatedButton(onPressed: () {}, child: const Text('Button 4')),
                  ElevatedButton(onPressed: () {}, child: const Text('Button 5')),
                ],
                content:Container(width:300.0,height:200.0,color:Colors.greenAccent)
);
```
- Output :
- 
![actiondirectorn.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628248872605/UOtMvO0VT.png)
- Compare the previous `actionsOverflowButtonSpacing`s' results and this one. You can clearly see the difference.


----------------------------

- **THAT'S IT**. That's all you need to know about **AlertDialog**.
- Thank you for reading.

![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1628423079302/y1nbKg9h6.gif)

 > Previous Blog : Widget In Detail - [AbsorbPointer & IgnorePointer](https://dhruvnakum.xyz/flutter-widget-in-detail-absorbpointer-and-ignorepointer) 
