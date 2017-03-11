# KMS Android Coding Standards

- [1. Purpose](#1-purpose)
- [2. Naming](#2-naming)
    - [2.1. General](#21-general)
    - [2.2. Naming Field](#22-naming-field)
- [3. Layout & Indentation](#3-layout--indentation)
- [4. Code Comments](#4-code-comments)
- [5. Exceptions](#5-exceptions)
- [6. Logging](#6-logging)
- [7. Unit Test](#7-unit-test)
- [8. Miscellaneous](#8-miscellaneous)
    - [8.1. Using standard Java annotations](#81-using-standard-java-annotations)
    - [8.2. Package and Import statement](#82-package-and-import-statement)

## 1. Purpose

* Develop reliable and maintainable application code
* The naming conventions, coding standards and best practices described in this document are compiled from KMS developer’s own experiences and by referring to Java/Android coding guidelines

## 2. Naming

### 2.1. General

Identifier Type | Rules for Naming | Examples
--------------- | ---------------- | --------
Packages | The prefix of a unique package name is always written in all- lowercase ASCII letters and should be one of the top-level domain names, currently com, edu, gov, mil, net, org, or one of the English two-letter codes identifying countries as specified in ISO Standard 3166, 1981. Subsequent components of the package name vary according to an organization's own internal naming conventions. Such conventions might specify that certain directory name components be division, department, project, machine, or login names. | `com.sun.eng` <br> `com.apple.quicktime.v2` <br> `edu.cmu.cs.bovik.cheese`
Classes | Class names should be nouns, in mixed case with the first letter of each internal word capitalized. Try to keep your class names simple and descriptive. Use whole words-avoid acronyms and abbreviations (unless the abbreviation is much more widely used than the long form, such as URL or HTML). | `class Raster;` <br> `class ImageSprite;`
Interfaces | Interface names should be capitalized like class names and always prefix with capital “I”. | `interface IDelegate;` <br> `interface IStoring;`
Methods | Methods should be verbs, in mixed case with the first letter lowercase, with the first letter of each internal word capitalized. | `run();` <br> `runFast();` <br> `getBackground();`
Variables | Except for variables, all instance, class, and class constants are in mixed case with a lowercase first letter. Internal words start with capital letters. Variable names should not start with underscore _ or dollar sign $ characters, even though both are allowed.<br><br>Variable names should be short yet meaningful. The choice of a variable name should be mnemonic- that is, designed to indicate to the casual observer the intent of its use. One- character variable names should be avoided except for temporary "throwaway" variables. Common names for temporary variables are i, j, k, m, and n for integers; c, d, and e for characters. | `int i;` <br> `char c;` <br> `float myWidth;`
Constants | The names of variables declared class constants and of ANSI constants should be all uppercase with words separated by underscores ("_"). (ANSI constants should be avoided, for ease of debugging.) | `static final int MIN_WIDTH = 4;` <br> `static final int MAX_WIDTH = 999;`

### 2.2. Naming Field

* Non-public, non-static field names start with m
* Static field names start with s
* Other fields start with a lower case letter
* Public static final fields (constants) are ALL_CAPS_WITH_UNDERSCORES

## 3. Layout & Indentation

* DO use 4 whitespaces for each nested level of code
* DO NOT nest code any more than 3 levels of depth
* DO use one blank line to separate blocks of code
* CONSIDER break single long line of code to multiple lines of code with level indentations

## 4. Code Comments

* Use Javadoc standard comments
* Comments should be at the same level of indent as the code that they are commenting on
* One-line comments // are preferred to multiline /**/ comments. Comments should be used to document why something is happening and not what is happening and should be used to explain situations that are not trivial
* Todos should be marked as follows as should contain a brief description of what there is to do, TODOs should include the string TODO in all caps, followed by a colon:<br>
    `// TODO: Remove this code after the UrlTable2 has been checked in`<br>
  and<br>
    `// TODO: Change this to use a flag instead of a constant`<br>
  If your TODO is of the form "At a future date do something" make sure that you either include a very specific date ("Fix by November 2005") or a very specific event ("Remove this code after all production mixers understand protocol V7.")
  
## 5. Exceptions

* DON’T ignore exceptions. You must handle every Exception in your code in some principled way. The specific handling varies depending on the case
* DON’T catch generic exceptions. Try to separate the exceptions by rethrowing, using multiple try blocks or using catch blocks for each exception
* Once you catch the exception, you should log it appropriately

## 6. Logging

* Use TAG in your logs
* CONSIDER using log levels:
    * FATAL: Should be used in extreme cases, where immediate attention is needed. This level can be useful to trigger a support engineer's pager
    * ERROR: Indicates a bug, or a general error condition, but not necessarily one that brings the system to a halt. This level can be useful to trigger email to an alerts list, where it can be filed as a bug by a support engineer
    * WARN: Not necessarily a bug, but something someone will probably want to know about. If someone is reading a log file, they will typically want to see any warnings that arise
    * INFO: Used for basic, high-level diagnostic information. Most often good to stick immediately before and after relatively long-running sections of code to answer the question "What is the app doing?" Messages at this level should avoid being very chatty
    * DEBUG: Used for low-level debugging assistance

## 7. Unit Test

* Although not required, it is recommended that test code is written before production code (i.e. test-first approach). Whether test-first or test-last is applied, never delay the act of writing test code. 
* Write one or more unit test cases to reproduce any defect found by QA team. 
* Follow these principles when writing unit test code:
    * Automatic: The whole testing process must be automated. Do not rely on any manual process such as data population, environment configuration etc. Test code must do all those things. 
    * Complete: Test anything that can possibly break. When you are in doubt whether something can possibly go wrong or not, write a test. 
    * Repeatable: All test cases must be able to run and rerun repeatedly and produce the same result every time. If it doesn’t, they are not reliable and must be fixed. 
    * Independent: Each test case must be configured and run in isolation from one another. Do not make any assumption that one test must be executed before another. 
    * Production-like: Test code must be treated like production code and subject to strict review. That means each and every coding convention in this document is very well applicable to test code. 
    * Fast: Test cases must run fast. If they do not, mock out the heavy dependencies (like database) to make them run fast. 

## 8. Miscellaneous

### 8.1. Using standard Java annotations

* @Deprecated: The @Deprecated annotation must be used whenever the use of the annotated element is discouraged. If you use the @Deprecated annotation, you must also have a @deprecated Javadoc tag and it should name an alternate implementation. In addition, remember that a @Deprecated method is still supposed to work
* @Override: The @Override annotation must be used whenever a method overrides the declaration or implementation from a super-class
* @SuppressWarnings: The @SuppressWarnings annotation should only be used under circumstances where it is impossible to eliminate a warning. If a warning passes this "impossible to eliminate" test, the @SuppressWarnings annotation must be used, so as to ensure that all warnings reflect actual problems in the code

### 8.2. Package and Import statement

* The first non-comment line of most Java source files is a package statement. After that, import statements can follow. For example:<br>
  `package java.awt;`<br>
  `import java.awt.peer.CanvasPeer;`
* The ordering of import statements is:
    * Android imports
    * Imports from third parties (com, junit, net, org)
    * java and javax
* To exactly match the IDE settings, the imports should be:
    * Alphabetical within each grouping, with capital letters before lower case letters (e.g. Z before a).
    * There should be a blank line between each major grouping (android, com, junit, net, org, java, javax).
    * USE the latter for importing all Android code. An explicit exception is made for java standard libraries


