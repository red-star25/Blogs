---
title: "Equatable in Flutter: A Complete Guide"
datePublished: Thu Sep 02 2021 04:29:24 GMT+0000 (Coordinated Universal Time)
cuid: ckt2filvx0a363js16hey4rpo
slug: equatable-in-flutter-a-complete-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1630556798706/_xEhe2S5q.png
tags: programming-blogs, dart, flutter, object-oriented-programming

---

## Comparing Two Objects in Manual Way
- While developing the Flutter application, we often wanted to compare two objects and check whether they are equal or not.
-  To do that, dart provides two methods `==` and `hashcode`.
- By `overriding` these methods we can compare our instances.
- Let's take an example and compare two objects by overriding these two methods.
- Example: **Comparing Two Car Objects Example**
- `Car.dart`
```
class Car {
  final String carName;
  final String carImage;

  const Car({required this.carName, required this.carImage});
}
```
- In `main.dart` I've created two `Car` objects
- 
```
final Car audi = Car(carName: "Audi", carImage: "assets/images/audi.png");
final Car bmw = Car(carName: "BMW", carImage: "assets/images/bmw.png");
```
- **UI of Car**
- 
```
@override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.amber,
      body: Center(
        child: Container(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: [
              CarWidget(
                carImage: audi.carImage,
                carName: audi.carName,
              ),
              SizedBox(
                width: 200,
                height: 50,
                child: ElevatedButton(
                  onPressed: () {
                    compareObjects(context);
                  },
                  child: Text("Compare"),
                ),
              ),
              CarWidget(
                carImage: bmw.carImage,
                carName: bmw.carName,
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```
- **Output** :
- 
![starter.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630246807003/Ta6Z9TEvY.png)

- Now Let's implement `Compare` function :
- 
```
  compareCars(BuildContext context) {
    if (audi == bmw) {
      ScaffoldMessenger.of(context)
          .showSnackBar(SnackBar(content: Text("YES, They are EQUAL")));
    } else {
      ScaffoldMessenger.of(context)
          .showSnackBar(SnackBar(content: Text("NO, They are not EQUAL")));
    }
}
```
- Call this function in `Compare` button
- 
```
ElevatedButton(
     onPressed: () {
         compareCars(context);
     },
    child: Text("Compare"),
),
```
- Now if we try to compare these two objects, we'll get `NO, They are not EQUAL` Scaffold message 
- 
![notequal.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630247036497/_GSGF9k53.png)
- **This seems fine**
- **But ** now let's create two same cars and compare :
- 
```
// Creating two same car
final Car audi = Car(carName: "Audi", carImage: "assets/images/audi.png");
final Car audi2 = Car(carName: "Audi", carImage: "assets/images/audi.png");
```
- 
![twosamecar.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630247232056/UzAMIRXFp.png)
- Now if we compare `audi` and `audi2`, what should be the output according to you?. Let's check!!
- 
```
compareCars(BuildContext context) {
    if (audi == audi2) {
      ScaffoldMessenger.of(context)
          .showSnackBar(SnackBar(content: Text("YES, They are EQUAL")));
    } else {
      ScaffoldMessenger.of(context)
          .showSnackBar(SnackBar(content: Text("NO, They are not EQUAL")));
    }
}
```
- **Output**
![samecarnotequal.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630247462971/X44a5B9xp.png)

- **Strange 🤔**!! It's still giving a **They are Not Equal** message. It's because under the hood Dart doesn't compare the objects by their value.
- Here the `audi` and `audi2` both objects are in different memory locations. It doesn't matter if they have exact same values. They both will be considered as different objects.
- So what we can do now?
- **Well**, Dart provides us two methods that we can override. `==` and `hashcode` methods.
- Let's implement those two methods in our `Car.dart` model class.
-  
```
class Car {
  final String carName;
  final String carImage;

  const Car({required this.carName, required this.carImage});

  @override
  bool operator ==(Object other) =>
      identical(this, other) ||
      other is Car &&
          runtimeType == other.runtimeType &&
          carName == other.carName &&
          carImage == other.carImage;

  @override
  int get hashCode => carName.hashCode ^ carImage.hashCode;
}
```
- What this `==` method do is, It will compare objects by their `type`, and `values`.
- Now if we click on the **Compare** button -
- 
![==.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630249920075/-vBhDsxuC.png)
- **It's Working.** But the problem is you have to compare each and every field of your model class manually in the `==`  method and also within the `hashcode` method.
- You can see how this can quickly become a hassle when dealing with complex classes. This is where `Equatable` comes in!

-----

## Using Equatable
- The `Equatable` simplify the above process by overriding `==` and `hashcode` for you.
- Let's install `equatable` package
- 
```
equatable: ^2.0.3
```
- Now all you have to do is to extend your class with **Equatable** and override a getter method `props`.
- 
```
import 'package:equatable/equatable.dart';
```
```
class Car extends Equatable {
  final String carName;
  final String carImage;

  const Car({required this.carName, required this.carImage});

  @override
  List<Object?> get props => [carName, carImage];
}
```
- `props` is a getter method that will return `List<Object>`. Here `Object` can be of any type (like : `int`,`double`, `list` etc). You have to simply return a list of all the objects that are available in your class (`carName` and `carImage` in our case).
- **THAT'S IT !!!!!!**
- 
![equatable.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630250539217/x-BELcD1c.png)
- >  **Note**: Equatable is designed to only work with immutable objects so all member variables must be final

## `EquatableMixin` :
- If your class is already extending anything then you can use `EquatableMixin` mixin.
- 
```
class Car extends Object with EquatableMixin {
  final String carName;
  final String carImage;

  const Car({required this.carName, required this.carImage});

  @override
  List<Object?> get props => [carName, carImage];
}
```
-----
- `Equatable` also provide one additional functionality i.e `stringify` method.
- If you want to override `toString` method simply override the `stringify` method -
- 
```
class Car extends Object with EquatableMixin {
  final String carName;
  final String carImage;

  const Car({required this.carName, required this.carImage});

  @override
  List<Object?> get props => [carName, carImage];

  @override
  bool get stringify => true;
}
```
- This will override `toString` method with all the fields which we have in our class.

------

%[https://pub.dev/packages/equatable]

--------
- **Thank you for reading. See you in the next article**
- **Comments and Feedbacks are welcomed 🙂**
- **Until then **....
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1630251476299/F-FXj2Ru1.gif)
