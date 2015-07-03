# 107: What’s New in Cocoa Touch

**Link:** [https://developer.apple.com/videos/wwdc/2015/?id=107]()

Starting from iOS 6 Apple introduced some changes to allow the application to run in differen screen sizes / form factories

* iOS 6 -> Introduction of Autolayout
* iOS 7 -> Introduction of DynamicType
* iOS 8 -> Introduction of Adaptivity (aka Size classes)
*  iOS 9 -> Introduction of multitasking, now the application need to adapt to mutiple lauout event on the same layout.

###News

**Autolayout**

A new class `UILayoutGuide` should be used instead of empty views added on the storyboard just for the alignment.
Two new properties on `UIView` should help on set margin and define the available space for the text: `layoutMarginGuide` and `readableContentGuide`.

**UIStackView**

`UIStackView` is a new UIView subclass that allows advanced layout. check https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIStackView_Class_Reference/


**Keyboard**

A new bar can appears on top of the keybord with the common buttons for text format (bold, italic etc). All the textview can set a property ad show a custom button on this bar.

If you have and hardware keyboard, long press on command key will show an hud with a list of all the application shortcuts.

**Storyboard**

Is possible to link multiple storyboard and set unwind segue.

**RightToLeft**

Full support for right-to-left languages. Viewcontrollers and view offer specific properties for set/get the value of the semantic Direction.


**Touch to display Latency**

Improvement on the latency between the user interaction and the drawing on the screen. From 60ms to 30ms.
Now we can have access to the *intermediate* touch events and the *predicted* ones.

**UIKitDynamics**

* Non rectangular collision bounds.
* UIFieldBehaviour for simulating force fields.
* New type of attachment

**Notification**

Notification with text reply UIUserNotificationAction with custom done button

**Safari Viewcontroller**

SFSafariViewController is a Viewcontroller to show webpages with all the safari functionalities
 
**New extension points**

- new vpn protocols
- Spotlight
- AudioUnitS: Builtin create custom autio units

**Mapkit**

* 3d flighh
* traffic
* custom callout


**HealtKit**

* access to user data
* new data types like water, sun exposure.


**HomeKit**

* Detailed change notification  (best delegate callback)
* predefined scenes.
* Triggers not only based on timer.


**CloudKit**

* update limits and prices
* cloudkit (js)


**UIDocument**
 
 * can open document in place


**GameCenter**

* ReplayKit for record and share.
* SpriteKit is based on Metal (if supported)
* Action editor and OnDemandResources

**SchemeKit**

* new SceneEditor
* GamePlayKit

**Various**

* New api for Contacs 
* New api for get curren location one shot.
* **animate blur radious**
* Nullabilty and Lighweight Generics for Obj-C
* On Demand Resources
* App Slicing

