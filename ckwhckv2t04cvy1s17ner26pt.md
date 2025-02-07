---
title: "Answering The Frequently Asked Questions in Flutter Development #2"
datePublished: Sat Nov 27 2021 05:02:50 GMT+0000 (Coordinated Universal Time)
cuid: ckwhckv2t04cvy1s17ner26pt
slug: answering-the-frequently-asked-questions-in-flutter-development-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1637989212318/Jqr4gNczNl.png
tags: programming-blogs, dart, flutter, flutter-examples

---

- This is **Part #2** of the **Flutter FAQs ** series. In this series, I'm compiling all of the frequently asked questions that Flutter developers encounter while building an app.
- So let's get this party started.
---------
## 1. How to Auto-Complete TextField
- Filling out a form in an application is really tedious. We don't want to retype the same information in the form every time, such as Name, Email, Address, Phone Number, and so on. 
- So, as developers, we can auto-suggest the user when they are on a specific text field.
- To accomplish this, simply supply an array of AutofillHints into the **TextField** widget's `autofillHints` attribute.
- 
```
TextField(
    ....,
    decoration: InputDecoration(hintText: "Username")
    autofillHints: [AutofillHints.name] // or AutofillHints.email, AutofillHints.postalAddress...
)
```
----------
## 2. How to Refresh/Update AlertDialog
- If you've ever tried to update the state of dialogue by clicking a button within it, you'll notice that the state doesn't update. It's because when you call `setState`, the parent widget's build is updated. However, in our case, we opened a separate dialogue that is unrelated to the `build` approach. That is why it is not being updated.
- To update the dialogue, enclose your AlertDialog within the **StatefulBuilder** widget.
- You will gain access to the `setState` method, which will be used to update the state of the dialogue.
- Use StatefulBuilder to use setState within Dialog and just update Widgets within it.
- 
```
showDialog(
     context: context,
     builder: (context) {
       return StatefulBuilder(
            builder: (context, setState) {
                 return AlertDialog(
                      .......
                 );
            },
       );
    },
);
```
-------
## 3. How to call `async` function inside `initState`
- Often, when the screen first loads, we want to call a function. And we call it in `initState` because it is only called once when the screen loads. This is sufficient for a standard solution. However, if you execute an `async` function within it, `initState`  will throw an error.
- To resolve this issue, just build your async function outside of `initState` and call it inside `initState` as seen below:
- 
```
 @override
  void initState() {
    super.initState();
    loadDataFromAPI();
  }
  Future<void> loadDataFromAPI() async {    // ....  }
```
----------
## 4. How to *preload* Image 
- Sometimes, we'd like to preload certain photos before the screen load. On the first page, for example, we want a background image.
- However, retrieving that image from assets or the internet will take some time before it loads. Because the image only flashes/blinks after image fetch, this could be a negative user experience.
- You can use the `precacheImage` method in the `initState` to begin loading an image before your page is constructed.
- 
```
@override
  void initState() {
    precacheImage(new AssetImage('...')); // or NetworkImage('...'), etc.
    super.initState();
  }
```
---------
## 5. How to hide StatusBar
- By default, the Status bar is visible as shown in the below image:
- 
![statusbar.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1637944044211/YMrSVdtyR.png)
- If you want to hide it for some reason then simply paste the below code in the `main` method.
- 
```
import 'package:flutter/services.dart';
void main(){
    SystemChrome.setEnabledSystemUIMode(SystemUiMode.immersive);
    //....
}
```
- 
![statusbar2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1637943939618/xm-qvlrap.png)
----------
## Wrapping Up
- **I hope you found this article to be beneficial. If you have any questions related to Flutter, please leave them in the comments. I will try my best to answer it.**
- **Thank you for spending time reading this article. See you in the next article. So, until then...**
- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1637944134500/xZaO6KMPE.gif)
