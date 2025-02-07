---
title: "Understanding Streams: Everything you need to know"
datePublished: Thu Aug 26 2021 04:28:29 GMT+0000 (Coordinated Universal Time)
cuid: ckssfeh4n060zdbs11pzf6t19
slug: understanding-streams-all-you-need-to-know
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1632809531909/T3cUhP4rO-.png
tags: programming-blogs, programming, dart, asynchronous, flutter

---

## Introduction
- **Streams ** are very complex and hard to understand. In this blog, I'll try to explain this concept with some examples.
- For beginners, this concept should be clear in their mind, because most of the time our application is dealing with asynchronous data, For example: Fetch data from API, DB, etc.
- Before start coding and implementing Stream let's first understand what actually a Stream is.
- 
![Let'SGetStartedGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629798086129/Ir9V4HcKC.gif)
------------------------
## What are Streams?
- A streams are nothing but a continuous flow of Data.
- It provides an **asynchronous** sequence of Data. And because of the **asynchronous** type, we have to use `async` and `await`.
- The `async` and `await` are keywords that are used to define an **asynchronous** function.
- 
```
someAsyncFunction () async{
   await getData();
}
```
- There are two main ends associated with Steams: **1.Sink** and **2.Source**.
- The **Sink** is the end from where we can add data inside the **Streams** and
- The **Source** is the end from where we can get the data from the **Streams**.
- 
![Stream.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629726184937/jBhn1EX1Q.png)
- If you've not understood then, you can think of a **Streams** like a water pipe, where the flow of water (**Data**) is continuously flowing from one end (**Sink**) and coming out from the second end (**Source**).
- 
![FrozenPipesGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629798345613/jGP07kdEM.gif)
- There are basically two types of **Streams**:
- **1. Single Subscription Stream** and 
- **2. Broadcast Stream**
- The **Single Subscription Streams** allow only one `listener` to listen to the stream. If you try to listen to the same stream again, you'll get an exception. The **Broadcast Stream** allows more than one `listener` to listen to the same stream.
- A `listener` listens to the particular event of the stream. Whenever data flows in the Streams the `listener` will recognize that event and listens to it.
- If there are no data flowing inside the Streams then it gets destroyed.
- Now let's write some code to understand how actually we can use the **Streams**.
------------------------
##  How to use Streams :
- To use Streams we have to make the function async generator (**async* **).
- The `async*` is used when a function returns multiple future values one at a time.
- When this function is called the **Stream** is created. Now to return the data from this function we have to use `yield` or `yield*`.
- **yield** is like **return** but the difference is `yield` doesn't terminate the function immediately.
- Let's take one simple example :
- 
```
Stream<int> numberGenerator() async*{
  for(int i=0; i<10; i++){
    await Future.delayed(Duration(milliseconds: 1000));
    yield i;
  }
}
```
```
void main() {
  final myStream = numberGenerator();  
  final subscription= myStream.listen(                                
    (data)=>{
      print("Number: $data")
    }
  );
}
```
- 
![simplecounterstream.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629735008411/VD_S6z-tu.gif)
- The `subscription` is a type of `StreamSubscription`. When you listen on a `Stream` using `Stream.listen`, a `StreamSubscription` object is returned.
- The `subscription` provides events to the `listener`, and holds the callbacks used to handle the events. The `subscription` can also be used to unsubscribe from the events, or to temporarily pause the events from the stream.
- Here when `subscription` starts listening to the `myStream`, one by one all the integer values start flowing into the stream.
- And then it will `yield` that `int` values one by one asynchronously.
- ### `listen()` properties:
- #### **onData()**: 
- On each data event from this stream, **onData** handler is called. If **onData ** is `null`, nothing happens. 
- Example :
- 
```
void main() {
final myStream = numberGenerator();  
final subscription = myStream.listen(                                
  (data)=>{                             // data handler function
    print("Number: $data")
  }
);
}
```
- #### **onDone()** : 
- Called when stream completes all its events.
- 
```
void main() {
  final myStream = timedCounter();
  final subscription = myStream.listen(
    (data){
      print("Number: $data");
    },
    onDone: () {
      print("You've reached at the end");
    },
  );
}
```
```
Stream<int> timedCounter() async* {
  int i = 0;
  while (i <= 5) {
    await Future.delayed(Duration(milliseconds: 1000));
    yield i++;
  }
}
```
- As you can see as soon as the stream completes its listening, `onDone` function is executed.
- 
![onDone.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629783757543/sMKWmvYxp.gif)
- #### **onError(error)**: 
- Subscription is automatically canceled when an error occurred.
- 
```
void main() {
  final myStream = timedCounter();
  final subscription = myStream .listen(
    (data){
      print("Number: $data");
    },
    onDone: () {
      print("You've reached at the end");
    },
    onError: (e){
      print("Error: $e");
    },
  );
}
```
```
Stream<int> timedCounter() async* {
  int i = 0;
  while (i <= 5) {
    await Future.delayed(Duration(milliseconds: 1000));
    if(i ==2){
      throw Exception("Error Occurred");
    }
    yield i++;
  }
}
```
- As soon as number `2` is encountered we've thrown an `error` and `onError` function executed.
![onError.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629737061205/d3s8oNEl7.gif)
- #### cancelOnError :
- If `cancelOnError` is `true`, the subscription is automatically canceled when the first `error` event is delivered. The default is `false`.
- We can see in the above example that even if the `error` is encountered, the stream has not stopped its execution. It executed `onDone` too. To close the stream subscription as soon as the `error` is encountered we have to give `true` value to 
`cancelOnError`.
- 
```
void main() {
  final myStream = timedCounter();
  final subscription = myStream.listen(
    (data){
      print("Number: $data");
    },
    onDone: () {
      print("You've reached at the end");
    },
    onError: (e){
      print("Error: $e");
    },
    cancelOnError: true
  );
}
```
```
Stream<int> timedCounter() async* {
  int i = 0;
  while (i <= 5) {
    await Future.delayed(Duration(milliseconds: 1000));
    if(i ==2){
      throw Exception("Error Occurred");
    }
    yield i++;
  }
}
```
- 
![cancelOnError.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629737991868/0_SNmX9Za.gif)
------------
### Manipulating Streams :
- We can manipulate the stream data on the fly.
- We can chain up methods such as `map`, `where`, `take` and `expand`.
- We can chain up all the methods that are available in the `iterable`(like, `elementAt`, `cast`, `contains`, `any`, etc) to manipulate the data of the stream
- ### map() :
- 
```
void main() {
  final myStream = timedCounter()
    .map((data)=> 'Number : ${data*2}')
    .listen(print);
}
```
```
Stream<int> timedCounter() async* {
  int i = 0;
  while (i <= 5) {
    await Future.delayed(Duration(milliseconds: 1000));
    yield i++;
  }
}
```
- 
![mapStream.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629739993722/BfWUV_41l.png)
- ### where() :
- 
```
void main() {
  final myStream = timedCounter()
    .where((data) => data % 2 == 0)
    .map((data)=> 'Number : $data')
    .listen(print);
}
```
```
Stream<int> timedCounter() async* {
  int i = 0;
  while (i <= 5) {
    await Future.delayed(Duration(milliseconds: 1000));
    yield i++;
  }
}
```
- 
![whereStream.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629740029323/XgITj5Fta.png)

------------------------
## Types of Stream :
- ### Single Subscription Stream :
- The Single Subscription Stream as the name suggests, only allows one listener to listen to the stream. 
- This type of stream is basically used in reading a file, receive a web request, etc. It's because we want a continuous flow of data in the correct order and without any errors.
- You can listen to this stream by the `listen()` method as we've seen in the above examples.
- This stream can listen only once. Listening again to this stream will cause an error.
- Example :
- 
```
void main() {
  final myStream = timedCounter();
  final subscription = myStream.listen(
      (data){
        print("Number: $data");
      },
   );
}
```
```
Stream<int> timedCounter() async* {
  int i = 0;
  while (i <= 5) {
    await Future.delayed(Duration(milliseconds: 1000));
    yield i++;
  }
}
```
- 
![singlesubstream.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629784676453/Wam-x-4xi.png)
- Listening with two subscribers will cause an error
- 
```
void main() {
  final myStream = timedCounter();
  final subscriber1 = myStream.listen(
      (data){
        print("Sub 1 : Number: $data");
      },
   );
  final subscriber2= myStream.listen(
        (data){
        print("Sub 2 : Number: $data");
      },
  );
}
```
```
Stream<int> timedCounter() async* {
  int i = 0;
  while (i <= 5) {
    await Future.delayed(Duration(milliseconds: 1000));
    yield i++;
  }
}
```
- 
![multisub.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629784624315/AaSMd797Q.png)
- ### Broadcast Stream :
- When more than one subscribers want to listen to one particular stream, we have to make that stream **broadcast** stream.
- `asBroadcastStream()` is used to make any stream a **Broadcast Stream**.
- Any subscriber can start listening to events as soon as they subscribe to it.
- Example :
- 
```
void main() {
  final myStream = timedCounter().asBroadcastStream();
  final subscriber = myStream.listen(
      (data){
        print("Sub 1 : Number: $data");
      },
   );
  final subscriber2 = myStream.map(
      (data)=> 'Sub 2 : Number : ${data*2}'
     ).listen(print);
}
```
```
Stream<int> timedCounter() async* {
  int i = 0;
  while (i <= 5) {
    await Future.delayed(Duration(milliseconds: 1000));
    yield i++;
  }
}
```
- 
![broadcaststream.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629785076062/ecB2FH0SZ.gif)

------------------------------

## Creating your Own Stream
- Most of the time we use the stream provided by the network libraries, file libraries, state management, etc.
- But we can create our own stream by using **StreamController**.
- **StreamController** gives you the ability to add your own events from anywhere.
- To use **StreamController** you have to import `dart:io` package inside your application.
- 
```
import 'dart:async';
```
```
void main() {
  final _streamController = StreamController<int>();   // initialization of StreamController
  int _number = 1;

  addData() {
    Timer.periodic(Duration(seconds: 1),(_) {
      _streamController.sink.add(_number);    // adding data to stream
      _number++;
    });
  }
  
  addData();
  
  Stream<int> myStream = _streamController.stream;  //creating a stream
  final subscription = myStream.listen(                         // listening to the stream
    (data) => {
      print(data)
    },
  );
}
```
- 
![streamcontroller.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629787713317/XnnGk0fxS.gif)
- Above stream will add data infinitely.
- If you want to close the stream at a certain point, you can do something like this :
- 
```
import 'dart:async';
```
```
void main() {
  final _streamController = StreamController<int>();
  int _number = 1;

  addData() {
    Timer.periodic(Duration(seconds: 1),(_) {
      if(_number == 5){
        _streamController.close();      // closing a stream
        return;
      }
      _streamController.sink.add(_number);
      _number++;
    });
  }
  
  addData();
  
  Stream<int> myStream = _streamController.stream;
  final subscription = myStream.listen(
    (data) => {
      print(data)
    },
    onDone: (){
      print("All data received");    // called when stream is closed
    }
  );
}
```
- 
![closestream.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629788013704/YHNDfIkItS.gif)
- You can also listen to different events like `onListen`, `onPause`, `onCancel`, `onResume` using **StreamController**.
- 
```
StreamController<int>(
      onListen:  ...,
      onPause: ...,
      onResume: ...,
      onCancel: ...
);
```

------------------
## StreamBuilder in Flutter
- We are often dealing with asynchronous data in our app.
- Flutter provides **StreamBuilder** which listens to the event flowing from the stream.
- For every new event it rebuilt the widget giving them the latest event to work with.
- You can give your stream to StreamBuilder's `stream` property.
- 
```
StreamBuilder(
    stream: myStream
    //...
)
```
- The `builder` property is used to return a Widget that we want to display on the screen.
- It has `context` and a `snapshot` as a parameter
- 
```
StreamBuilder(
    stream: myStream,
    builder: (context, snapshot) {
        return Container()
    }
)
``` 
- The `initialValue` property of the StreamBuilder is used to give the initial data to the widget while it's waiting for the first event.
- You can check if the `snapshot` has data or not, has any error or not and also the connection state :
- 
```
StreamBuilder(
    stream: myStream,
    builder: (context, snapshot) {
        if(!snapshot.hasData) return CircularProgressIndicator()   //checking is there any data
        if(snapshot.hasError) return Text("Something went wrong") //cheking for the error
        if(snapshot.connectionState == ConnectionState.done){} // or `waiting`,`none`, `active`
        return Container()
    }
)
```
- Let's take one simple example :
- In the below example, there is one container and a button underneath it.
- When the button is pressed we are adding a new data(Color)to the stream.
- 
```
class FlutterStreamBuilder extends StatefulWidget {
  @override
  _FlutterStreamBuilderState createState() => _FlutterStreamBuilderState();
}
```
```
class _FlutterStreamBuilderState extends State<FlutterStreamBuilder> {
  final colorStream = StreamController<Color>();  

    // generate new Color randomly
   Color generateColor() {
    final random = Random();

    return Color.fromARGB(
      255,
      random.nextInt(255),
      random.nextInt(255),
      random.nextInt(255),
    );
  }
  
  // add Color to `colorStream`
  addData(){
    colorStream.sink.add(generateColor());
  }
  
   @override
  void initState() {
    addData();
    super.initState();
  }
  
  @override                     
  void dispose() {
    colorStream.close(); // To prevent memory leak, Make Sure you close the Stream.
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SizedBox.expand(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          crossAxisAlignment: CrossAxisAlignment.center,
          children: [
            StreamBuilder(
                stream: colorStream.stream,
                builder:
                    (BuildContext context, AsyncSnapshot<dynamic> snapshot) {
                  if (!snapshot.hasData) {
                    return Center(child:CircularProgressIndicator());
                  }

                  if (snapshot.connectionState == ConnectionState.done) {}

                  return Container(
                    height: 220,
                    width: 220,
                    color: snapshot.data,
                  );
                }),
            SizedBox(height:30),
            ElevatedButton(onPressed: addData, child: Text("Click"))
          ],
        ),
      ),
    );
  }
}
```
- 
![streambuilder.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629797953880/zGoO-lb7A.gif)


--------------------------------
## Wrapping Up
- Thanks for reading. Hope you liked it.
- Make sure you leave feedback in the comments 🙂.
- 
![PeaceOutImOutGIF (2).gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629799866689/4c6eCMY6R.gif)
