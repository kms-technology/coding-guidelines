
# KMS iOS Coding Standards

- [1. Purpose](#1-purpose)
- [2. Naming](#2-naming)
    - [2.1 General Principles](#21-general-principles)
        - [2.1.1 Clarify](#211-clarify)
        - [2.1.2 Consistency](#212-consistency)
        - [2.1.3 No Self Reference](#213-no-self-reference)
    - [2.2 File Names](#22-file-names)
    - [2.3 Naming Classes](#23-naming-classes)
    - [2.4 Naming Methods](#24-naming-methods)
    - [2.5 Naming Functions](#25-naming-functions)
    - [2.6 Naming Properties and Data Types](#26-naming-properties-and-data-types)
        - [2.6.1 Declared Properties and Instance Variables](#261-declared-properties-and-instance-variables)
        - [2.6.2 Constants](#262-constants)
    - [2.7 Naming Notifications and Exceptions](#27-naming-notifications-and-exceptions)
    - [2.8 Naming Categories](#28-naming-categories)
    - [2.9 Acceptable Abbreviations and Acronyms](#29-acceptable-abbreviations-and-acronyms)
- [3. Layout and Indentation](#3-layout-and-indentation)
- [4. Code Comments](#4-code-comments)
- [5. Properties](#5-properties)
- [6. Exceptions](#6-exceptions)
- [7. Logging](#7-logging)
- [8. Unit Test](#8-unit-test)
- [9. Miscellaneous](#9-miscellaneous)
    - [9.1 Pragma Mark](#91-pragma-mark)
    - [9.2 Expressions](#92-expressions)
    - [9.3 Literals](#93-literals)
    - [9.4 Blocks](#94-blocks)
    - [9.5 Prefix.pch, Info.plist, AppDelegate](#95-prefixpch-infoplist-appdelegate)

## 1. Purpose

- Develop reliable and maintainable application code with Object-C.
- The naming conventions, coding standards and best practices described in this document are compiled from KMS developer&#39;s own experiences and by referring to Apple coding guidelines.

## 2. Naming
### 2.1 General Principles
#### 2.1.1 Clarify

- Develop reliable and maintainable application code.
- It is good to be both clear and brief as possible, but clarity shouldn&#39;t suffer because of brevity:

|Code | Commentary|
|---|---|
|insertObj ect: atIndex: | Good.|
|insert:at: | Not clear; what is being inserted? what does "at" signify?|
|removeObjectAtIndex: | Good.|
|removeObject: | Good, because it removes object referred to in argument.|
|remove: | Not clear; what is being removed?|

- In general, don&#39;t abbreviate names of things. Spell them out, even if they&#39;re long:
|Code | Commentary|
|---|---|
|destinationSelection| Good|
|destSel| Not clear|
|setBackgroundColor| Good|
|setBkgdColor| Not clear|

You may think an abbreviation is well known, but it might not be, especially if the developer encountering your method or function name has a different cultural and linguistic background.

- Avoid ambiguity in API names, such as method names that could be interpreted in more than one way.

|Code | Commentary|
|---|---|
|sendPort| Does it send the port or return it?|
|displayName| Does it display a name or return the receiver's title in the user interface?|

#### 2.1.2 Consistency

- Try to use names consistently throughout the Cocoa programmatic interfaces. If you are unsure, browse the current header files or reference documentation for precedents.
- Consistency is especially important when you have a class whose methods should take advantage of polymorphism. Methods that do the same thing in different classes should have the same name.

|Code | Commentary|
|---|---|
|- (NSInteger)tag|Defined in NSView, NSCell, NSControl|
|- (void)setStringValue:(NSString *)|Defined in a number of Cocoa classes|

#### 2.1.3 No Self Reference

- Names shouldn&#39;t be self-referential.

|Code | Commentary|
|---|---|
|NSString|Okay|
|NSStringObject|Self-referential|

- Constants that are masks (and thus can be combined in bitwise operations) are an exception to this rule, as are constants for notification names.

|Code | Commentary|
|---|---|
|NSUnderlineByWordMask|Okay|
|NSTableViewColumnDidMoveNotification|Okay|

### 2.2 File Names

- File names should reflect the name of the class implementation that they contain—including case. Follow the convention that your project uses.
- File names for categories should include the name of the class being extended, e.g. GTMNSString+Utils.h or GTMNSTextView+Autocomplete.h.
- All class files should be stored in the Classes directory unless they belong to another subproject or library. The only files that should be in the root of the project are: Prefix.pch, Info.plist and main.m.

### 2.3 Naming Classes

- AVOID using generic class names like ViewController or TextParser because it&#39;s possible a framework you include in your app may fail to follow conventions and create classes with the same names.
- In order to keep class names unique, the convention is to use prefixes on all classes. You&#39;ll have noticed that Cocoa and Cocoa Touch class names typically start either with NS or UI. Use two-letter prefixes likes these are reserved by Apple for use in framework classes.

### 2.4 Naming Methods

- Start the name with a lowercase letter and capitalize the first letter of embedded words. Don&#39;t use prefixes.
- Use keywords before all arguments.
- For methods that represent actions an object takes, start the name with a verb:

```cpp
    - (void)invokeWithTarget:(id)target;
    - (void)selectTabViewItem:(NSTabViewItem *)tabViewItem
```

_Do not use &quot;do&quot; or &quot;does&quot; as part of the name because these auxiliary verbs rarely add meaning._

- If a method includes an error pointer parameter to be set if an error occurred, this should be the last parameter to the method.
- If a method takes a block, the block parameter should be the last parameter in order to make any method invocations as readable as possible when specifying a block inline. For the same reason, it&#39;s best to avoid methods that take multiple block arguments, wherever possible.
- Any method that is empty or just calls super should be removed from the source code as they are redundant. In case a method is required by the implementation of a protocol and nothing should be done, a single comment line must be used to indicate this is intentional.
- Private methods should always be created in a class extension for simplicity since a named category can&#39;t be used if it adds or modifies any properties.

### 2.5 Naming Functions

- Function names are formed like method names, but with a couple exceptions:
  - They start with the same prefix that you use for classes and constants.
  - The first letter of the word after the prefix is capitalized.
- Most function names start with verbs that describe the effect the function has: NSHighlightRect, NSDeallocateObject

### 2.6 Naming Properties and Data Types
#### 2.6.1 Declared Properties and Instance Variables

- If the property is expressed as a noun or a verb, the format is:

```cpp
    @property (strong) NSString *title;
    @property (assign) BOOL showsAlpha;
```

- If the name of a declared property is expressed as an adjective, however, the property name omits the &quot;is&quot; prefix but specifies the conventional name for the get accessor, for example:

```cpp
    @property (assign, getter = isEditable) BOOL editable;    
```

- Each @synthesize should be on a single line and should synthesize a member-variable with a leading \_. (When LLVM 4.0 is used, a manual synthesize should be omitted and autosynthesization should be used.)

```cpp
    @property(nonatomic, strong) UIColor *topColor;
    @property(nonatomic, assign) CGSize shadowOffset;
    @property(nonatomic, unsafe_unretained, readonly) UIActivityIndicatorView *activityIndicator;
    @property(nonatomic, getter = isLoading) BOOL loading;
```
- If you need to declare an instance variable, explicitly declare it with either @private or @protected.
- If an instance variable is to be an accessible attribute of instances of the class, make sure you write accessor methods for it (when possible, use declared properties).

#### 2.6.2 Constants

- Use enumerations for groups of related constants that have integer values.
- Use const to create constants for floating point values. You can use const to create an integer constant if the constant is unrelated to other constants; otherwise, use enumeration.
- Define constants for strings used for such purposes as notification names and dictionary keys. By using string constants, you are ensuring that the compiler verifies the proper value is specified (that is, it performs spell checking).

### 2.7 Naming Notifications and Exceptions

- Notification names should always follow the following naming scheme:
- Class of Affected Object + Did/Will + Action + &quot;Notification&quot;

```cpp
    UIApplicationWillResignActiveNotification
```

- Exceptions are identified by global NSString objects whose names are composed in this way: [Prefix] + [UniquePartOfName] + Exception
- The unique part of the name should run constituent words together and capitalize the first letter of each word. Here are some examples:

```cpp
    NSApplicationDidBecomeActiveNotification
    NSWindowDidMiniaturizeNotification
    NSTextViewDidChangeSelectionNotification
    NSColorPane1ColorDidChangeNotification
```
### 2.8 Naming Categories

- Categories should be named for the sort of functionality they provide. Don&#39;t create umbrella categories.
- Categories should mainly be used for code where the implementation is not available (framework code) and should be avoided if possible, because they can create name clashes and weird bugs. Categories should always be named like follows:

```cpp
    @interface UITableView (NGLoading)
    @interface UITableView (TVLoading)
```

-  When using a category to add methods to an existing framework class, you should include a prefix on the method name to avoid clashes.

### 2.9 Acceptable Abbreviations and Acronyms

In general, you shouldn&#39;t abbreviate names when you design your programmatic interface. However, the abbreviations listed below are either well established or have been used in the past, and so you may continue to use them. There are a couple of additional things to note about abbreviations:

- Abbreviations that duplicate forms long used in the standard C library—for example, alloc and getc —are permitted.
-  You may use abbreviations more freely in argument names (for example, imageRep , col (for column), obj, and otherWin).

|Abbreviation |Meaning and comments|
|---|---|
|nib |Interface Builder archive.|
|pboard |Pasteboard (but only in constants).|
|rect |Rectangle.|
|Rep |Representation (used in class name such as NSBitmapImageRep).|
|temp |Temporary.|
|vert |Vertical.|

|Abbreviation |Meaning and comments|
|---|---|
|alloc |Allocate.|
|alt |Alternate.|
|app |Application. For example, NSApp the global application object. However, “application” is spelled out in delegate methods, notifications, and so on.|
|calc |Calculate.|
|dealloc |Deallocate.|
|func |Function.|
|horiz |Horizontal.|
|info |Information.|
|init |Initialize (for methods that initialize new objects).|
|int |Integer (in the context of a C int—for an NSInteger value, use integer).|
|max |Maximum.|
|min |Minimum.|
|msg |Message.|

- You may use abbreviations and acronyms that are common in the computer industry in place of the words they represent. Here are some of the better-known acronyms:

| |
|---|
| ASCII |
| PDF |
| XML |
| HTML |
| URL |
| RTF |
| HTTP |
| TIFF |
| JPG |
| PNG |
| GIF |
| LZW |
| ROM |
| RGB |
| CMYK |
| MIDI |
| FTP |

## 3. Layout and Indentation

- Tabs, not spaces
- End files with a newline.
- One space should be used between the - or + and the return type, and no spacing in the parameter list except between parameters.
- Method brackets should be on the following line and flush left. Code should be indented 2 spaces from the opening bracket.
- When brackets are needed in a switch they are to be left aligned with the case line and on their own line. NOTE: brackets in switches should be avoided.
- All other brackets should inline.
- If you have too many parameters to fit on one line, giving each its own line is preferred. If multiple lines are used, align each using the colon before the parameter.

```cpp
    - (void)doSomethingWith: (GTMFoo *)theFoo
                       rect: ( NSRect )theRect
                   interval: (float )theInterval {

    }
```

- When the first keyword is shorter than the others, indent the later lines by at least four spaces, maintaining colon alignment:

```cpp
    - (void)short:(GTMFoo *)theFoo
                longKeyword:(NSRect)theRect
          evenLongerKeyword:(float)theInterval
         error:(NSError **):theError {

    }

```

- Don&#39;t use any of these styles:

```cpp
    [myObject doFooWith:arg1 name:arg2 // some lines with >1 arg
                error:arg3];

    [myObject doFooWith:arg1
                name:arg2 error:arg3];

    [myObject doFooWith:arg1
        name:arg2 // aligning keywords instead of colons
        error:arg3];
```


## 4. Code Comments

- Comments should be at the same level of indent as the code that they are commenting on.
- One-line comments // are preferred to multiline /\*\*/ comments. Comments should be used to document why something is happening and not what is happening and should be used to explain situations that are not trivial.
- Todos should be marked as follows as should contain a brief description of what there is to do:

```cpp
    // TODO: Fix the Bug XYZ that happens when the user cLicks on the second button while the App is Loading
```

## 5. Properties

- **AVOID** explicitly declaring public instance variables.
- If the property is nonatomic, it should be first.
- The next option should **ALWAYS** be strong, weak, or assign since if it is omitted, there is a warning.
- readonly should be the next option if it is specified.
- readwrite should never be specified in header file.
- readwrite  should only be used in class extensions to overwrite a specified readonly in the header file.
- getter or setter should be last, setter should rarely be used, getter should mainly be used for BOOL properties.
- Explicitly defined iVars for properties should be omitted:

```cpp
    @interface MyClass : NSObject {

    }
    @property(nonatomic, retain) Foo* foo;
    @end

```

Instead of

```cpp
    @interface MyClass : NSObject {
        Foo* foo;
    }
    @property(nonatomic, retain) Foo* foo;
    @end
```

## 6. Exceptions

- DON&#39;T use exceptions for flow controlling.
- Use exceptions only to indicate programmer error.
- To indicate errors, use an NSError\*\* argument or use NSError as return value as suggested by Apple.

## 7. Logging

- DO log the actual error with all possible information (e.g. parameters, SQL statement, file data). This will help a lot in diagnosing problems.
- AVOID log the critical information (e.g. credit card number, SSN). Consider encrypt critical information in log if the information logging is required.
- Although not required, it is recommended that test code is written before production code (i.e. test-first approach). Whether test-first or test-last is applied, never delay the act of writing test code.
- DON&#39;T use NSLog in production mode, defined log is recommended

```cpp
    #ifdef DEBUG
        #define DLog(fmt, ...) HSLog((@"%s [Line %d] " fmt),
    __PRETTY_FUNCTION__, __LINE__, ##__VA_ARGS__);
    #else
        #define DLog(...)
        #define NSLog(...)
    #endif
```
## 8. Unit Test

- Although not required, it is recommended that test code is written before production code (i.e. test-first approach). Whether test-first or test-last is applied, never delay the act of writing test code.
- Write one or more unit test cases to reproduce any defect found by QA team.
- Follow these principles when writing unit test code:

- **Automatic:** The whole testing process must be automated. Do not rely on any manual process such as data population, environment configuration etc. Test code must do all those things.
- **Complete:** Test anything that can possibly break. When you are in doubt whether something can possibly go wrong or not, write a test.
- **Repeatable:** All test cases must be able to run and rerun repeatedly and produce the same result every time. If it doesn&#39;t, they are not reliable and must be fixed.
- **Independent:** Each test case must be configured and run in isolation from one another. Do not make any assumption that one test must be executed before another.
- **Production-like:** Test code must be treated like production code and subject to strict review. That means each and every coding convention in this document is very well applicable to test code.
- **Fast:** Test cases must run fast. If they do not, mock out the heavy dependencies (like database) to make them run fast.

## 9. Miscellaneous
### 9.1 Pragma Mark

- There should be a pragma mark before each group, formatted like above (A good tip is to create a Xcode snippet with the above layout and use the key pragma for example).

```cpp
    ////////////////////////////////////////////////////////////////////////
    #pragna mark - Lifecycle

    ////////////////////////////////////////////////////////////////////////

    - (void)dealloc {
        // Unregister Notifications, cLean up etc.
    }

    ////////////////////////////////////////////////////////////////////////
    #pragna mark - UIView
    ////////////////////////////////////////////////////////////////////////

    - (id)layoutSubviews {
        [super layoutSubviews];
        // Stuff
    }

    - (void)drawRect:(CGRect)rect {
        // Drawing code
    }

```

### 9.2 Expressions

- DON&#39;T access an iVar (Instance Variable) unless you&#39;re in -init, -dealloc or a custom accessor.
- Use dot-syntax when invoking idempotent methods, including setters.
- Use object literals, boxed expressions, and subscripting over the older, grosser alternatives.
- Comparisons should be explicit for everything except BOOLs.
- Objective-C uses YES and NO. Therefore true and false are incorrect. Also since nil resolves to NO it is unnecessary to compare it in conditions.
- Prefer positive comparisons to negative.
- Never use more than one ternary operator in single line
- Long form ternary operators should be wrapped in parentheses and only used for assignment and arguments.

```cpp
    Blah *a = (stuff == thing ? foo : bar);
```

- Short form, nil coalescing ternary operators should avoid parentheses.

```cpp
    Blah *b = thingThatCouldBeNil ?: defaultValue;
```
- Separate binary operands with a single space, but unary operands and casts with none:

```cpp
    void *ptr = &value + 10 * 3;
    NewType a = (NewType)b;

    for (int i = 0; i < 10; i++) {
        doCoolThings();
    }
```
### 9.3 Literals

- **AVOID** making numbers a specific type unless necessary (for example, prefer 5 to 5.0, and 5.3 to 5.3f).
- The contents of array and dictionary literals should not have a space on both sides.
- Dictionary literals should have a single space between the key and the colon, and a single space between colon and value.

```cpp
    NSArray *theStuff = @[@1, @2, @3];
    NSDictionary *keyedStuff = @{NSDidCreateStyleGuide : @YES};
```

- Longer or more complex literals should be split over multiple lines (optionally with a terminating comma):

```cpp
    NSArray *theStuff = @[
         @"Got some long string objects in here.",
        [AndSomeModelObjects too],
        @"Moar strings."
    ];

    NSDictionary *keyedStuff = @{
        @"this.key": @"corresponds to this value",
        @"otherKey": @"remoteData.payload",
        @"some": @"more",
        @"JSON": @"keys",
        @"and": @"stuff",
    };
```
### 9.4 Blocks

- Blocks should have a space between their return type and name.
- Block definitions should omit their return type when possible.
- Block definitions should omit their arguments if they are void.
- Parameters in block types should be named unless the block is initialized immediately.

```cpp
    void (^blockName1)(void) = ^{
        // do some things
    };

    id (^blockName2)(id) = ^id (id args) {
        // do some things
    };
```

### 9.5 Prefix.pch, Info.plist, AppDelegate

- The pre-compiled header should always be named Prefix.pch and not Project\_Prefix.pch or anything else.
- The info.plist should always be named Info.plist and not Project\_Info.plist or anything else.
- The application delegate, if its a separate class, should be named AppDelegate and not Project\_AppDelegate or anything else.
- String constants should be #define and stored in the Prefix.pch. The exception is a #define that is highly local to a specific class.
