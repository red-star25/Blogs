---
title: "Iterable & Iterator in Flutter & Dart"
datePublished: Tue Aug 24 2021 04:58:33 GMT+0000 (Coordinated Universal Time)
cuid: ckspllgtc0as6wps1cde675d8
slug: iterable-and-iterator-in-flutter-and-dart
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1629781338876/gx_KcaJYl.png
tags: programming-blogs, dart, flutter, coding

---

## Iterable 
- If you are familiar with **Dart**/**Flutter** you are knowingly or unknowingly using **Iterable** in your application or program.
- You might have come across **objects** like `List`, `Map`, and `Set` when building an application.
- These are nothing but **Iterable**. You can verify this by taking a look into the implementation of these collections.
- **List** :
- 
![listiterable.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629449681556/_mdGvo4Fj.png)
- **Set** :
- 
![setiterable.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629449811003/iYJ93fn5hI.png)
- An **Iterable** as the name suggests, it has something to do with **iteration**.
- The definition of **Iterable** given by Dart is :
> An Iterable is a collection of elements that can be accessed sequentially
- If we look at the implementation of the **Iterable**, we can see that **Iterable** is an **abstract** class.
- 
![iterableabstract.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629448533377/0ZuqZ-vYN.png)
- That means we cannot instantiate the **Iterable** class.
- But we can create a new **Iterable** by creating **List**, **Set**, **Map**. For example :
- 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629454420022/HLOBEbYLJ.png)
- We cannot access the value by `index`, like `numbers[index]`. It's because `Iterable` doesn't have `[ ]` operator like **List**.
- Let's try to access the element of the `Iterable` by `[ ]`, And see what error it throws:
- 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629454440212/NC36PTpt3.png)
- ![[notdefine].png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629450579721/Gf8Ke6z0i.png)
- As expected it threw an error that says **operator [ ] is not defined in Iterable class**.
- **Iterable** has many useful **properties** and **methods** available.
- As `List`, `Set` is Implementing **Iterable** , All the methods that are available in **Interable** are also accessible in `List` and `Set`.
- A `Map` is different than `List` and `Set`, because it contains `key` : `value` pairs. We cannot directly loop through the `Map` variable as we're doing in `Set` and `List`. Because `Map` is not implementing `Iterable`
- 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629454208958/blTIti9Nq.png)
- 
![mapiterableerror.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629452436797/R_M4G1Pxl.png)
- **Map** has `keys` and `values` **Iterables** inside it.
- **Keys Iterable**
![keyiterable.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629451844523/neqp6R1bKn.png)
- **Values Iterable**
- 
![valueiterable.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629451871155/1daJ7nlXe.png)
- So to iterate over the `Map` we can do something like :
- 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629454185459/uhh_Ax4Pl.png)

-------------------
## Iterator 
- In simple terms **Iterator** is a single element of a collection that we can get one at a time.
- **Iterator** is an `Interface`. The `for-in` loop we've used in the above examples is using this `Iterator` interface under the hood.
- The thing is **Iterable** doesn't know how to iterate over the collection. That is why **Iterable** has an `Iterator` getter inside it. 
- ![iterableiterator.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629453378982/pqEvjP9t6.png)
- Its job is to move sequentially through all the elements of the iterable.
- All **iterables ** have an **iterator**
- 
![listiterator.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629453593969/ZNxUNEqpp.png)
- 
![setierator.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629453610515/XobrBuSlH.png)
- The **Iterator** has a method called `moveNext()`, which returns a boolean value.
- If it returns `true` then it means that iterable contains the next element.
- if it returns `false` then it means that there are no further elements.
- **Iterator** has one very important getter called `current`. Which gives the `current element` of the iterable.
- Example :
- 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629454154191/p7OgOLyVh.png)

------------------------------------

## Properties of Iterable :
- ### `first` & `last`:
- `first` returns the first value/element from the `Iterable`.
- `last` returns the last value/element from the `Iterable`.
- `first` Example :
```
void main() {
   final List<String> listOfCar = ["Audi","BMW","Ferrari","Mercedes"];
   print(listOfCar.first);
}
```
- 
![first.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629612506890/mj-Pydm8p.png)
- For accessing the `first` element from `Map` :
- 
```
void main() {
   final Map<String,dynamic> mapOfNumbers = 
 {"0":"Zero","1":"One","2":"Two","3":"Three"};
   print(mapOfNumbers.values.first);
}
```
- 
![mapfirst.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629612737468/-kgDiAvLZ.png)
- `last` Example :
- 
```
   final List<String> listOfCar = ["Audi","BMW","Ferrari","Mercedes"];
   print(listOfCar.last);
```
- 
![last.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629613180103/q63QhOIcD.png)
---------------
- ### `isEmpty` & `isNotEmpty`:
- `isEmpty` returns `true` if `Iterable` is empty, otherwise `false`.
- `isNotEmpty` returns `true` if `Iterable` is not empty, otherwise `false`
- 
```
void main() {
  final List<String> listOfCar = ["Audi","BMW","Ferrari","Mercedes"];
  print(listOfCar.isEmpty);
}
```
- 
![isEmpty.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629612518927/j0Yh2m4R4.png)
- Same for the `Map`
- 
```
void main() {
   final Map<String,dynamic> mapOfNumbers = 
 {"0":"Zero","1":"One","2":"Two","3":"Three"};
   print(mapOfNumbers.isEmpty); // false
}
```


-------------------------
- ### `length` :
- Returns the total number of elements/values present in the `Iterable`.
- 
```
void main() {
   final Map<String,dynamic> mapOfNumbers = 
 {"0":"Zero","1":"One","2":"Two","3":"Three"};

   final List<String> listOfCar = ["Audi","BMW","Ferrari","Mercedes"];

   print("List: "+listOfCar.length.toString());
   print("Map: "+mapOfNumbers.length.toString());
}
```
- 
![length.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629613335462/_0UG_ZoXh.png)

-----------------------------
- ### `runtimeType` :
- Returns the type of the object.
- 
```
void main() {
   final Map<String,dynamic> mapOfNumbers = 
 {"0":"Zero","1":"One","2":"Two","3":"Three"};

   final List<String> listOfCar = ["Audi","BMW","Ferrari","Mercedes"];

   print(listOfCar.runtimeType);
   print(mapOfNumbers.runtimeType);
}
```
- 
![runtimeType.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629613479112/7Q3CkFteO.png)

----------------------------
- ### `single` :
- If the Iterable has only one element inside it, then `single` returns that value/element.
- 
```
void main() {
   final List<String> listOfCar = ["Audi"];
   print(listOfCar.single);
}
```
- 
![single.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629615997859/1N3iiS2kG.png)
- If there are more than one element then it will throw an error.

----------------------
## Methods of Iterable :

- ### `elementAt(index)` :
- As we've seen in the explanation of `Iterable` that we cannot access the element of `Iterable` by `[ ]`. Because `Iterable` doesn't have `[ ]` defined.
- So we can use `elementAt()` method to access any element from the `Iterable`.
- 
```
void main() {
   final Map<String,dynamic> mapOfNumbers = 
 {"0":"Zero","1":"One","2":"Two","3":"Three"};

   final Iterable<String> listOfCar = ["Audi","BMW","Ferrari","Mercedes"];

   print(listOfCar.elementAt(0));
   print(mapOfNumbers.values.elementAt(0));
}
```
- 
![elementAt.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629616292473/NUZeQqfAu.png)

------------------------
- ### `contains(element)` :
- Returns `true` if the `Iterable` contains the element passed inside the `contains()` method.
- 
```
void main() {
   final Map<String,dynamic> mapOfNumbers = 
 {"0":"Zero","1":"One","2":"Two","3":"Three"};

   final List<String> listOfCar = ["Audi","BMW","Ferrari","Mercedes"];

   print(listOfCar.contains("BMW"));
   print(mapOfNumbers.values.contains("Five"));
}
```
- 
![contains.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629616468410/4WOihEB9n.png)

----------------------------
- ### `firstWhere()`
- This will return the **first encountered ** element which satisfies the condition given to the function.
- The function must return `boolean` value.
- This method takes two things: 1. The function which returns the value if a certain condition is satisfied & 2. `orElse` function which will be called when no condition is satisfied.
- 
```
void main() {
   final List<String> listOfCar = ["Audi","Audi A5","BMW","Ferrari","Mercedes"];
   print(listOfCar.firstWhere((element)=> element.startsWith("Au")));
}
``` 
- 
![firstwhere.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629617077192/gYGd0cGcj.png)
- `orElse` 
```
void main() {
   final List<String> listOfCar = ["Audi","Audi A5","BMW","Ferrari","Mercedes"];
   print(listOfCar.firstWhere((element)=> element.startsWith("Zu"),orElse: ()=> "No Element Found"));
}
```
- 
![orElseFirstWhere.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629617153567/3RRLC0-bl.png)

---------------------------
- ### `where()`
- Takes `boolean` function. 
- This function will iterate over all the elements and checks if the condition given to the function is satisfied on that element.
- 
```
void main() {
   final List<String> listOfCar = ["Audi","Audi A5","BMW","Ferrari","Mercedes"];
   print(listOfCar.where((element)=> element.length > 4));
}
``` 
- 
![where.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629617627797/toOJDIkfs.png)

- `Map`:
- 
```
void main() {
   final Map<String,dynamic> mapOfNumbers = 
 {"0":"Zero","1":"One","2":"Two","3":"Three"};
   print(mapOfNumbers.values.where((element)=> element.length > 3));
}
```
- 
![wheremap.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629620081813/x1Wfb3enQ.png)

--------------------------

- ### `toSet()` :
- Used to convert from type `T` to `Set`, where `T` can be : `List`,`Map` etc.
- The `Set` will remove duplicate element from previous iterable.
- 
```
void main() {
   final List listOfCar = ["Audi","Audi","BMW","Ferrari","Mercedes"];
   print(listOfCar.toSet());
}
```
- 
![toSet.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629620658138/Awwhje2ui.png)

--------------------------------

- ### `toList()` :
- Used to convert any iterable to `List`.
- Takes one optional argument `growable`. If `true` we can further `add`  elements in list, otherwise `add()` will not work.
- 
```
void main() {
   final Set<String> setOfCar = {"Audi","BMW","Ferrari","Mercedes"};
   print(setOfCar.toList());
}
```
- 
![toList.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629621127407/nlOI-lSho.png)
- `growable : true` (default) :
- 
```
void main() {
   final Set<String> setOfCar = {"Audi","BMW","Ferrari","Mercedes"};
   final List listOfCar = setOfCar.toList();
   listOfCar.add("Jeep");
   print(listOfCar);
}
```
- 
![growabletrue.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629621238972/XL2QFKGkH.png)
- `growable : false` : 
- 
```
void main() {
   final Set<String> setOfCar = {"Audi","BMW","Ferrari","Mercedes"};
   final List listOfCar = setOfCar.toList(growable: false);
   listOfCar.add("Jeep");
   print(listOfCar);
}
```
- 
![growablefalse.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629621269665/X5A6j2IqL.png)
- As you can see `add` is not working now.

---------------------------

- ### `takeWhile()` :
- This will return every element in a list from index 0 to the element that first satisfies the condition.
- 
```
void main() {
   final List<String> listOfCar = ["Audi","Audi A5","BMW","Ferrari","Mercedes","Audi A3"];
   final fileteredList =  listOfCar.takeWhile((element) => element.startsWith("Au"));
   print(fileteredList);
}
```
- 
![takeWhile.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629621644470/QyMhenQg-.png)

--------------------

- ### `take(int count)` : 
- This will return every element in a list from index 0 to the index specified in this method.
- 
```
void main() {
   final List<String> listOfCar = ["Audi","Audi A5","BMW","Ferrari","Mercedes","Audi A3"];
   final fileteredList =  listOfCar.take(3);
   print(fileteredList);
}
```
- 
![take.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629621859705/9L1f8hRFX.png)

-----------------------------

- ### `skipWhile()`:
- Returns an iterable that skips leading elements while the provided predicate is satisfied.
- 
```
void main() {
   final List<String> listOfCar = ["Audi","Ferrari","BMW","Mercedes","Audi A3"];
   final fileteredList =  listOfCar.skipWhile((element)=> element.endsWith("i"));
   print(fileteredList);
}
```
- 
![skipwhile.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629622151935/em3U5NzRk.png)

--------------------------

- ### `skip(int count)` :
- This will skip every element in a list from index 0 to the index specified in this method and returns the remaining element.
- 
```
void main() {
   final List<String> listOfCar = ["Audi","Ferrari","BMW","Mercedes","Audi A3"];

   final fileteredList =  listOfCar.skip(3);

   print(fileteredList);
}
```
- 
![skip.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629622281575/srSiu3lay.png)

--------------------------------------
- ### `singleWhere()` : 
- Returns the single element that satisfies a given condition.
- If no element is found this method will give an error. To handle this error using `orElse`
- This will also throw an error if any duplicate value is found.
- 
```
void main() {
   final List<String> listOfCar = ["Audi","Ferrari","BMW","Mercedes"];

   final fileteredList =  listOfCar.singleWhere((element)=> 
 element.startsWith("Au"),orElse:()=> "No Element Found");

   print(fileteredList);
}
```
- 
![singleWhere.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629622598148/FQkyg-Qpu.png)

------------------------
- ### `reduce()`:
- This will reduce a given `iterable` to a single value by combining elements of the `iterable` using a provided function.
- The iterable must have at least one element. If it has only one element, that element is returned.
- 
```
void main() {
  final List<int> listNumber = [1,2,3,4];
  final reduced =  listNumber.reduce((value,element){
    print("value: "+value.toString());
    print("element "+element.toString());
    return value+element;
  });
  print("total: "+reduced.toString());
}
```
- 
![reduce.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629623372660/V6oTvtUCy.png)

----------------------------------

- ### `map()` :
- Returns a brand new list.
-  The function defined in `map` will run on each element.
- After that new list will be returned.
- 
```
void main() {
   final List<int> listNumber = [1,2,3,4];
   final filteredList = listNumber.map((element)=> element += 1);
   print(filteredList);
}
```
- 
![map.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629623799418/lFJCpGUEo.png)

---------------------
- ### `lastWhere()` :
- Returns the last element that satisfies the given condition.
- 
```
void main() {
   final List<int> listNumber = [1,2,3,4];
   final fileteredElement =  listNumber.lastWhere((element)=> element.isEven);
   print(fileteredElement);
}
```
- 
![lastWhere.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629623964381/fJEL_d4UJ.png)

------------------------
- ### `join()` :
- Joins every element of the iterable with a given `separator` and returns it as String.
- 
```
void main() {
   final List<int> listNumber = [1,2,3,4];
   final fileteredElement =  listNumber.join(",");
   print(fileteredElement);
}
```
- 
![join.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629624176284/SsHJOkQrkr.png)

----------------------------
- ### `forEach` :
- The function defined inside `forEach` will run on every element of the iterable.
- The difference between `map` and `forEach` is `forEach` doesn't return a new list whereas `map` does.
- 
```
void main() {
   final List<int> listNumber = [1,2,3,4];
   listNumber.forEach((element)=> print(element * 2));
}
```
- 
![forEach.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629624427339/4up1cRBjO.png)

-----------------------------

- ### `followedBy()` : 
- If you want to add new `iterable` inside your current `iterable` then you can use `followdBy()` by passing your `iterable` inside it.
- 
```
void main() {
   final List listOfFruits = ["Apple","Banana","Carrot"];
   final newFruitList = listOfFruits.followedBy(["Dates","Emu"]);
   print(newFruitList);
}
``` 
- 
![followedBy.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629624742123/hPl3hvWSs.png)

--------------------------------
- ### `fold`:
- It is the same as the `reduce` method. 
- It reduces an `iterable` to a `single` value by iteratively combining each element of the collection with an existing value.
- 
```
void main() {
   final List<String> listOfFruits = ["Apple","Banana","Carrot"];
   listOfFruits.fold(0, (value, element) {
     print("value: "+value.toString());
     print("element: "+ element.toString());
     return value + element.length;
  });
}
```
- 
![fold.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629625787962/wpZjaa0CN.png)
- Difference between `reduce` and `fold` is: `reduce` can only be used on non-empty collections with functions that return the same type as the types contained in the collection whereas `fold` can be used in all cases.
- We cannot compute the sum of the length of all strings in a list with `reduce` but you can use `fold` to do that.

--------------------------
- ### `expand` :
- If you have nested `iterables` inside one main `iterable` and you want to extract out those iterables into one single iterable then you can use `expand` to do this.
- 
```
void main() {
   final nestedList = [["Apple","Banana","Carrot"],[1,2,3],[true,false]];
   final flattenedList = nestedList.expand((list)=>list);
   print(flattenedList);
}
```
- 
![expand.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629626209864/FclzDt4gV.png)
- 
```
void main() {
   final listOfFruit = ["Apple","Banana","Carrot"];
   final duplicateFruits = listOfFruit .expand((element)=>[element,element]);
   print(duplicateFruits );
}
```
- 
![expand2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629626410229/HefFhqc9G.png)

-------------------------
- ### `every()` : 
- This method returns a boolean depending upon whether all elements satisfies the condition or not.
- 
```
void main() {
   final listOfFruits = ["Apple","A Banana","A Carrot"];
   final filteredList = listOfFruits.every((element) => element.startsWith("A"));
   print(filteredList);
}
```
- 
![every.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629626596552/Nw5yy5AqU.png)
---------------------------------
- ### `any()` :
- Returns `true` if any element satisfies the given condition, otherwise `false`.
- 
```
void main() {
   List<int> listOfNumbers = [11,23,3,45,5];
   print(listOfNumbers.any((element)=> element.isEven));
}
```
- 
![any.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629627666643/aHgbpH-Dc.png)

---------------------
- ### `cast()`: 
- This will return a new list with a given `castType` so that you can use it in places where the analyzer expects `Iterable<Type>`.
- This is a** very rarely** used method.
- **Remember** this will not cast an element of the `iterable`.
- It only gives an illusion to the analyzer that it got that `type` that it wanted.
- 
```
void main() {
   List<num> listOfNumbers = [5, 20, 12.5];
   List<double> castedDoubleList = listOfNumbers.cast<double>();
  
   print("casted list: "+castedDoubleList.toString());
   print("casted list type: "+castedDoubleList.runtimeType.toString());
   print("casted list element type: ");
   castedDoubleList.forEach((element)=> print(element.runtimeType)); 
}
```
- 
![cast.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629627271468/mVi9UXR7b.png)
- We can use this `castedDoubleList` if any function requires it. For example: 
- 
```
void main() {
   List<num> listOfNumbers = [5, 20, 12.5];
   List<double> castedDoubleList = listOfNumbers.cast<double>();
  
   reverseDoubleList(castedDoubleList);
}
```
```
reverseDoubleList(List<double> doubleList){
   print(doubleList.reversed);
}
```
- 
![cast2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629627466872/9ltSnaU1F.png)


-------------------------

## Wrapping Up
- These all are very useful methods and properties which are very handy during the development.
- Hope you liked it. Thanks for reading.
- Comments and Feedbacks are welcomed 🙂
- ![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629628001148/xOMlscPud.gif)
