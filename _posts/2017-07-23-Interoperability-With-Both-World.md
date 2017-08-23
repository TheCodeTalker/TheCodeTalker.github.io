---
layout: post
title: Interoperability With Both World
---

## Intro

Swift designed  to pervoid seamless compatibility with  Cocoa and objective-c . you can use objective c api in swift as well . its a powerful tool to integrate into you workflow.

Start from Import 

`import Foundation`

This Statement will import statement access all of Foundation’s classes, protocols, methods, properties, and constants. The Process of importing can have following effects
* objective-c type to their equivalent in swift like id to Any
* Objective-C core types to their alternatives in Swift, like NSString to String
* Objective-C concepts to matching concepts in Swift, like pointers to optionals

### NOTE

`You cannot import C++ code directly into Swift. Instead, create an Objective-C or C wrapper for C++ code`

Alongside these Swift modules are generated Objective-C headers.These headers vend the APIs that can be mapped back to Objective-C. Some Swift APIs do not map back to Objective-C because they leverage language features that are not available in Objective-C.

### initialization

>obj-c initialisation begin with `init` or `initwith:` When an Objective-C initializer is imported by Swift, the init prefix becomes an `init`  keyword to indicate swift initializer.
objc  initializer  
{% highlight js %}
-(instancetype)init;
-(instancetype)initWithFrame:(CGRect)frame style:(UITableViewStyle)style;
{% endhighlight %}
swift equivalent swift initializer 
{% highlight js %}
init(){}
init(frame:CGRect, style: UITableViewStyle){}
{% endhighlight %}

if you go through these 2 styles of syntax you will find don’t need to call `alloc` Swift handles this for you. Notice also that `init` doesn’t appear anywhere when calling the Swift-style initializer.
### Example 
objc
`UITableView *myTableView = [[UITableView alloc] initWithFrame:CGRectZero style:UITableViewStyleGrouped];`
swift
`let myTableView: UITableView = UITableView(frame: .zero, style: .grouped)`

### Failable Initialization
In objc initalizer directly return the object they initialize. or when initialiser failed an it return nil. in swift the patten  built into a language feature called failable initialization.

if you want to design you own you can choose You can indicate whether initializers in your own Objective-C classes can fail using nullability annotations . 

### nullability annotation
1. indicate whether objc/c pointer can be nil
2. better Communicates the intent of apis 
3. allow better static checking 
4. improves usages in apis in swift


* Types declared to be nonnullable, either with a _Nonnull annotation or in an audited region, are imported by Swift as a nonoptional.
* Types declared to be nullable with a _Nullable annotation, are imported by Swift as an optional.
* Types declared without a nullability annotation are imported by Swift as an implicitly unwrapped optional

`[tableView deselectRowAtIndexPath: nil animated: false]; ` these api is you pass nil new warnings for nonnull parameters.


### example
`UIImage(contentsOfFile:)` <strong>initialize can fail to initialize a UIImage object if an image file doesn’t exist at the provided path. You can use optional binding to unwrap the result of a failable initializer if initialization is successful <strong>

### Accessing Properties

Objective-C property  declarations using the `@property` syntax are imported as Swift properties in the following way:
* Properties with the nullability property attributes (nonnull, nullable, and null_resettable) are imported as Swift properties with optional or nonoptional type
* Properties with the readonly property attribute are imported as Swift computed properties with a getter ({ get })
* Properties with the weak property attribute are imported as Swift properties marked with the weak keyword (weak var)
* Properties with an ownership property attribute other than weak (that is, assign, copy, strong, or unsafe_unretained) are imported as Swift properties with the appropriate storage
* Properties with the class property attribute are imported as Swift type properties
* Atomicity property attributes (atomic and nonatomic) are not reflected in the corresponding Swift property declaration, but the atomicity guarantees of the Objective-C implementation still hold when the imported property is accessed from Swift
* Accessor property attributes (getter= and setter=) are ignored by Swift
### Working With Methods
obj-c method calls like this 
`[myTableView insertSubview:mySubview atIndex:2];`
in swift these calls are like this 
`myTableView.insertSubview(mySubview, at: 2)`
If you’re calling a method with no arguments, you must still include parentheses.
`myTableView.layoutIfNeeded()`

### ID Compatibility
1. the Obj-c id type is imported by swift as Any.
2. the compiler introduces a universal bridging conversion operation when a Swift value or object is passed into Objective-C as an id parameter.
3. When id values are imported into Swift as Any, the runtime automatically handles bridging back to either class references or Swift value types.



### DownCasting Any
Any means any type downcast any type is not guaranteed to succesed . so we have to use (as?) or if certain about of the object you force downcast the object (as!) instead . if force Downcast the object fails a runtime error is trigger .
-----

Want to see something else added? <a href="https://github.com/TheCodeTalker/TheCodeTalker.github.io/issues/new">Open an issue.</a>
