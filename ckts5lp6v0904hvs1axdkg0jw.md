---
title: "Flutter and AdMob: A blog around monetizing your Flutter app with AdMob."
datePublished: Mon Sep 20 2021 04:33:52 GMT+0000 (Coordinated Universal Time)
cuid: ckts5lp6v0904hvs1axdkg0jw
slug: flutter-and-admob-a-blog-around-monetizing-your-flutter-app-with-admob
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1632047910227/GoVfs6MBf.png
tags: programming-blogs, flutter, flutter-sdk, flutter-examples

---

## Introduction
- Mobile applications are a great way to earn revenue from your programming skills. There are many ways to earn money apart from the app store revenue. You can add ads to your apps and monetize them.
- Google is the biggest player in the online advertisement industry. Recently, Flutter released a package called [google_mobile_ads](https://pub.dev/packages/google_mobile_ads) for monetizing the Flutter application.
- This plugin currently supports loading and displaying **banner**, **interstitial **(full-screen), **native ads**, and **rewarded video ads**.
- This plugin can also support **Google Ad Manager**, if you want to load and display ads from Google Ad Manager

---------

## Starter Project
- The starter project contains a basic layout for showing **posts**.
- You can get the starter project from the below link - 
%[https://github.com/red-star25/google_ad_flutter]
- **Output of the starter project**
![starter.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631600279932/JHpu7mvVY.png)

- These **Posts ** are coming from the `post.dart` file and is displayed with the help of `ListView.builder()` widget.
- Now that we've seen the starter projects, we can now proceed further by integrating ads in the app.
----------

## Install Package
- Goto **pub.dev** and copy the latest version of `google_mobile_ads` package.
%[https://pub.dev/packages/google_mobile_ads]
- And then paste it inside `pubspec.yaml`
- 
```
dev_dependencies:
    flutter_test:
      sdk: flutter
    google_mobile_ads: ^0.13.4
```

------

## Create AdMob account
- Open **admob** website and LogIn/SignUp by using your google account.
%[https://admob.google.com/home/]
- After signing in into the admob account. You will be redirected to the dashboard. Which will look like this -
- 
![admob_dashboard.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631600915919/OQNUPg35Ek.png)
- Now go to the **Apps ** in the left sidebar and then click “Add Your First App”.
- 
![admob_app.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631601134020/MMIqDPGKC.png)
- Now you have to choose the **Platform** on which you want to show ads. The steps for both are the same. I'm choosing **Android** for this tutorial. 
- They are also asking **if your app has already been listed on the play store or not**. If **yes** then select yes, otherwise select no. 
- 
![add_app.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631601313569/yT-eSVwi1.png)
- After that, you will be asked to enter the name of your app and whether you want to use **user metrics** or not. **User Metrics** is used to understand the user behavior like, how they are interacting, how many daily active users are there for how much time, etc.
- 
![add_app2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631601765401/Zx3AxU1eyO.png)
 - Now that you have successfully added your app. Let's create an **Ad Unit**

----------
## Create Ad Unit
- **Ad units ** are containers you place in your apps to show ads to users. **Ad units** send ad requests to **AdMob**, then display the ads they receive to fill the request. When you create an ad unit, you assign it an ad format and ad type(s). Ad format describes the way ads will look in your app and where they'll be located.
- Head over to the **Ad units** section in the left panel. And click on the **Get Started** button in order to create ad units.
- 
![add-unit.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631602159578/9cnHz_IDw.png)
- Here you will see different types of ad units.
- 
![different_ad_unit.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631602352103/d5VOX57-q.png)
- We are going to use **Banner**, **Interstitial**, and **Rewarded** ad units in our app.
- First, let's create a **Banner** ad unit. You have to enter a name for your ad unit. You can also change some advanced settings if necessary.
- 
![banner_Ad.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631602685333/dYuWVTLj_.png)
- Now click on the **Create ad unit** and you'll get the `app ID` and `ad unit ID` that you need to place when you are shipping your app in production.
> Don't use production `app id` and `unit id` while developing apps. Use the `test` keys provided by the admob. You can get the test ids for **Android** [here](https://developers.google.com/admob/android/test-ads#sample_ad_units) and for **iOS** [here](https://developers.google.com/admob/ios/test-ads#demo_ad_units) 
- Now that we've created a banner ad unit we can add it inside our flutter application.

---------

## Configuration

### iOS Configuration :
- Update your app's ios/Runner/Info.plist file to add two keys:
- A `GADApplicationIdentifier` key with a string value of your AdMob app ID (identified in the AdMob UI).
- A `SKAdNetworkItems` key with Google's `SKAdNetworkIdentifier` value of `cstr6suwn9.skadnetwork`.
- 
```
<key>GADApplicationIdentifier</key>
<string>ca-app-pub-3940256099942544~1458002511</string>
<key>SKAdNetworkItems</key>
  <array>
    <dict>
      <key>SKAdNetworkIdentifier</key>
      <string>cstr6suwn9.skadnetwork</string>
    </dict>
</array>
```

### Android Configuration :
- Head over to `AndroidManifest.xml` file and add the below code under the `<application>` tag
- 
```
<meta-data
   android:name="com.google.android.gms.ads.APPLICATION_ID"
   android:value="ca-app-pub-3940256099942544~3347511713"/>
```
- Now head over to app-level `build.gradle` and update the **minSdkVersion** to **19 or higher**
- 
```
    defaultConfig {
        applicationId "com.example.google_ad"
        minSdkVersion 19
        targetSdkVersion 30
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
    }
```

---------

## Initialize SDK
- Now that all the configuration is done. The next thing to do is to initialize the **Android Ad SDK**.
- To do that, head over to `main.dart` and add the below code under `main` function.
- 
```
void main() {
  WidgetsFlutterBinding.ensureInitialized();
  MobileAds.instance.initialize();
  runApp(const MyApp());
}
```
---------
## Create Ad State Class
- To provide **AdUnitId** for different platforms (**Android**, **iOS**) we need a state which gives us that `unit id` according to platform.
- So let's create a file `ad_state.dart`and add the below code under it.
- 
```
class AdState {
  String get bannerUnitId {
    if (Platform.isAndroid) {
      return "ca-app-pub-3940256099942544/6300978111"; // test unit id
    } else {
      return "ca-app-pub-3940256099942544/2934735716"; // test unit id
    }
  }
}
```
- This `bannerUnitId` getter will provide `unitId` for specific platform. You have to update this test id with your production `unit id`s when you deploy your app.

-------
## Adding BannerAd to UI
- Now let's create a reference of BannerAd and also a boolean which will change its value when the ad initializes.
- Open the `HomePage.dart` and add below code 
- 
```
class _HomePageState extends State<HomePage> {
    late BannerAd _bannerAd;
    final bool _isBottomBannerAdLoaded = false;
....
```
- Now to initialize the `_bannerAd` override the `initstate` and add below code inside it.
- 
```
  @override
  void initState() {
    super.initState();
    _bottomBannerAd = BannerAd(
      adUnitId: AdState.bannerUnitId,
      size: AdSize.banner,
      listener: BannerAdListener(
        onAdLoaded: (_) {
          setState(() {
            _isBottomBannerAdLoaded = true;
          });
        },
        onAdFailedToLoad: (ad, error) {
          setState(() {
            _isBottomBannerAdLoaded = false;
          });
          ad.dispose();
        },
      ),
      request: const AdRequest(),
    )..load();
  }
```
- And also don't forget to **dispose** the BannerAd instance.
- Here the `adUnitId` gets our banner **unit id** from the class **AdState** that we've created earlier.
- `size` property takes the size of the ad. There are different sizes available. For example, **fullBanner**, **largeBanner**, **leaderborad**, etc.
- `listener` will receive notification for the lifecycle of a **BannerId**. `onAdLoaded` suggests **Ad successfully loaded - display an AdWidget with the banner ad.** `onAdFailedToLoad` suggests **Ad failed to load - log the error and dispose the ad.**
- `request` is used to request the ad for displaying it in the UI.

-------
## Adding AdWidget to UI
- Now to add `BannerAd` to the screen, the package provides us a widget called **AdWidget**.
- We have to pass our `_bottomBannerAd` to `AdWidget` constructor
- 
```
Scaffold(
      bottomNavigationBar: _isBottomBannerAdLoaded
          ? SizedBox(
              height: _bottomBannerAd.size.height.toDouble(),
              width: _bottomBannerAd.size.width.toDouble(),
              child: AdWidget(ad: _bottomBannerAd),
            )
          : Container(),
// .....
```
- 
![banner_ad_app.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631725793851/ZBEQQ9qaF.png)
- Woohoo!! 🎉
- 
![MarvinsappYouMadeItGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631726007518/HWzlqCwDm.gif)

-------

## Adding InterstialAd to UI
- **Interstitial** ads are full-screen ads that cover the interface of the app. 
- So, first, create an InterstialAd ad unit from the AdMob console. And then head over to the next step.
- Let's now create a getter in `AdState` file for getting the **unitID**
- 
```
  static String get interstitialAdUnitId {
    if (Platform.isAndroid) {
      return "ca-app-pub-3940256099942544/8691691433";
    } else {
      return "ca-app-pub-3940256099942544/5135589807";
    }
  }
```
- To display Interstitial ads we have to first create an instance and also a boolean which is used to check if the ad is loaded or not.
- 
```
InterstitialAd? _interstitialAd;
bool _isInterstitialAdLoaded = false;
```
- Now, `load` the `InterstitialAd` inside the `initstate` and also dispose the `_interstitialAd` inside `dispose` function.
- 
```
 @override
  void initState() {
    super.initState();
    InterstitialAd.load(
      adUnitId: AdState.interstitialAdUnitId,
      request: const AdRequest(),
      adLoadCallback: InterstitialAdLoadCallback(
        onAdLoaded: (InterstitialAd ad) {
          _interstitialAd = ad;
          _isInterstitialAdLoaded = true;
        },
        onAdFailedToLoad: (LoadAdError error) {
          _isInterstitialAdLoaded = false;
          _interstitialAd.dispose();
        },
      ),
    );
  }

  @override
  void dispose() {
    _bottomBannerAd.dispose();
    _interstitialAd.dispose();
    super.dispose();
  }
```

- Now let's load this `InterstitialAd` when the user clicks on any of the posts. 
- To do that, all you have to do, is to call the `show()` method on Navigation, Just like below
- 
```
GestureDetector(
                onTap: () {
                  if (_isInterstitialAdLoaded) {  
                    _interstitialAd.show();   // <- here
                  }
                  Navigator.push(
                    context,
                    MaterialPageRoute(
                      builder: (_) => PostPage(
                        post: post,
                      ),
                    ),
                  );
                },
                child: PostCard(
                  hasReadMore: true,
                  post: post,
    )
),
```
- 
![interstitial.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631727626879/E3Afk6Pp6.gif)

- Woohoo!! 🎉
![YouDidItAgainBgtGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631727682958/Mmzj3HKgK.gif)

---------

## Adding RewardedAd to UI
- Rewarded ads provide an opportunity for users to watch a video or engage with a playable ad in exchange for a reward within the app.
- This is usually used in **Games**.
- So, first, create a Rewarded ad unit from the AdMob console. Here you can also Enter information about the rewards users will receive after viewing a rewarded ad in this ad unit. Define the reward items—such as coins or extra lives—and their amounts.
- 
![rewardedconsole.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1632045400919/4cvoF5Ix5.png)
- First, let's create a getter for getting the **unitId** for rewarded ads
- 
```
  static String get rewardedAdUnitId {
    if (Platform.isAndroid) {
      return "ca-app-pub-3940256099942544/5224354917";
    } else {
      return "ca-app-pub-3940256099942544/1712485313";
    }
  }
```
- Now, let's implement it in our app. First, let's create an instance and a boolean as we've done in the above two example
- 
```
  late RewardedAd _rewardedAd;
  bool _isRewardedAdLoaded= false;
```
- Let's initialize this inside `initState`
- 
```
  @override
  void initState() {
    super.initState();
    RewardedAd.load(
      adUnitId: AdState.rewardedAdUnitId,
      request: const AdRequest(),
      rewardedAdLoadCallback: RewardedAdLoadCallback(
        onAdLoaded: (ad) {
          _rewardedAd = ad;
          ad.fullScreenContentCallback = FullScreenContentCallback(
            onAdDismissedFullScreenContent: (ad) {
              setState(() {
                _isRewardedAdLoaded = false;
              });
            },
          );
          setState(() {
            _isRewardedAdLoaded = true;
          });
        },
        onAdFailedToLoad: (err) {
          setState(() {
            _isRewardedAdLoaded = false;
          });
        },
      ),
    );
}
```
- Also dispose it inside `dispose()` function
- 
```
  @override
  void dispose() {
    _bottomBannerAd.dispose();
    _interstitialAd.dispose();
    _rewardedAd.dispose();
    super.dispose();
  }
```
- Now let's `show()` this on FloatingActionButton click
```
Scaffold(
      floatingActionButton: FloatingActionButton(
        child: const Icon(Icons.gamepad),
        onPressed: () {
          _rewardedAd.show(
            onUserEarnedReward: (ad, reward) {
              // perform operation when earned rewards
            },
          );
        },
      ),
//....
```
- 
![rewarded.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631728757842/kFCCZb5VC.gif)
- 
![WhooHooYeahGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1631728899795/i02xz2KZGh.gif)

-----------

## Wrapping Up
- **That's It**. It's that simple to integrate ads in your app. But only adding ads is not efficient when it comes to monetizing. 
- You should also take care of your user experience and not popping ads every single place. There are many strategies that you can use to make your app more user-friendly and also a source of income at the same time.
- **So, If you found this article helpful then make sure to share it with others. And also leave feedback in the comments.**
- **Thanks for reading. See you in the next article. Till then.....**
- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632045811367/ekAs5_Rnd.gif)
