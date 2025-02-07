---
title: "FlutterGen: Manage Assets Like a PRO!!"
datePublished: Mon Jun 06 2022 06:05:58 GMT+0000 (Coordinated Universal Time)
cuid: cl42bxrnb025gpmnv801h1f3c
slug: fluttergen-manage-assets-like-a-pro
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1654425132064/Omycx0wPe.png
tags: programming-blogs, dart, flutter, beginners, codegeneration

---

## The Problem
- In any application, images, fonts, color, etc are crucial. However, managing them might be difficult at times.
- For example, if we require a new picture, we must first update the pubspec file, and then supply the entire raw path as below
```
Image.asset('assets/image/some_image.png)
```
- Because we're supplying a raw string here, there's a larger risk of typos; this approach isn't advised for production-level applications.
- Another issue is Code Repetition: If you require this picture in another location, you'll have to rewrite the entire route. This also makes the code more difficult to read.
- So, what's the best way to go about it? We may, however, specify the constant for all of these assets in a single class, as seen below.
```
class AppConstants {
    static const image1 = 'assets/image/some_image.png';
}
```
- This eliminates the problem of typos and code readability, as well as the necessity to mention the entire route again.
```
Image.asset(AppConstants.image1)
```
- That's great, but there's an issue. What if there are hundreds of photos, colours, and other factors to consider? This is going to take a long time.
- We need something that can handle all of these asset-related things for us automatically in order to swiftly build the constants. So we don't have to write the boilerplate code again and over.

-------

## The Solution
- In order the solve the above problem, we are going to make use of one package, which will help us by managing our assets automatically.
- And the package, which will do this is named [flutter_gen](https://pub.dev/packages/flutter_gen)


![logo.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1654424481390/E6Pb8mm9y.jpg align="left")

 ### Installation
- In order to install this package, head over to your OS specific terminal and run the below command :

```
dart pub global activate flutter_gen
```

---------

### Adding Dependencies
- Now after the successful installation, head over to your flutter project, and the following dependencies inside the pubspec.yaml file.

```
dev_dependencies:
  build_runner:
  flutter_gen_runner:
```

--------

### Adding and Specifying Assets
- In order to use this package, first of all, we must have an assets folder inside the root directory.
- Let's add some images inside the assets folder


![added.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1654424540546/RbRrXvehH.png align="left")

- After adding images to the assets folder, head over to pubspec.yaml file and specify this assets folder

![pub.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1654424586354/72qnmWG9R.png align="left")

--------

### Assets Generation
- Now, within the project level terminal, we need to run one command to produce all the constants for the assets that we provided earlier.
- Run the following command from the project level terminal:

```
fluttergen -c pubspec.yaml
```

- After running the following command, a new folder named `gen` will be created inside the `lib` folder. The 'assets.gen.dart' file is located in this directory.
- And if you examine this file, you'll notice that this package generates all of the asset references automatically. Isn't it amazing?

-------

### How to use Generated Assets
- You can use the assets by specifying the path inside the Image widget like below :

```
Image.asset(Assets.images.apple.path)
```

- Or, there is another cooler way, you can directly create an Image by calling `.image()` function after the asset name like below.

```
Assets.images.apple.image(),
```

----------

### Generating Svg.
- If you are using SVG images with `flutter_svg` you can also generate the SVG easily by changing the `flutter_svg` value to `true` inside the `flutter_gen`'s `integration` parameter like below:

```
# pubspec.yaml
flutter_gen:
  integrations:
    flutter_svg: true

flutter:
  assets:
    - assets/images/bike.svg
```

- Now as we've used normal assets as above, we can use the generated SVG in the same way :

```
Widget build(BuildContext context) {
  return Assets.images.bike.svg(
    width: 120,
    height: 120
  );
}
```

-------

### Generating Colors
- As the FlutterGen supports generating colors from XML format files, we can specify the XML colors inside the configuration as below:

```
# pubspec.yaml
flutter_gen:
  colors:
    inputs:
      - assets/color/colors.xml
      - assets/color/colors2.xml
```

- And use it like below:

```
Text(
  'Flutter Gen Color',
  style: TextStyle(
    color: ColorName.denim,
  ),
```

- More on Color, click [here](https://pub.dev/packages/flutter_gen#colors)

----------------

## Wrapping Up
- **That concludes this article. You can generate many cool things using this package. You can head over to its GitHub repo checkout for more information. And also don't forget to leave a ⭐. That'll motivate developers to create amazing things like this.**
- **I hope you enjoyed and learned something from this article. If you have any feedback/queries, leave them in the comments.**
- **Thank you for spending time reading this article. See you in the next article. Until then...**