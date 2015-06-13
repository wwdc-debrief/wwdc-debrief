# WWDC Debrief

A colleciton of WWDC 2015 information, resources and summaries.


## General info

- **Date:** 8 June 2015
- **Homepage:** [https://developer.apple.com/videos/wwdc/2015/]()

## Top 10 News
1. New OSX version: "El Capitan" [http://www.apple.com/osx/elcapitan-preview/]()
2. New iOS version: iOS9 [http://www.apple.com/ios/ios9-preview/]()
3. New Apple watch version: watchos 2. With this version developers can write native application for the watch. [https://www.apple.com/watchos-2-preview/]()
4. Apple release his own music streaming service: "Music"  [http://www.apple.com/music/]()
5. Removed the newstand application, a new one is introduced: "news" with a secific data format [https://developer.apple.com/news-publisher/]()
6. Siri become proactive, google now style. 
7. On iPad user can split the screen and work on two separate app at the same time.
8. Apple maps shows public transportation info
9. Single Developer programm
10. CarPlay improvement

## Most Important Videos

Code  | Title           | Link
----- | --------------- | ---------------- |
101   | Keynote         | [https://developer.apple.com/videos/wwdc/2015/?id=101]()
102   | State of the Union | [https://developer.apple.com/videos/wwdc/2015/?id=102]()






## Resources

**wwdc-downloader:**

Name            | Desc                                               | URL | 
----------------| ---------------------------------------------------|
wwdc-downloader | A bash script for downloading all the wwdc videos. | https://github.com/ohoachuck/wwdc-downloader
Links | [http://mjtsai.com/blog/2015/06/09/wwdc-2015-links/]()








## Videos

### 104: What's new in Xcode

**Link:** [https://developer.apple.com/videos/wwdc/2015/?id=104]()


With Xcode 7 is possible to build applicatin for iOS, OSX and now WatchOS and also is included support for Swift 2.
Xcode7 includes a migrator for swift1.x to 2 and also support generics and nullability for Objective-C.

Xode7 includes some new features for Playground, like rich comments (using markdonw), resource folders, pmultiple pages and is it possible include code result directly below the source code.

**APP THINNING**

Xcode7 includes includes funcitionalities for the App Thinning:

* **bitcode:** an intermediae rapresentation of the source code that apple can re-compile and re-optmize
* **slicing:** applications now will download olny the resources specific for that device. For example @3x images are downloaded only on iOS6+
* **On Deman Resources:** Apple can store some (up to 4GB) of assets on his servers. These assets can be downloaded and used a usual.

*min. 9 Starting demo*

* Migration to watchos2
* App slicing

Asset can contains all type of data and is possible specify some constraints, like "use this version of the file if the device has more than 1GB RAM"

If the resources are downloaded, all the other api work as usual (imageWithName:)

Is possible to remove all the downloaded resources.

The resources can be downloaded using a `NBundleResourceRequest` and a `tag`

*min. 18: End demo*

**DEBUGGING**

Instrument includes a new profile Location Instrument  and a function called "Address Sanitizer"

*min. 20: Starting demo Address sanitizer*

Enable Address sanitizer from schema, the app is recompiled and we can see the dump of the memory and who allocated or deallocated a specific part of it.


It can run on the server
*min. 26: End demo*



*min. 27: Starting demo*

Demo about crash report on xcode

*min. 26: End demo*


**TESTING**

XCode can create Code Coverage report after run a test. When enabled on the schema the code is colored if is not covered by test.

Xcode include also a UI test Kit

*min. 27: Starting demo*

demo about UI Testing 

*min. 37: end demo*









