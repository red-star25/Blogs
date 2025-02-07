---
title: "How to Publish Flutter App on Play Store"
datePublished: Thu Aug 19 2021 04:54:39 GMT+0000 (Coordinated Universal Time)
cuid: cksig95ix05gnwqs12jn9gsx9
slug: how-to-publish-flutter-app-on-play-store
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1629346680588/w2y9IdYBL.png
tags: app-development, programming-blogs, flutter, google

---

## Introduction 
- Every Flutter application developer wishes to create a public app that will be downloaded by the people and used by many. 
- If you are one among them then you have come to the right place. Here, I am going to share with you the best and easy way to publish your flutter application on the Play store. 
- This step-by-step tutorial will take you through every step required to publish your flutter app on the play store.
- **Excited**? 
![ExcitedHockeyGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629036130911/Iu8Kq6H9F.gif)
- Let's get started.

----------------------------------------

## Step - 1: Add a Launcher Icon
- After you've designed your Icon. Now it's time to add it to our project.
- For that go to [App Icon Generator](https://appicon.co/#app-icon).
- Drop your Icon.
- After that select **Android** and click on **Generate** button.
- It will create a **zip** file containing all the different sizes of Icons that you require for publishing the application.
- 
![generateAppIcon.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629038455874/YDIAk7RqH.gif)
- Extract the zip file
- 
![afterextract.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629037886105/7QyE3Eg1t.png)
- Here we got **android**(containing all the mip-map folders), **playstore** icon (will use this later when publishing), and **appstore** icon.
- Now **copy ** all the folder available in the `android` folder and replace it with `android > app > src > res` `mip-map` folders
- 
![replacingmipmap.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629038388267/Kwve57LNH.gif)
- To check whether the icon has been set or not let's run the app.
- 
![appicongenerated.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629040633717/j-UiTmb1M.png)
- Okay, so we've successfully added Launcher Icon. Let's `rename` our app and also the `bundle` and `appId`.

-----------------------------

## Step - 2: Rename the App, BundleId, AppId
- For renaming the app, Bundld and AppId we can use [rename](https://pub.dev/packages/rename) package available in **Pub.dev**.
- For that first of all we have to activate the command. For that paste the below command in your terminal.
- 
```
pub global activate rename
```
- After activating the command, we can now rename the app by running the below command. 
- 
```
pub global run rename --appname "Counter"
```
- Instead of **Counter** specify your own app name
- You'll get this message after running this command.
- 
![appnamechanged.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629041621376/MfHg7ZDsb.png)
- Now to rename the `BundleId` run the below command.
- 
```
pub global run rename --bundleId com.dhruvnakum.counter
```
- 
![bundleIdchanged.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629041535744/vKcry9T2O.png)
- Make sure your BundleId and AppId are unique.
- Now let's run the app and check if the name has changed or not.
- 
![appnamechangedonphone.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629041856290/prPZ3jpQl.png)

--------------------------------------

## Step - 3: Signing the app
- To publish on the Play Store, you need to give your app a **digital signature**. Use the following instructions to sign your app.
- Create `key.properties` file inside the `android` folder.
- 
![keyfilecreated.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629042146956/baSxRDhtq.png)
- Now paste the below text inside `key.properties`
- 
```
storePassword=eChim2v6qKn3     '''use your password here and make sure to keep it in secret.'''
keyPassword=eChim2v6qKn3
keyAlias=upload
storeFile=<location of the key store file, such as /Users/<user name>/upload-keystore.jks>
```
- After this run the below command in your terminal.
- 
> For Windows
```
keytool -genkey -v -keystore c:\Users\nakum\upload-keystore.jks -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 -alias upload
```
> For Mac / Linux
```
keytool -genkey -v -keystore ~/key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias key
```
- 
![keyjksgenerated.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629043244166/IZg0mAWN5.gif)
- Go to the file location where `key` is generated.
- 
![localkey.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629043301296/Idko4_o5j.png)
- Now move this `upload-keystore.jsk` inside `android > app` folder.
- 
![keymovedtoandroid.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629043577517/8B9Y6WQ3R.png)
- Update the `storeFile` path inside the `key.properties` file.
- 
```
storePassword=eChim2v6qKn3
keyPassword=eChim2v6qKn3
keyAlias=upload
storeFile=../app/upload-keystore.jks
```
- Now go to `[project] > android > app > build.gradle` file and add the following text above the `android { ... }`
- 
```
def keystoreProperties = new Properties()
def keystorePropertiesFile = rootProject.file('key.properties')
if (keystorePropertiesFile.exists()) {
    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
}
```
- 
![aboveandroid.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629043937611/Gdxv3m7r0.png)
- Scroll down a little bit and remove `buildType{ ... }` and paste the below text instead.
- 
```
    signingConfigs {
       release {
           keyAlias keystoreProperties['keyAlias']
           keyPassword keystoreProperties['keyPassword']
           storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null
           storePassword keystoreProperties['storePassword']
       }
   }
   buildTypes {
       release {
           signingConfig signingConfigs.release
       }
   }
```
- 
![replacebuild.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629044187962/ngDvQqObG.png)

---------------------------------------

## Step: 4 - Create android app bundle
- Run `futter clean` to clean the previous build.
- 
```
flutter clean
```
- Now to generate `appbundle` run the below command.
- 
```
flutter build appbundle
```
- This will create a `.aab` inside `build > app > output > bundle > app-release.aab`.
- 
![aabgenerated.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629044715351/XnLGcPwnJ.png)

- Now it's time to publish this app via `Developer Console`.

------------------------------

## Step: 5 - Create Developer Account
- Head over to [Developer Account](https://play.google.com/console)
- You have to pay **$25** to create a Developer account. If you have it already skip this step.
- So create the account and then jump over to **Step : 6**

----------------------------------

## Step: 6 - Create App
- Now click on the **Create App** button
- 
![createapp.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629203706806/-DE3gBWP4A.png)
- Now Fill **App Name**, **Default Language**, **App Type**, **Free or Paid** and check all the checkbox.
- 
![createappcrated.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629203942390/Vrvv7OrnY.png)

-----------------------------------

## Step: 7 - Adding Description, Logo, Screenshots, Videos, Feature Graphics.
- Now go to `Store presence > Main store listing`.
- 
![mainstorepresence.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629204166971/OxeMzK9kw.png)
- Fill out the **Short** and **Full description**.
- 
![appdis.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629204276589/hZ8nQozO2.png)
- Now to add **App Icon** open the previously downloaded **AppIcons** file.
- Here you will see a `png` file named **playstore**.
- Simply drag and drop this `playstore.png` into **App icon** box.
- 
![icondrop.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629204515117/3c7x6OwQJ.gif)
- Now you have to add **Feature Graphics**.
- For that, I've found out a very good website [Online Graphic Generator](https://www.norio.be/graphic-generator/). You can create **Feature Graphic** using this website. Feel free to use any website.
- 
![feature_graphic.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629205467650/HrkqPiF-c.png)
- Now add at least 2 **Screenshots** of your app in the `Phone Screenshots` section.
- 
![ss.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629205553099/lhchoMF4Ye.png)
- If you have **7' and 10' tablets Screenshot please add it also in the ** **Tablet** section.
- 
![tablet.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629205114481/oob6THwVn.png)
- Now **Save** the `Main Store Listing`.

-----------------------------

## Step: 8 - Store Setting
- Now go to **Store Settings** and select your app `Category` and add tags if you want to.
- 
![category.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629205714120/g9w6kkvjq.png)
- Now enter your **email **(*required), **phone number**, and **website** URL.
- 
![email.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629205771245/bqCU7Mp4Y.png)
- **Save it**.

-----------------------------------

## Step: 9 - Add Country and Region
- Go to `Production > Country / Region` and then add the countries where you want to show your app.
- 
![country.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629205991680/uaeCZbcdY.gif)

----------------------------------

## Step: 10 - App Content
- Add **Privacy policy** of your app. You can use [Privacy Policy Generator](https://app-privacy-policy-generator.nisrulz.com/) or if have any then paste the link in the text field.
- 
![privacy.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629206489226/IqoaGFUH1.png)
- > Select **App Access** 
- 
![appaccess.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629206581242/gH9FIHaXG.png)
- > Go to **Ads** and select **YES** if your app contains **ADS** or **NO** if app doesn't contain any type of **ADS** 
- 
![ads.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629206719794/_giAb2EAz.png)
- > Go to **Content Rating**. Select the **category** of your app.
- 
![contentrating1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629206917175/afcfOL4Qxy.png)
- Now go to **Questionnairy** tab and answer the given questions.
- After answering all the questions **Save** it.
- > Now go to **Target audience and content**
- Select What are the target age groups of your app?
- 
![targetage.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629207274642/N6OVA8OVC.png)
- Click **Next**
- Select the appropriate options on the **App Details** page.
- 
![appdetails.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629207376866/R5prbGhKM.png)
- Click **Next** 2 times. You'll end up in **Store presence** tab. Select appropriate option.
- 
![storepresence.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629207468162/aFdaA4T3J.png)
- Click **Next** and **Save** it.
- > Go to **News apps**
- Select **YES** if your app is **news** app, otherwise select **NO**.
- 
![newsapp.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629207682174/h_b8f16j2.png)
- **ALL DONE**.

-----------------------------

## Step: 11 - Rollout the Application in Production
- Click on **Production** from the sidebar.
- Create a **New Release**
- 
![newrelease.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629207838908/Ucu_J5i3R.png)
- Now upload the `app-release.abb` app bundle file in **App Bundle** section.
- 
![bundleadded.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629208100113/BywenRh6m.gif)
- Now add **Release Note** this will be displayed on your Google Play's App's home page.
- 
![releasedetail.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629208245507/0NpigTAca.png)
- **Save it** and **Review Release**.
- Now **FINALLY** click on **Start Rollout To Production**.
- ![rollout.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629347518859/-xf9n1_tD.png)
- That's it 🎉!! Now you have to wait for the response from the google team. They will review your application manually and then will add it to the **Google Play Store**. 
- 
![SimonGoldenBuzzerGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629208694108/WlNgft79c.gif)
--------------------------------

## Wrapping Up
- Thanks for reading. Hope you liked it. 
- Feedback and Comments are welcomed 🙂

- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629208644941/Kw8gn62QQ.gif)
