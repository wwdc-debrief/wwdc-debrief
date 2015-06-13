# 106: What’s New in Swift

**Link:** [https://developer.apple.com/videos/wwdc/2015/?id=106]()

Topics:

* Fundamentals
* Pattern Matching
* Availability Checking
* Protocol Extentions
* Error Handling


## Fundamentals

### Enums

Printing an enum will show its real value (not `(Enum Value)`)

```swift
enum Animals {
	case Dog, Cat, Troll, Dragon
}
let a = Animals.Dragon
print(a)
```

Before the output was `(Enum Value)`.
In Swift 2 is finally `Animals.Dragon`

### Associated values in Enum

Now you can define an enum like this

```swift
enum Either<T1, T2> {
	case First(T1)
	case Second(T2)
}
```

### Recursive Enums

You can define recursive enums, using `indirect` keyword

```swift
enum Tree<T> {
	case Leaf(T)
	indirect case Node(Tree, Tree)
}
```

### "do" Statement

To avoid confusion between `do` keyword for scoping variables and `do-while` cycle, the second one has been replaced by `repeate`

Scoping:
```swift
do {
	let a = Animals.Troll
	...
}
```

Do-while:
```swift
repeate {
	let a = Animals.Troll
	...
} while (...)
```

### Option Sets

In Swift 1, option sets are defined and use like this
```swift
viewAnimationOptions = .Repeate | .CurseEaseIn | .TransitionCurlUp
viewAnimationOptions = nil
if viewAnimationOptions & .TransitionCurlUp != nil {
```

Note that `nil` here is conceptually wrong.

Swift 2 uses parenthesys

```swift
viewAnimationOptions = [.Repeate | .CurseEaseIn | .TransitionCurlUp]
viewAnimationOptions = []
if viewAnimationOptions.contains(.TransitionCurlUp) {
```

### Defining an Option Set

```swift
struct MyFontStyle : OptionSetType {
	let rawValue = Int
	static let Bold          = MyFontStyle(rawValue: 1)
	static let Italic        = MyFontStyle(rawValue: 2)
	static let Underline     = MyFontStyle(rawValue: 4)
	static let Strikethrough = MyFontStyle(rawValue: 8)
}

myFont.style = []
myFont.style = [.Underline]
myFont.style = [.Bold, .Italic]

if myFont.style.contains(.StrikeThrought) {
```

### Functions and Methods

Unified functions and methods usage with consistent argument labels. You can also disable or make explicit label for each parameter.

NOTE: # argument syntax has been removed.

### Diagnostics

Warnings and quick fix has been improved widely.

Example 1:

```swift
struct MyCoordinates {
	var points : [CGPoint]
	
	func updatePoint() {
		points[42].x = 19
	}
}
```

Old warning on `points[42].x = 19`: `'@lvalue $T7' is not identical to 'CGFloat'`
New warning: `Cannot assign to 'x': 'self' is immutable`
Plus quick fix: `Fix-it: Mark method 'mutating' to make 'self' mutable`

Example 2:

```swift
func processEntries() {
	var entries : ...
	
	let size = entries.count
	
	var indices = entries.map { $0.index }
	indices.sort()
}
```

On `var entries`: `Variable 'entries' was never mutated`.

On `let size ...`: `Immutable value 'size' was never usd`.

On `indices.sort()`: `'sort' result is unused; use 'sortInPlace' to mutate in-place`.

### SDK Improvements

Added new features (like nullability qualifiers and typed collections) to Objective-C in order to improve the interoperability between Swift and Obj-C itself.

### Unit Testing and Access Control

Your code is now built in a "compile for testing" build mode in order to make **public** and **internal** symbols available in tests.

NOTE: no behavior change for release builds.

### Rich comments

Comments support Markdown format.

## Pattern Matching

## inside "if" statement

To avoid the "Pyramid of Doom", Swift introduces the **Compount Conditions** 

Before:

```swift
func prepareForSegue(segue: UIStoryboardSegue, sender: AnyObject?) {
	if let dest = segue.destinationViewController as? BlogViewController {
		if let blogIndex = tableView.indexPathForSelectedRow()?.row {
			if segue.identifier == blogSegueIndentifier {
				dest.blogName = swiftBlogs[blogIndex]
				...
			}
		}
	}
}
```

With Compound Conditions:

```swift
func prepareForSegue(segue: UIStoryboardSegue, sender: AnyObject?) {
	if let dest = segue.destinationViewController as? BlogViewController
		let blogIndex = tableView.indexPathForSelectedRow()?.row
		where segue.identifier == blogSegueIndentifier {
				dest.blogName = swiftBlogs[blogIndex]
				...
	}
}
```

To improve the "Early Exits" design, the **guard** statement has been introduced:

Before: 

```swift
func process(json: AnyObject) -> Either<Person, String> {
	let name: String? = json["name"] as? String
	if name == nil {
		return .Second("missing name")
	}
	let year: Int? = json["year"] as? Int
	if year == nil {
		return .Second("missing year")
	}
	
	let person = processPerson(name!, year!)
	return .First(person)
}
```

NOTE: you have to force and wrap name and year.

With **guard** statement:

```swift
func process(json: AnyObject) -> Either<Person, String> {
	guard let name = json["name"] as? String else {
		return .Second("missing name")
	}
	guard let year = json["year"] as? Int else {
		return .Second("missing year")
	}
	
	let person = processPerson(name, year)
	return .First(person)
}
```

You can also combine multiple guards in a single check

```swift
func process(json: AnyObject) -> Either<Person, String> {
	guard let name = json["name"] as? String,
	      let year = json["year"] as? Int else {
		return .Second("bad input")
	}
	
	let person = processPerson(name, year)
	return .First(person)
}
```

### inside "switch" statement

With single swich case, you can use the same "switch" features to "if"

```swift
switch bar() {
	case .MyEnumCase(let value) where value != 42:
		doThing(value)
	default: break
}
```

```swift
if case .MyEnumCase(let value) = bar() where value != 42 {
	doThing(value)
}
```

### with "for ... in" loop

```swift
for value in mySequence {
	if value != "" {
		doThing(value)
	}
}
```

```swift
for value in mySequence where value != "" {
	doThing(value)
}
```

```swift
for case .MyEnumCase(let value) in enumValues {
	doThing(value)
}
```

## API Availability Checking

If you try to use an API that is not available since your deployment target, the compiler warns you (with an error). This way you can avoid checking the availability using `respondsToSelector()`.

To use new APIs, Swift 2 introduces `#available(<start api versio>, <end api version>)`.

Example


```swift
@IBOutlet var dropButton: NSButton!

override func awakeFromNib() {
	if #available(OSX 10.10.3, *) {
		dropButton.springLoaded = true
	}
}
```

## Protocol Extensions

Before you had to create global functions to add functionality to interfaces. You could "extends" just classes (like `Array`). With Swift 2 you're allow to extend also interfaces (like `CollectionType`).

```swift
Swift 1:
let x = filter(map(numbers) { $0 * 3 }) { $0 >= 0 }

Swift 2:
let x = numbers.map { $0 * 3 }.filter { $0 >= 0 }
```

See "**Protocol-Oriented Programming in Swift**" video for more details.

## Error handling

Use `try` keyword in front of a method that can throw an error.
Use `try!` to handle the error like a fatal error (it will crash the app).

Use `do-catch` statement to handle the `try doStuff()`  locally.
If you want to propagate the error out instead, use the keyword `throws` in the method name definition. 


A new protocol, `ErrorType` is available. Any `ErrorType` implementation can be thrown and caught.

Use `enum` as your custom error type:

```swift
enum DataError : ErrorType {
	case MissingName
	case MissingYear
	// add more later
}
```

Final example:

```swift
func processPerson(json: AnyObject) throws -> Person {
	guard let name = json["name"] as? String else {
		throw DataError.MissingName
	}
	guard let year = json["year"] as? Int else {
		throw DataError.MissingYear
	}
	
	return Person(name, year)
}
``` 

### Defer Actions

Using `defer` block you can execute some code on any function ends (on return, on throw, etc)

```swift
func processSale(json: AnyObject) throws {
	delegate?.didBeginReadingSale()
	defer { delegate?.didEndReadingSale() }
	
	guard let buyerJSON = json["buyer"] as? NSDictionary {
		throw DataError.MissingBuyer
	}
	let buyer = try processPerson(buyerJSON)
	guard let price = json["price"] as? Int {
		throw DataError.MissingPrice
	}
	
	return Sale(buyer, price)
}
```