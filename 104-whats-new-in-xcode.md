# 104: What's new in Xcode

**Link:** [https://developer.apple.com/videos/wwdc/2015/?id=104]()


With Xcode 7 is possible to build applicatin for iOS, OSX and now WatchOS and also is included support for Swift 2.
Xcode7 includes a migrator for swift1.x to 2 and also support generics and nullability for Objective-C.

Xode7 includes some new features for Playground, like rich comments (using markdonw), resource folders, pmultiple pages and is it possible include code result directly below the source code.

#### APP THINNING

Xcode7 includes includes funcitionalities for the App Thinning:

* **bitcode:** an intermediae rapresentation of the source code that apple can re-compile and re-optmize
* **slicing:** applications now will download olny the resources specific for that device. For example @3x images are downloaded only on iOS6+
* **On Deman Resources:** Apple can store some (up to 4GB) of assets on his servers. These assets can be downloaded and used a usual.

##### min. 9..18:  Demo

* Migration to watchos2
* App slicing

Asset can contains all type of data and is possible specify some constraints, like "use this version of the file if the device has more than 1GB RAM"

If the resources are downloaded, all the other api work as usual (imageWithName:)

Is possible to remove all the downloaded resources.

The resources can be downloaded using a `NBundleResourceRequest` and a `tag`


#### DEBUGGING

Instrument includes a new profile Location Instrument  and a function called "Address Sanitizer"

##### min. 20..26:  Demo about address sanitizer

Enable Address sanitizer from schema, the app is recompiled and we can see the dump of the memory and who allocated or deallocated a specific part of it.



#### TESTING

XCode can create Code Coverage report after run a test. When enabled on the schema the code is colored if is not covered by test.

Xcode include also a UI test Kit

##### min. 27..37:  Demo about UI Test


