# KMS Java Coding Standards

- [1. Introduction](#1-introduction)
- [2. Formatting](#2-formatting)
    - [2.1. Indentation](#21-indentation)
    - [2.2. Comments](#22-comments)
    - [2.3. Statements](#23-statements)
    - [2.4. Java Source Layout](#24-java-source-layout)
- [3. Naming Conventions](#3-naming-conventions)
    - [3.1. Package Naming](#31-package-naming)
    - [3.2. Class Naming](#32-class-naming)
    - [3.3. Interface Naming](#33-interface-naming)
    - [3.4. Enumeration Naming](#34-enumeration-naming)
    - [3.5. Operation Naming](#35-operation-naming)
    - [3.6. Field Naming](#36-field-naming)
    - [3.7. Local Variable Naming](#37-local-variable-naming)
    - [3.8. Exception Naming](#38-exception-naming)
    - [3.9. Unit-test Naming](#39-init-test-naming)
    - [3.10. UI Component Naming](#310-ui-component-naming)
- [4. Comments](#4-comments)
    - [4.1. Legal Comments](#41-legal-comments)
    - [4.2. Informative Comments](#42-informative-comments)
    - [4.3. Explanation of Intent](#43-explanation-of-intent)
    - [4.4. Warning of Consequences](#44-warning-of-consequences)
    - [4.5. TODO Comments](#45-todo-comments)
    - [4.6. Javadocs in Public APIs](#46-javadocs-in-public-apis)
    - [4.7. Some Bad Comments](#47-some-bad-comments)
- [5. Methods](#5-methods)
    - [5.1. Do One Thing](#51-do-one-thing)
    - [5.2. Use Descriptive Names](#52-use-descriptive-names)
    - [5.3. Size of a Method](#53-size-of-a-method)
    - [5.4. Method Arguments](#54-method-arguments)
    - [5.5. DRY – Don’t Repeat Yourself](#55-dry–dont-repeat-yourself)
- [6. Unit-Tests](#6-unit-tests)
    - [6.1. Keeping Tests Clean](#61-keeping-tests-clean)
    - [6.2. F.I.R.S.T](#62-first)
    - [6.3. Unit-Test Smells](#63-unit-test-smells)
- [7. Design & Best Practicest](#7-design--best-practices)
    - [7.1. Encapsulations](#71-encapsulations)
    - [7.2. Interfaces and Inheritances](#72-interfaces-and-inheritances)
    - [7.3. Structure over Convention](#73-structure-over-convention)
    - [7.4. Exceptions and Error Handlings](#74-exceptions-and-error-handlings)
    - [7.5. Constant interface pattern](#75-constant-interface-pattern)
    - [7.6. Concurrency](#76-concurrency)
- [8. References](#8-references)

## 1. Introduction

This document describes a collection of standards, conventions, and guidelines for writing solid Java code. They are based on sound, proven software engineering principles that lead to code that is easy to understand, to maintain, and to enhance. Furthermore, code conventions are important to programmers for a number of reasons: 

* 80% of the lifetime cost of a piece of software goes to maintenance
* Hardly any software is maintained for its whole life by the original author.
* Code conventions improve the readability of the software, allowing engineers to understand new code more quickly and thoroughly.
* If you ship your source code as a product, you need to make sure it is as well packaged and clean as any other product you create.

Experience shows that by taking the time to write high-quality code right from the start you will have a much easier time modifying it during the development process. Finally, following a common set of coding standards leads to greater consistency, making teams of developers significantly more productive. For the conventions to work, everyone writing software must conform to the code conventions.

## 2. Formatting

Code formatting is about communication, and communication is the professional developer’s ﬁrst order of business.

### 2.1. Indentation

Four spaces should be used as the unit of indentation. Tabbing should only be used when the editor translates it into spaces. Vertical justified indentation should be used for group matching parenthesis and brackets when the expression or code section is bigger than one line.

**Line Length**

It is allowed lines are less than 120 characters.

**Wrapping Lines**

When a line is too long, consider reducing nesting by encapsulation. If an expression still will not fit on a single line, break it according to these general principles: 

* Do not reduce the length of a descriptive method or variable name just to make an expression fit on one line.
* Break after a comma.
* Break before an operator.
* Prefer higher-level breaks to lower-level breaks.
* Align the new line with the beginning of the expression at the same level on the previous line.
* If the above rules lead to confusing code or to code that’s squished up against the right margin, just indent 8 spaces instead.

Some examples:

```java
aLongFunctionName(aVeryVeryLongExpression1, aVeryVeryLongExpression2,
        aVeryVeryLongExpression3, aVeryVeryLongExpression4,
        aVeryVeryLongExpression5);

Object var = aLongFunctionName1(aVeryVeryLongExpression1,
                                aLongFunctionName2(
                                        aVeryVeryLongExpression2,
                                        aVeryVeryLongExpression3));
```

```java
// DO
longName1 = longName2 * (longName3 + longName4 - longName5)
        + 4 * longName6;

// DON'T
longName1 = longName2 * (longName3 + longName4
        - longName5) + 4 * longName6;
```

```java
// DO
if ((condition1 && condition2)
        || (condition3 && condition4)
        ||!(condition5 && condition6)) {
    doSomethingAboutIt();
}

// DO
if ((condition1 && condition2) || (condition3 && condition4)
        ||!(condition5 && condition6)) {
    doSomethingAboutIt();
}

// DON'T
if ((condition1 && condition2)
    || (condition3 && condition4)
    ||!(condition5 && condition6)) {
    doSomethingAboutIt();
}
```

```java
result = (aLongBooleanExpression) ? longName1 : longName2;

result = (aLongBooleanExpression) ? aVeryVeryLongExpression1
        : aVeryVeryLongExpression2;

result = (aLongBooleanExpression)
        ? aVeryVeryLongExpression1
        : aVeryVeryLongExpression2;
```

### 2.2. Comments

Sometimes it is useful to comment out code while you are developing or debugging. However, never leave these commented-out lines in the code when it is checked in. This is what source code configuration is for. If you have multiple working versions of your code, check both in so you can switch between them and we have a record of your changes.

Comment Type | Usage | Example
------------ | ----- | -------
Documentation Comments | Documentation comments are processed by javadoc, to produce API documentation in HTML format. Use documentation comments immediately before declarations of interfaces, classes, member functions, and fields. | `/**`<br>`*`<nbsp>`This`<nbsp>`is`<nbsp>`javadoc`<nbsp>`comments`<br>`*/`
C-style Comments | The javadoc program ignores C-style comments. Use C-style comments for multi-line comments that are not part of the API documentation. | `/*`<br>`*`<nbsp>`This`<nbsp>`is`<nbsp>`non-javadoc`<nbsp>`comments`<br>`*/`
Single-line Comments | The javadoc program ignores Single-line comments. Use single line comments internally within member functions to document business logic, sections of code, and declarations of temporary variables. | `//`<nbsp>`This`<nbsp>`is`<nbsp>`single`<nbsp>`line`<nbsp>`comments`

### 2.3. Statements

**Simple Statements**

Each line should contain at most one statement. Example:

```java
// DO
count++;
count--;

// DON'T
count++; count--;
```

**Compound Statements**

Compound statements are statements that contain lists of statements enclosed in braces:

```java
{
    <statement>
}
```

* The enclosed statements should be indented one more level than the compound statement.
* Braces are used around all statements, even single code-line statements, when they are part of a control structure, such as a if-else or for statement. This makes it easier to add statements without accidentally introducing bugs due to forgetting to add braces.

**return Statements**

A return statement with a value should not use parentheses unless they make the return value more obvious in some way. Example:

```java
return 1;
return products.size();
return (size < 10 ? size : DEFAULT_SIZE);
```

**if-else Statements**

The if-else class of statements should have the following form:

```java
if (condition1) {
    <statements>
} else if (condition2) {
    <statements>
} else {
    <statements>
}

return 1;
```

**if** statements always use braces {}.
Positive conditionals are easier to read than negative conditionals.

**for Statements**

A for statement should have the following form:

```java
for (<initialization>; <condition>; <update>) {
    <statements>
}
```

An empty for statement (one in which all the work is done in the initialization, condition, and update clauses) should have the following form:

```java
for (<initialization>; <condition>; <update>);
```

When using the comma operator in the initialization or update clause of a **for** statement, avoid the complexity of using more than three variables. If needed, use separate statements before the **for** loop (for the initialization clause) or at the end of the loop (for the update clause).

**while Statements**

A **while** statement should have the following form:

```java
while (<condition>) {
    <statements>
}
```

An empty while statement should have the following form:

```java
while (<condition>);
```

**do-while Statements**

A **do-while** statement should have the following form:

```java
do {
    <statements>
} while (<condition>);
```

**switch Statements**

A **switch** statement should have the following form:

```java
switch (status) {
    case ABC:
        <statements>
        /* falls through */
    case DEF:
        <statements>
        break;
    case XYZ:
        <statements>
        break;
    default:
        <statements>
        break;
}
```

Every time a case falls through (doesn’t include a **break** statement), add a comment where the **break** statement would normally be. This is shown in the preceding code example with the /\* falls through \*/ comment. Every **switch** statement should include a **default** case. The **break** in the **default** case is redundant, but it prevents a fall-through error if later another case is added.

**try-catch Statements**

A **try-catch** statement should have the following format:

```java
try {
    <statements>
} catch (Exception e) {
    <statements>
}
```

A **try-catch** statement may also be followed by **finally**, which executes regardless of whether or not the try block has completed successfully:

```java
try {
    <statements>
} catch (Exception e) {
    <statements>
} finally {
    <statements>
}
```

### 2.4. Java Source Layout

Each Java source file contains a single public class or interface. When private classes and interfaces are associated with a public class, you can put them in the same source file as the public class. The public class should be the first class or interface in the file. Java source files have the following ordering:

* File comments
* Package and Import statements
* Type comments
* Class and interface declarations
* Class-members and interface-members declarations

```java
// Copyright (c) 2017 KMS Technology, Inc.
package com.kmstechnology.demoapp;

import java.util.ArrayList;
import java.util.List;

/**
* A demo class presents a suggestion of Java file layout
*
* @author trungnguyen
*
*/

public class DemoApp {
    public static final String VERSION = "1.0";
    private static final List<String> INSTANCES = new ArrayList<String>();
        
    public static int countInstances() {
        return INSTANCES.size();
    }

    private final String name;
    private boolean stopped;
    public DemoApp(String name) {
        this.name = name;
        INSTANCES.add(name);
    }
    
    public String getName() {
        return name;
    }

    public boolean isStopped() {
        return stopped;
    }

    public void setStopped(boolean stopped) {
        this.stopped = stopped;
    }
}
```

**package and import Statements**

It’s recommended to avoid using the wildcards like the import **java.util.*** and prefer **java.util.List** for greater readability and to clearly know which classes are used by this class.

**Always Initialize Static Fields**

Static fields, also known as class fields, should be given valid values because you cannot assume that instances of a class will be created before a static field is accessed.

**Declare one local variable per line of code**

This is consistent with one statement per line of code and makes it possible to document each variable with an inline comment.

## 3. Naming Conventions

We will be discussing naming conventions throughout the standards, so let's set the stage with a few basics: 

* Use full English descriptors that accurately describe the variable/field/class. For example, use names like **firstName**, **grandTotal**, or **CorporateCustomer**. Although names like **x1**, **y1**, or **fn** are easy to type because they are short, they do not provide any indication of what they represent and result in code that is difficult to understand, maintain, and enhance. 
* Use terminology applicable to the domain. If your users refer to their clients as customers, then use the term **Customer** for the class, not **Client**. Many developers will make the mistake of creating generic terms for concepts when perfectly good terms already exist in the industry/domain. 
* Use mixed case to make names readable. You should use lower case letters in general, but capitalize the first letter of class names and interface names, as well as the first letter of any non-initial word.
* Use abbreviations sparingly, but if you do so then use them intelligently. This means you should maintain a list of standard short forms (abbreviations), you should choose them wisely, and you should use them consistently. For example, if you want to use a short form for the word **number**, then choose one of **nbr**, **no**, or **num**, document which one you chose (it does not really matter which one), and use only that one. 
* Avoid names that are similar or differ only in case. For example, the variable names **persistentObject** and **persistentObjects** should not be used together, nor should **anSqlDatabase** and **anSQLDatabase**. 
* Avoid leading or trailing underscores. Names with leading or trailing underscores are usually reserved for system purposes, and may not be used for any user-created names except for pre-processor defines. More importantly, underscores are annoying and difficult to type so try to avoid their use whenever possible. 
* Do Not "Hide" Names: Name hiding refers to the practice of naming a local variable, argument, or fields the same (or similar) as that of another one of greater scope. For example, if you have a field called **firstName** do not create a local variable or parameter called **firstName**, or anything close to it like **firstNames** or **fistName**. This makes your code difficult to understand and prone to bugs because other developers, or you, will misread your code while they are modifying it and make difficult to detect errors.

### 3.1. Package Naming

There are several rules associated with the naming of packages. In order, these rules are:

* Local package names begin with an identifier that is not all upper case. Local packages are ones that are used internally within your organization and that will not be distributed to other organizations. Examples of these package names include **demoapp.persistence** and **demoapp.ui**. 
* Global package names begin with the reversed Internet domain name for your organization. A package that is to be distributed to multiple organizations should include the name of the originating organization's domain name, with the top-level domain type capitalized. For example, to distribute the previous packages, they would be named **com.kmstechnology.demoapp.persistence**, **com.kmstechnology.demoapp.ui**

### 3.2. Class Naming

The standard Java convention is to use a full English descriptor starting with the first letter capitalized using mixed case for the rest of the name. Class names shall be in singular form.

```java
public class Customer {
    // ...
}

public class Employee {
    // ...
}

public class Order {
    // ...
}

public class OrderItem {
    // ...
}
```

### 3.3. Interface Naming

The Interface shares the same naming with Class.

A note for method members in an interface: By default, they are public access modifiers, so don’t repeat public keyword in their method signatures

```java
public interface UserService {
    // DON'T
    public UserStatus getUserStatus();

    //DO
    UserStatus getUserStatus();
}
```

### 3.4. Enumeration Naming

The Enumeration shares the same naming with Class. All enumeration items should be all words capitalized.

```java
public enum RecordStatus {
    AWAITING_REVIEW,
    IN_PROCESS,
    IN_ERROR,
    PROCESSED,
    MIGRATED
}
```

### 3.5. Operation Naming

Operations should be named using a full English description, using mixed case with the first letter of any non-initial word capitalized. It is also common practice for the first word of an operation name to be a strong, active verb.

```java
public void execute(Command command) {
    // ...
}

public void exportUsers(List<User> users, OutputStream output) {
    // ...
}

public boolean authenticate(String username, String password) {
    // ...
    return false;
}
```

**Getters**

Getters are operations that return the value of a field. You should prefix the word get to the name of the field, unless it is a **boolean** field and then you prefix **is** to the name of the field instead of get. 

```java
private boolean active;
private String email;

public boolean isActive() {
    return active;
}

public String getEmail() {
    return email;
}
```

**Setters**

Setters, also known as mutators, are operations that modify the values of a field. You should prefix the word **set** to the name of the field, regardless of the field type.

```java
public void setActive(boolean active) {
    this.active = active;
}

public void setEmail(String email) {
    this.email = email;
}
```

**Collections Naming Accessors**

Member Function Type | Naming Convention | Example
-------------------- | ----------------- | -------
Getter for the collection | `getCollection()` | `getOrderItems()`
Setter for the collection | `setCollection()` | `setOrderItems()`
Insert an object into the collection | `insertObject()` | `insertOrderItem()`
Delete an object from the collection | `deleteObject()` | `deleteOrderItem()`
Create and add a new object into the collection | `newObject()` | `newOrderItem()`

The advantage of this approach is that the collection is fully encapsulated, allowing you to later replace it with another structure, perhaps a linked list or a B-tree.

**Operation Parameters Naming**

Parameters should be named following the exact same conventions as for local variables and fields. Use the word this as a prefix of field name to avoid the name hiding problem in case the parameter name is the same with field name.

```java
private Command command;
public void execute(Command command) {
    this.command = command;
    // ...
}
```

### 3.6. Field Naming

You should use a full English descriptor to name your fields to make it obvious what the field represents. Fields that are collections, such as arrays or vectors, should be given names that are plural to indicate that they represent multiple values. All first letters of non-initial words should be capitalized.

```java
private String firstName;
private String zipCode;
private BigDecimal unitPrice;
private double discountRate;
private List<OrderItem> orderItems;
```

**Constants Naming**
In Java, constants, values that do not change, are typically implemented as static final fields of classes. The recognized convention is to use full English words, all in uppercase, with underscores between the words.

```java
public static final double MINIMUM_BALANCE = 10.0;
public static final int MAX_FILE_SIZE = 10 * 1024;
public static final Date DEFAULT_START_DATE = new Date();
```

Replace all Magic Numbers / Strings with named constants to give them a meaningful name when meaning cannot be derived from the value itself.

For the class that implemented **Serializable** interface, the **serialVersionUID** variable should be followed the form:

```java
private static final long serialVersionUID = <yyyyMMdd>L;
```

For the logger, it should be followed the form:

```java
private static final Logger Logger = LoggerFactory.getLogger(<ClassName>.class);
```

### 3.7. Local Variable Naming

In general, local variables are named following the same conventions as used for fields, in other words use full English descriptors with the first letter of any non-initial word in uppercase. 

Don’t use a local variable that has the same name as a class member variable.

**Streams Naming**

When there is a single input and/or output stream being opened, used, and then closed within a member function the common convention is to use **input** and **output** for the names of these streams, respectively.

```java
InputStream input = null;
OutputStream output = null;
try {
    input = new FileInputStream("...");
    output = new FileOutputStream("...");

    IOUtils.copy(input, output);
} catch (IOException e) {
    // ...
} finally {
    IOUtils.cLoseQuietLy(output);
    IOUtils.cLoseQuietLy(input);
}
```

**Loop Counters Naming**

Because loop counters are a very common use for local variables, and because it was acceptable in C/C++, in Java programming the use of **i**, **j**, or **k**, is acceptable for loop counters. If you use these names for loop counters, use them consistently.

```java
for (int i=1; i<MAX_ROWS; i++) {
    for (int j=1; j<MAX_COLUMNS; j++) {
        // ... 
    }
    // ...
}
```

**Exception Objects Naming**

Because exception handling is also very common in Java coding the use of the letter **e** for a generic exception is considered acceptable.

```java
try {
    // ...
} catch (Exception e) {
    // ...
}
```

**Collections Naming**

A collection, such as an array or a vector, should be given a pluralized name representing the types of objects stored by the array. The name should be a full English descriptor with the first letter of all non-initial words capitalized.

For a map, It should be followed the pattern **valuesByKeys**

```java
List<User> users = new ArrayList<User>();
Command[] commands = new Command[MAX_COMMANDS];
Map<String, User> usersByEmails = new HashMap<String, User>();
```

### 3.8. Exception Naming

Exceptions should be name with a short name describing the error suffixed by the word **Exception**

```java
public class UserNotFoundException extends Exception {
    private static final long serialVersionUID = 20131210L;

    // ...
}

public class AuthenticationFailedException extends Exception {
    private static final long serialVersionUID = 20131210L;

    // ...
}
```

### 3.9. Unit-test Naming

Classes used for unit testing of code should be prefixed with **Test** followed by the name of the class to be tested. In contrast, a test method would model some kind of action, like **testMethodName**. A per-package test class called **TestAll** may also be specified.

```java
public class ExpenseService {
    public ExpenseErrors submitExpense(Expense expense) {
        // ...
    }
}

public class ExpenseServiceTest {
    public void testSubmitExpenseWithNoError() {
        // ...
    }

    public void testSubmitExpenseWithErrors() {
        // ...
    }
}
```

### 3.10. UI Component Naming

For names of components you should use a full English descriptor postfixed by the component type. This makes it easy for you to identify the purpose of the component as well as its type, making it easier to find each component in a list (many visual programming environments provide lists of all components in an applet or application and it can be confusing when everything is named **button1**, **button2** etc.).

```java
private JButton okButton;
private JList customerList;
private JMenu fileMenu;
private JMenuItem newFileMenuItem;
```

## 4. Comments

Some comments are necessary or beneﬁcial. We’ll look at a few that I consider worthy of the bits they consume. Keep in mind, however, that the only truly good comment is the comment you found a way not to write.

### 4.1. Legal Comments

Sometimes our corporate coding standards force us to write certain comments for legal reasons. For example, copyright and authorship statements are necessary and reasonable things to put into a comment at the start of each source ﬁle.

```java
// Copyright (c) 2017 KMS Technology, Inc.
```

Where possible, refer to a standard license or other external document rather than putting all the terms and conditions into the comment.

### 4.2. Informative Comments

It is sometimes useful to provide basic information with a comment:

```java
// format matched kk:mm:ss EEE, MMM dd, yyyy
Pattern timeMatcher = Pattern.compile("\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```

It might have been better, and clearer to use the name of the function to convey the information where possible:

```java
// Returns an instance of the Responder being tested.
protected abstract Responder responderInstance();
vs
protected abstract Responder responderBeingTested();
```

### 4.3. Explanation of Intent

Sometimes a comment goes beyond just useful information about the implementation and provides the intent behind a decision

```java
public int compareTo(Object o) {
    if (o instanceof WikiPagePath) {
        WikiPagePath p = (NikiPagePath) o;
        String compressedName = StringUtils.join(names, "");
        String compressedArgumentName = StringUtils.join(p.names, "");
        return compressedName.compareTo(compressedArgumentName);
    }
    return 1; // we are greater because we are the right type.
}
```

### 4.4. Warning of Consequences

Sometimes it is useful to warn other programmers about certain consequences

```java
public static SimpleDateFormat makeStandardHttpDateFormat() {
    // SimpleDateFormat is not thread safe,
    // so we need to create each instance independently.
    SimpleDateFormat df = new SimpleDateFormat("EEE, dd MMM  yyyy HH:mm:ss z");
    df.setTimeZone(TimeZone.getTimeane("GMT"));
    return df;
}
```

### 4.5. TODO Comments

TODOs are jobs that the programmer thinks should be done, but for some reason can’t do at the moment. It might be a reminder to delete a deprecated feature or a plea for someone else to look at a problem. It might be a request for someone else to think of a better name or a reminder to make a change that is dependent on a planned event. Whatever else a TODO might be, it is not an excuse to leave bad code in the system.

```java
// TODO these are not needed
// We expect this to go away when we do the checkout model
protected VersionInfo makeVersion() throws Exception {
    return null;
}
```

### 4.6. Javadocs in Public APIs

There is nothing quite so helpful and satisfying as a well-described public API. The javadocs for the standard Java library are a case in point. It would be difﬁcult, at best, to write Java programs without them. If you are writing a public API, then you should certainly write good javadocs for it.

### 4.7. Some Bad Comments

Redundant Comments: The comment probably takes longer to read than the code itself

```java
// Utility method that returns when this.closed is true. Throws an exception
// if the timeout is reached.
public synchronized void waitForClose(final long timeoutMillis) throws Exception {
    if(!closed) {
        wait(timeoutMillis);
        if(!closed) {
            throw new Exception("MockResponseSender could not be closed");
        }
    }
}
```

Mandated Comments: Comments like below just clutter up the code, propagate lies, and lend to general confusion and disorganization

```java
/**
*
* @param title The title of the CD
* @param author The author of the CD
* @param tracks The number of tracks on the CD
* @param durationInMinutes The duration of the CD in minutes
*/
public void addCD(String title, String author, int tracks, int durationInMinutes) {
    CD Cd = new CD();
    cd.title = title;
    cd.author = author;
    cd.tracks = tracks;
    cd.duration = durationInMinutes;
    cdList.add(cd);
}
```

Noise Comments: comments restate the obvious and provide no new information

```java
public class AnnualDateRule {
    /** The day of the month. */
    private int dayOfMonth;

    /** Default constructor. */
    protected AnnualDateRule() {
    }
}
```

Closing Brace Comments: if you ﬁnd yourself wanting to mark your closing braces, try to shorten your functions instead

```java
public static void main(String[] args) {
    BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
    String line;
    int lineCount = 0;
    int charCount = 0;
    int wordCount = 0;
    try {
        while ((line = in.readLine()) != null) {
            lineCount++;
            charCount += line.length();
            String words[] = line.split("\\W");
            wordCount += words.length;
        } //while
        System.out.println("wordCount = " + wordCount);
        System.out.println("lineCount = " + lineCount);
        System.out.println("charCount = " + charCount);
    } // try
    catch (IOException e) {
        System.err.println("Error:" + e.getMessage());
    } //catch
} //main
```

Commented-Out Code: Source code control systems will remember the code for us. We don’t have to comment it out any more. Just delete the code

```java
InputStreamResponse response = new InputStreamResponse();
response.setBody(formatter.getResultStream(), formatter.getByteCount());
// InputStream resultsStream = formatter.getResultStream();
// StreamReader reader = new StreamReader(resultsStream);
// response.setContent(reader.read(formatter.getByteCount()));
```

Too Much Information: Don’t put interesting historical discussions or irrelevant descriptions of details into your Comments

## 5. Methods

Every system is built from a domain-speciﬁc language designed by the programmers to describe that system. Methods are the verbs of that language, and classes are the nouns. Your methods should be short, well named, and nicely organized.

### 5.1. Do One Thing

A method is doing more than “one thing” is if you can extract another function from it with a name that is not merely a restatement of its implementation

### 5.2. Use Descriptive Names

Don’t be afraid to make a name long. A long descriptive name is better than a short enigmatic name

### 5.3. Size of a Method

* 20-50 lines long at most
* 80-120 characters each line long at most
* code blocks within if, else ,while should be one line long
* indent level should NOT be greater than one or two

### 5.4. Method Arguments

Arguments are even harder from a testing point of view. Imagine the difﬁculty of writing all the test cases to ensure that all the various combinations of arguments work properly.

To avoid method arguments that more than 3, uses argument objects instead. 

```java
public abstract Circle makeCircle(double x, double y, double radius);
// vs.
public abstract Circle makeCircle(Point center, double radius);
```

To avoid flag argument, separate functions for each case.

```java
public abstract void render(boolean isSuite);
// vs.
public abstract void renderForSuite();
public abstract void renderForSingleTest();
```

To avoid output argument, use this keyword because this is intended to act as an output argument in OOP.

```java
public void appendFooter(StringBuffer report) {
    // ...
}

Formater formatter = new Formater();
// vs.
public class Report {
    // ...
    private StringBuffer render = new StringBuffer();
    // ...
    public void appendFooter() {
        this.render.append("...");
    }
    // ...
}
report.appendFooter();
```

### 5.5. DRY – Don’t Repeat Yourself

Duplication may be the root of all evil in software. Consider also how object-oriented programming serves to concentrate code into base classes that would otherwise be redundant. Structured programming, Aspect Oriented Programming, Component Oriented Programming, are all, in part, strategies for eliminating duplication.

## 6. Unit-Tests

Tests are as important to the health of a project as the production code is. Perhaps they are even more important, because tests preserve and enhance the ﬂexibility, maintainability, and reusability of the production code. So keep your tests constantly clean.

### 6.1. Keeping Tests Clean

* Unit-Test should not be maintained to the same standards of quality as their production code.
* Having dirty tests is better than having no tests.
* Test code is just as important as production code
* Use the SetUp / TearDown methods only for infrastructure that your unit-test needs. Do not use it for anything that is under test.
* Clean Test: Builds up the test data (Given). The second part operates on that test data (When). Checks that the operation yielded the expected results. (Then)
* Single Scenario per Test

```java
public void testGetPageHierarchyAsXml() throws Exception {
    givenPages("PageOne", "PageOne.ChildOne", "PageTwo");
    whenRequestIsIssued("root", "type:pages");
    thenResponseShouldBeXML();
}

public void testGetPageHierarchyHasRightTags() throws Exception {
    givenPages("PageOne", "PageOne.ChildOne", "PageTwo");
    whenRequestIsIssued("root", "type:pages");
    thenResponseShouldContain("PageOne", "PageTwo", "ChildOne");
}
```

### 6.2. F.I.R.S.T

**F**ast: Unit-tests have to be fast in order to be executed often. Fast means much smaller than seconds.

**I**ndependent: Clear when the failure happened. No dependency between tests (random order).

**R**epeatable: No assumed initial state, nothing left behind, no dependency on external services that might be unavailable (databases, file system …)

**S**elf-validating: No manual test interpretation or intervention. Red or green!

**T**imely: Tests are written at the right time. TDD (Test Driven Development): Red – green – refactor, test a little – code a little. DDT (Defect Driven Testing): Write a unit test that reproduces the defect – Fix code – Test will succeed – Defect will never return. POUTing (Plain Old Unit Testing, aka. Test After): Write unit tests to check existing code, you cannot and probably do not want to test drive everything.

### 6.3. Unit-Test Smells

**Test Not Testing Anything**: Passing test that at first sight appears valid but does not test the testee. 

**Checking Internals**: A test that accesses internals (private/protected members) of the testee directly (Reflection). This is a refactoring killer. 

**Test Only Running on Developer’s Machine**: A test that is dependent on the development environment and fails elsewhere. Use continuous integration to catch them as soon as possible. 

**Test Checking More than Necessary**: A test that checks more than it is dedicated to. The test fails whenever something changes that it checks unnecessarily. Especially probable when fakes are involved or checking for item order in unordered collections. 

**Chatty Test**: A test that fills the console with text – probably used once to manually check for something. 

**Test Swallowing Exceptions**: A test that catches exceptions and lets the test pass. 

**Test Not Belonging in Host Test Fixture**: A test that tests a completely different testee than all other tests in the fixture. 

**Hidden Test Functionality**: Test functionality hidden in either the SetUp method, base class or helper class. The test should be clear by looking at the test method only – no initialisation or asserts somewhere else. 

**Conditional Test Logic**: Tests should not have any conditional test logic because it’s hard to read. 

**Test Logic in Production Code**: Tests depend on special logic in production code. 

**Erratic Test**: Sometimes passes, sometimes fails due to left overs or environment.

## 7. Design & Best Practices

For some good Object-oriented code design guidelines, see the Gang of Four book or the ObjectMentor website: http://www.objectmentor.com/

### 7.1. Encapsulations

It’s important to keep data and behavior as encapsulated as possible to reduce dependencies and therefore increase the maintainability of the system. These following guidelines should be considered in your design to increase encapsulation:

* Aim to make all of your instance variables private and provide accessor methods only where necessary.
* Make accessor methods for instance variables “final”.
* Only use protected instance variables or protected constructors in well-defined packages
* Use packages to manage complexity
* If a class is only used within a package, make it package local (default visibility) to reduce system-level coupling.
* Avoid using inner classes, an inner class only makes sense, and should only be used, if it is going to associate and be visible only to the class that contains it.

### 7.2. Interfaces and Inheritances

A well-designed system is set with assignment well-defined responsibilities and interfaces. The interface defines the “contract” that a class should meet and it’s essential to the development of large systems. The interface concept can be implemented in different ways, like abstract classes or actual Java interfaces. Most people tend to abuse of the use of inheritance when what they really needed was interfaces. Creating deep class hierarchies generate large dependencies and therefore less maintainability. Below some guidelines: 

* Keep inheritance hierarchies small
* Prefer delegation or using utility classes over inheritance for reuse
* Program to an interface, not to an implementation
* If a class is designed to be inherited, but it does not make sense to have an instance of the class, it should be defined as abstract

### 7.3. Structure over Convention

Enforce design decisions with structure over convention. Naming conventions are good, but there are inferior to structures that force compliance.

### 7.4. Exceptions and Error Handlings

The general philosophy is to use exceptions only for errors: logic and programming errors, configuration errors, corrupted data, resource exhaustion, etc. The general rule is that the systems in normal condition and in the absence of overload or hardware failure should not raise any exceptions.  Keep in mind that throwing an exception is a very expensive operation in Java. Unwinding the stack and forming String objects requires many CPU cycles. Never program by exceptions. If you can anticipate a situation, include it in your code rather than using an exception to signal it.

Avoid putting more than one **try/catch** block in a method. In general, all methods should follow this form:

```java
public void doSomething() throws SomeException {
    <initializations>
    try {
        <code that throws exceptions>
    } catch (SomeException e) {
        throw e;
    } catch (SomeOtherException e) {
        <create a new SomeException se from e>
        throw se;
    } catch (Exception e) {
        <create a new SomeExcention se from e>
        throw se;
    } finally {
        <cleanup>
    }
}
```

If you find that you need to nest try/catch blocks, consider encapsulating the nested block in a new method that handles the special exception.

**Exception Factory**

Every Application should have an exception handling framework. You should use a message ID to create exceptions within the code. Never use the new operator to create an exception. 

Here is the procedure you should follow when creating an exception

* Decide on an appropriate message and exception class. You may subclass Exception or use it directly. 
* Check the existing exception hierarchy and message catalog to see if an appropriate exception/message pair already exists.
* If an appropriate exception doesn’t already exist, check out the message catalog and add a new message/exception class pair. You may choose an appropriate string identifier for your message that is descriptive. If you need to pass additional static parameters to your exception constructor, put them in the message catalog as well.
* If necessary, write the new exception class.
* In your code, use an ExceptionFactory to generate the new exception. You may include an exception to be nested and any special purpose properties when creating this exception.

**Additional Exception Guidelines**

* Never, ever, consume an exception without taking an action. This form is unacceptable:

```java
try {
    <code that throws exceptions>
} catch (SomeException e) {
    // do nothing
}
```

* Use exceptions to handle logic and programming errors, configuration errors, corrupted data, and resource exhaustion. 

```java
// DON'T 
if (doSomething()) { 
    if (doSomethingElse()) { 
        if (doSomethingElseAgain()) { 
            // ... 
        } else {
            // handle doSomethingElseAgain failed 
        }
    } else { 
        // handle doSomethingElse failed 
    } 
} else { 
    // handle doSomething failed
}
```

```java
// D0
try {
    doSomething();
    doSomethingElse();
    doSomethingElseAgain();
} catch (SomethingException e) {
    // handle doSomething failed
} catch (SomethingElseException e) {
    // handle doSomethingElse failed
} catch (SomethingElseAgainException e) {
    // handle doSomethingElseAgain failed
}
```

* Report exceptions by the appropriate logging mechanism as early as possible, including at the point of raise.
* Minimize the number of exceptions exported from a given abstraction by categorizing them and using a constant (typesafe) to represent the condition
* Do not use exceptions for frequent, anticipated events. 
* Do not use exceptions to implement control structures.
* Make sure status codes have an appropriate value.
* Perform safety checks locally; do not expect your client to do so.
* Catch as many exceptions as possible explicitly – avoid catch(Exception) as the only exception handler
* Separate fatal and non-fatal exception hierarchies
* Never let exceptions propagate out a finally block
* Never declare throws Exception, always use a subclass of the base Application Exception.

### 7.5. Constant interface pattern

Avoid declaring constant variables in an interface

```java
public interface UserService {
    String SYSTEM_USERNAME = "system";
    int AWAITING_QUEUE_SIZE = 20;

    int AWAITING_APPROVAL_STATUS = 1;
    int ACTIVE_SIATUS = 2;
    int LOCKED_SIATUS = 3;

    void approveUser(String username);

    int getUserStatus();
```

An **enum** may be a better approach. Or you could simply put the constants as public static fields in a class that cannot be instantiated

```java
public final class UserConstants {
    public static final String SYSTEM_USERNAME = "system";
    public static final int AWAITING_QUEUE_SIZE = 20;

    private UserConstants() {
    }
}

public enum UserStatus {
    AWAITING_APPROVAL,
    ACTIVE,
    LOCKED
}
```

### 7.6. Concurrency

What follows is a series of principles and techniques for defending your systems from the problems of concurrent code:

* Keep your concurrency-related code separate from other code.
* Limit the scope of data. Take data encapsulation to heart; severely limit the access of any data that may be shared.
* Use Copies of Data. A good way to avoid shared data is to avoid sharing the data in the ﬁrst place. In some situations it is possible to copy objects and treat them as read-only. In other cases it might be possible to copy objects, collect results from multiple threads in these copies and then merge the results in a single thread.
* Threads should be as independent as possible. Attempt to partition data into independent subsets than can be operated on by independent threads, possibly in different processors.
* Review the classes available to you. In the case of Java 5, become familiar with **java.util.concurrent**, **java.util.concurrent.atomic**, **java.util.concurrent.locks**.
* Keep your synchronized sections as small as possible. 
* Write tests that have the potential to expose problems and then run them frequently, with different programmatic conﬁgurations and system conﬁgurations and load. If tests ever fail, track down the failure. Don’t ignore a failure just because the tests pass on a subsequent run.

## 8. References

* Java Code Conventions [http://www.oracle.com/technetwork/java/codeconventions-150003.pdf]
* EASS – Java Coding Guidelines
* Clean Code: A Handbook of Agile Software Craftsmanship [book]
* Clean Code Cheat Sheet [http://www.planetgeek.ch/wp-content/uploads/2013/06/Clean-Code-V2.2.pdf]


