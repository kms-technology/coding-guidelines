# KMS .NET Coding Standards

- [1. Purpose](#1-purpose)
- [2. Naming](#2-naming)
    - [2.1 Casing Style](#2-1-casing-style)
    - [2.2 Capitalization Rules for Identifiers](#2-2-capitalization-rules-for-identifiers)
    - [2.3 Capitalizing Compound Words and Common Terms](#2-3-capitalizing-compound-words-and-common-terms)
    - [2.4 General Naming Conventions](#2-4-general-naming-conventions)
        - [2.4.1 Word Choice](#2-4-1-word-choice)
        - [2.4.2 Using Abbreviations and Acronyms](#2-4-2-using-abbreviations-and-acronyms)
    - [2.5 Names of Assemblies and DLLs](#2-5-names-of-assemblies-and-dlls)
    - [2.6 Names of Namespaces](#2-6-names-of-namespaces)
        - [2.6.1 General rules](#2-6-1-general-rules)
        - [2.6.2 Namespaces and Type Name Conflicts](#2-6-2-namespaces-and-type-name-conflicts)
    - [2.7 Names of Classes, Structs, and Interfaces](#2-7-names-of-classes-structs-and-interfaces)
        - [2.7.1 Names of Generic Type Parameters](#2-7-1-names-of-generic-type-parameters)
        - [2.7.2 Naming Enumerations](#2-7-2-naming-enumerations)
    - [2.8 Names of Type Members](#2-8-names-of-type-members)
        - [2.8.1 Names of Methods](#2-8-1-names-of-methods)
        - [2.8.2 Names of Property](#2-8-2-names-of-property)
        - [2.8.3 Names of Events](#2-8-3-names-of-events)
        - [2.8.4 Names of Fields](#2-8-4-names-of-fields)
    - [2.9 Naming Resources](#2-9-naming-resources)
- [3. Layout &amp; Indentation](#3-layout-amp-indentation)
- [4. Methods](#4-methods)
- [5. Exceptions](#5-exceptions)
    - [5.1 Exception Throwing](#5-1-exception-throwing)
    - [5.2 Exception Handling](#5-2-exception-handling)
    - [5.3 Exceptions and Performance](#5-3-exceptions-and-performance)
        - [5.3.1 Tester-Doer Pattern](#5-3-1-tester-doer-pattern)
        - [5.3.2 Try-Parse Pattern](#5-3-2-try-parse-pattern)
- [6. Logging](#6-logging)
- [7. Code Comments](#7-code-comments)
- [8. String Manipulation](#8-string-manipulation)
- [9. Unit Test](#9-unit-test)
- [10. Miscellaneous](#10-miscellaneous)
- [11. ASP.NET Web Form controls naming](#11-aspnet-web-form-controls-naming)
- [12. Managed Threading Best Practices](#12-managed-threading-best-practices)
    - [12.1 Understand Deadlocks and Race Conditions](#12-1-understand-deadlocks-and-race-conditions)
        - [12.1.1 Deadlocks](#12-1-1-deadlocks)
        - [12.1.2 Race Conditions](#12-1-2-race-conditions)
    - [12.2 General Recommendations](#12-2-general-recommendations)
- [13. SharePoint Best Practices](#13-sharepoint-best-practices)
    - [13.1 Best Practices with Event Receivers](#13-1-best-practices-with-event-receivers)
    - [13.2 Caching SharePoint Objects That Are Not Thread-Safe](#13-2-caching-sharepoint-objects-that-are-not-thread-safe)
    - [13.3 Working with Folders and Lists](#13-3-working-with-folders-and-lists)
    - [13.4 Deleting Multiple Versions of a List Item](#13-4-deleting-multiple-versions-of-a-list-item)
    - [13.5 Using SPQuery Object](#13-5-using-spquery-object)
    - [13.6 Using Disposable Windows SharePoint Services Objects](#13-6-using-disposable-windows-sharepoint-services-objects)



## 1. Purpose

- Develop reliable and maintainable application code.
- The naming conventions, coding standards and best practices described in this document are compiled from KMS developers own experiences and by referring to Microsoft guidelines.

## 2. Naming
### 2.1 Casing Style

- Pascal Casing: The first letter in the identifier and the first letter of each subsequent concatenated word are capitalized. You can use Pascal case for identifiers of three or more characters. For example: BackColor, FrontColor.
- Camel Casing: The first letter of an identifier is lowercase and the first letter of each subsequent concatenated word is capitalized. For example: backColor, foreColor
- Uppercase: All letters in the identifier are capitalized. For example: IO, DB.

### 2.2 Capitalization Rules for Identifiers

- **DO** use Pascal casing for all public member, type, and namespace names consisting of multiple words.
- **DO** use Camel casing for parameter names.

<table>
<tr>
  <th>Identifier</th><th>Casing</th><th>Example</th>
</tr>
<tr>
  <td>Namespace</td>
  <td>Pascal</td>
  <td>namespace KMS.CodingStandard {....}</td>
</tr>
<tr>
  <td>Type</td>
  <td>Pascal</td>
  <td>public class BinaryStreamWriter {....}</td>
</tr>
<tr>
  <td>Interface</td>
  <td>Pascal</td>
  <td>public interface IStreamWriter {....}</td>
</tr>
<tr>
  <td>Method</td>
  <td>Pascal</td>
  <td>
    <pre>public class BinaryStreamWriter 
{
    public void Write(byte[] data)  {....}
}</pre>
  </td>
</tr>
<tr>
  <td>Property</td>
  <td>Pascal</td>
  <td>
    <pre>public class Stream 
{
    public long Length  { get; }
}</pre>
  </td>
</tr>
<tr>
  <td>Event</td>
  <td>Pascal</td>
  <td>
    <pre>public class Process 
{
    public EventHandler Existed;
}</pre>
  </td>
</tr>
<tr>
  <td>Public Field</td>
  <td>Pascal</td>
  <td>
    <pre>public class MessageQueue
{
    public static readonly TimeSpan Timeout;
}</pre>
  </td>
</tr>
<tr>
  <td>Private Field</td>
  <td>Camel</td>
  <td>
    <pre>public class MessageQueue
{
    public Queue&lt;Message&gt; internalQueue;
}</pre>
  </td>
</tr>
<tr>
  <td>Constant</td>
  <td>Pascal</td>
  <td>
    <pre>public class MessageQueue
{
    public const int MaxQueueLength = 500;
}</pre>
  </td>
</tr>
<tr>
  <td>Enum</td>
  <td>Pascal</td>
  <td>
    <pre>public enum FileMode
{
    CreateNew,
    Append,
    ...
}</pre>
  </td>
</tr>
<tr>
  <td>Parameter</td>
  <td>Camel</td>
  <td>
    <pre>public class Converter
{
    public int ToInt32(string value) {...}
}</pre>
  </td>
</tr>
</table>


 ### 2.3 Capitalizing Compound Words and Common Terms

- **DO NOT** capitalizes each word in so-called closed-form compound words. For example: use endpoint, Endpoint, not EndPoint, nor endPoint.

| Pascal | Camel | Not |
| --- | --- | --- |
| BitFlag | bitFlag | Bitflag |
| Callback | callback | CallBack |
| Email | email | EMail |
| FileName | fileName | Filename |
| Hashtable | hashtable | HashTable |

### 2.4 General Naming Conventions

- **DO** use self-explanatory names for everything (interfaces, classes, methods, variables etc.)
- **DO NOT** sacrifice length for clarity. Long but communicative names are much better than short but convoluted names.

#### 2.4.1 Word Choice

- **DO** choose easily readable identifier names. For example, a property named HorizontalAlignment is more English-readable than AlignmentHorizontal.
- **DO** favor readability over brevity. The property name CanScrollHorizontally is better than ScrollableX (an obscure reference to the X-axis).
- **DO NOT** use underscores, hyphens, or any other non-alphanumeric characters.
- **DO NOT** use Hungarian notation, e.g. bConfirm, iCount.
- **CONSIDER** prefix Boolean variables and properties with &quot;can&quot;, &quot;is&quot; or &quot;has&quot;. Example:
```csharp
  public class Command
  {
    private bool canExecute = false;
    public bool CanExecute { get; }
    public bool HasExecute { get; }
  }
```

- Do not include the parent class name within a property name. Example:
```csharp
  public class Customer
  {
    // DO
    public string Address { ... }
    // DO NOT
    public string CustomerAddress {...}
  }
```

- **AVOID** using identifiers that conflict with keywords of widely used programming languages. Uses the **@** sign as an escape mechanism in this case, for example @class, @dynamic. However, it is still a good idea to avoid common keywords because it is much more difficult to use a method with the escape sequence than one without it.

#### 2.4.2 Using Abbreviations and Acronyms

- **DO NOT** use abbreviations or contractions as part of identifier names. For example, use GetWindow rather than GetWin.
- **DO NOT** uses any acronyms that are not widely accepted, and even if they are, only when necessary.
- **DO** use a generic CLR type name, rather than a language-specific name, in the rare cases when an identifier has no semantic meaning beyond its type.
```csharp
  // DO 
  long ConvertToInt64(object value)
  // DO NOT
  long ConvertToLong(object value)
```

- **DO** use a common name, such as value or item, rather than repeating the type name, in the rare cases when an identifier has no semantic meaning and the type of the parameter is not important.
```csharp
  // DO 
  long ConvertToInt64(object value)
  // DO NOT
  long ConvertToInt64(object valueObject)
```

### 2.5 Names of Assemblies and DLLs

- **DO** choose names for your assembly DLLs that suggest large chunks of functionality, such as System.Data, System.IO.
- **CONSIDER** name DLLs according to the following pattern: &lt;Company&gt;.&lt;Component&gt;.dll where &lt;Component&gt; contains one or more dot-separated clauses. For example: Web.Controls.dll

### 2.6 Names of Namespaces

#### 2.6.1 General rules

- **DO** follow the template : &lt;Company&gt;.(&lt;Product&gt;|&lt;Technology&gt;)[.&lt;Feature&gt;][.&lt;Subnamespace&gt;]. For example: Security.Authentications.
- **DO** prefix namespace names with a company name to prevent namespaces from different companies from having the same name.
- **DO NOT** use organizational hierarchies as the basis for names in namespace hierarchies, because group names within corporations tend to be short-lived. Organize the hierarchy of namespaces around groups of related technologies.
- **DO** use Pascal casing, and separate namespace components with periods (e.g., QualityAssurance.qTest). If your brand employs nontraditional casing, you should follow the casing defined by your brand, even if it deviates from normal namespace casing (e.g. use qTrace instead of QTrace or Qtrace).
- **CONSIDER** using plural namespace names where appropriate. For example, use Collections instead of Collection. Brand names and acronyms are exceptions to this rule, however. For example, use IO instead of IOs.
- **DO NOT** use the same name for a namespace and a type in that namespace.

#### 2.6.2 Namespaces and Type Name Conflicts

- **DO NOT** introduce generic type names such as Element, Node, Log, and Message. You should qualify the generic type names (FormElement, XmlNode, EventLog, SoapMessage).
- **DO NOT** give the same name to types in namespaces within a single application model.

### 2.7 Names of Classes, Structs, and Interfaces

- **DO** name classes and structs with nouns or noun phrases, using Pascal casing.
- **DO** prefix interface names with the letter I, to indicate that the type is an interface.
- **DO** name interfaces with adjective phrases, or occasionally with nouns or noun phrases.
```csharp
  public interface IExecutable {...}
  public class Command : IExecutable {...}
```

- **DO NOT** give class names a prefix (e.g., &quot;C&quot;).
- **CONSIDER** ending the name of derived classes with the name of the base class. Example:
```csharp
  public abstract class Repositoty {...}
  public sealed class EmployeeRepository : Repositoty {...}
```

#### 2.7.1 Names of Generic Type Parameters

- **CONSIDER** using T as the type parameter name for types with one single-letter type parameter.
```csharp
  public int IComparer<T> {...}
  public delegate bool Predicate<T>(T item);
  public struct Nullable<T> where T:struct {...}
```

- **DO** prefix descriptive type parameter names with T.
```csharp
  public interface ISessionChannel<TSession> 
    where TSession : ISession {...}
```

#### 2.7.2 Naming Enumerations

- **DO** use a singular type name for an enumeration unless its values are bit fields.
```csharp
  public enum UserRole
  {
    Guest,
    Subsriber,
    Administrator
  }
  [Flags]
  public enum Permissions
  {
    Read = 0,
    Write =1
  }
```

- **DO NOT** use a prefix on enumeration value names (e.g., &quot;ad&quot; for ADO enums, &quot;rtf&quot; for rich text enums, etc.).

### 2.8 Names of Type Members
#### 2.8.1 Names of Methods

- **DO** give methods names that are verbs or verb phrases.
```csharp
  public class String
  {
    public int CompareTo(...){...}
    public string[] Split(...) {...}
    public string Trim() {...}
  }
```

- DO suffix asynchronous method name by &quot;Async&quot;
```csharp
  private static async Task FooAsync()
  {
    await Task.Delay(1000);
    Console.WriteLine("Done with first delay");
    await Task.Delay(1000);
  }
```

#### 2.8.2 Names of Property

- **DO** name properties using a noun, noun phrase, or adjective.
- **DO NOT** have properties that match the name of &quot;Get&quot; methods as in the following example:
```csharp
  public string Body { get;set }
  public string GetBody() {....}
```
- **DO** name collection properties with a plural phrase describing the items in the collection instead of using a singular phrase followed by &quot;List&quot; or &quot;Collection&quot;.
```csharp
  // DO
  public ICollection<Person> Persons { get;set; }
  // DO NOT
  public ICollection<Person> PersonCollection { get;set; }
```

#### 2.8.3 Names of Events

- **DO** name events with a verb or a verb phrase. For example: Clicked, Painting, DroppedDown.
- **DO** give events names with a concept of before and after, using the present and past tenses.
- **DO NOT** use &quot;Before&quot; or &quot;After&quot; prefixes or postfixes to indicate pre- and post-events. Use present and past tenses as just described.

#### 2.8.4 Names of Fields

- **DO** name fields using a noun, noun phrase, or adjective.

### 2.9 Naming Resources

- **DO** use Pascal casing in resource keys.
- **DO** use only alphanumeric characters and underscores in naming resources.
- **DO** use the following naming convention for exception message resources: &lt;ExceptionType&gt;&lt;SpecificError&gt;. For example: ArgumentExceptionIllegalCharacters, ArgumentExceptionInvalidName.

## 3. Layout &amp; Indentation

- **DO** use 4 whitespaces for each nested level of code.
- **DO NOT** nest code any more than 3 levels of depth.
- **DO** use one blank line to separate blocks of code.
- **CONSIDER** break single long line of code to multiple lines of code with level indentations.
```csharp
  using <ReferenceNamespacesAndAlias>
  namespace <Namespace>
  {
    public class <ClassName>
    {
      public void Method()
      {
        // Method content
      }
      public void MethodWithManyParameters(
          string <parameter1>,
          string <parameter2>,
          long <parameter3>,
          bool <parameter4>)
        {
           // Method content
        }
    }
  }
```

## 4. Methods

- **DO** write methods which do one and only one job.
- **AVOID** methods which have more than 30 lines of code.
- Public methods must validate their input arguments. Use the prescribed Design By Contract (DBC) library to perform such validation. For example:
```csharp
  public ICollection<Person> SearchPersons(string firstName, string lastName)
  {
    // Do validate input parameter
    if(string.IsNullOrEmpty(firstName))
      throw new ArgumentNullException("firstName");
    if(string.IsNullOrEmpty(lastName))
      throw new ArgumentNullException("lastName"); 
    
    // Do actual method logic  

  }
```

- **AVOID** writing methods accepting any more than 5 parameters. Consider use a class or struct to wrap those parameters instead.
```csharp
  // DO NOT
  public ICollection<Person> SearchPerson(
    string firstName,
    string lastName,
    DateTime? dateOfBirth,
    string email,
    bool isActive,
    bool hasChild)
  {
    ...
  }
  // DO 
  public ICollection<Person> SearchPerson(SearchPersonCriteria criteria)
  {
    ...
  }
```

- DRY (Don&#39;t Repeat Yourself). That is NEVER allowing duplication in code. Refactor duplicated code into new methods of same or different class.
- **DO** return empty collection instead of null.
- To return (or receive) data as collection of objects, use interface (IEnumerable&lt;T&gt; , ICollection&lt;T&gt;, IList&lt;T&gt;, ..) instead of concrete class. Prefer using ICollection&lt;T&gt; for common case.
```csharp
  // DO 
  public IList<Person> GetAllPersons() {...}
  // DO NOT
  public List<Person> GetAllPersons() {...}
```

## 5. Exceptions
### 5.1 Exception Throwing

- **DO** report execution failures by throwing exceptions.
- **DO NOT** return error codes.
```csharp
  // DO NOT 
  public void Execute(out int errorCode)
  {
    // Case 1 failed
    errorCode = 100;
    ...
    // Case 2 failed 
    errorCode = 200;
    ...
    // Success
    errorCode = 0;
  }
  // DO 
  public void Execute()
  {
    // Case 1 failed
    throw new ABCException("Case 1 failed");
    ...
    // Case 2 failed 
    throw new CDEException("Case 2 failed");
    ...
    // Success
    ...
  }
```

- **DO NOT** use exception as a flow control structure. Exceptions are for exceptional cases only.
```csharp
  // DO NOT 
  public void Execute()
  {
    try
    {
      // Execute normal case 
      ...
      // If failed 
      throw new ABCException();
    }
    catch(ABCException)
    {
      // Execute alternative case
      ...
    }
  }
```

- **DO** throw the most specific exceptions which match the current level of abstraction. For examples:

- Do not throw [SqlException](https://www.assembla.com/wiki/show/pe_gameworld/SqlException) to the GUI because that makes the GUI depends on the low-level implementation details. Throw a high-level exception like [InsufficientBalance](https://www.assembla.com/wiki/show/pe_gameworld/InsufficientBalance) instead
- Never throw Exception. Use a more specific exception (either custom-built or built-in) instead.

- **DO NOT** throw or derive from ApplicationException, use Exception instead. It was originally thought that custom exceptions should derive from the ApplicationException class; however in practice this has not been found to add significant value.
- **DO NOT** give error messages like &quot;Error in Application&quot;, &quot;There is an error&quot; etc. Instead give specific messages like &quot;Failed to update database. Please make sure the login id and password are correct&quot;.
- **DO** show short and friendly message to the user. But log the actual error with all possible information. This will help a lot in diagnosing problems.
- **DO** not put critical information in the message field of exception objects.
- **DO NOT** use throw ex, instead use throw to rethrow an exception to avoid the call stack from being erased.
```csharp
  public void X()
  {
    try
    {
      ...
    }
    catch(Exception ex)
    {
      // DO 
      throw;

      //DO NOT
      throw ex;

      //DO NOT 
      throw new ABCException(ex);
    }
  }
```

### 5.2 Exception Handling

- **DO NOT** declare an empty catch block.
```csharp
  // DO NOT 
  try
  {
    ...
  }
  catch
  {
    // DO NOTHING
  }
```

- **DO** only use the finally block to release resources from a try statement.
```csharp
  // DO NOT 
  try
  {
    // Open database connection 
    dbConnection.Open();
  }
  catch
  {
    dbConnection.Close();
  }

  // DO 
  try
  {
    // Open database connection 
    dbConnection.Open();
  }
  catch
  {
    // Log exception
  }
  finally
  {
    // This code block is executed for both case of success or failure.
    // Release connection.
    dbConnection.Close();
  }
```
- **DO** catch and handle exceptions (like logging) as late in the call stack as possible, unless a lower level module can catch and do something meaningful about the exception.
- **DO** define a global exception handling policy to intercept all exceptions not caught by low-level modules.
- **NEVER** swallow exceptions. There should always be some indication that an exception occurred. Log trace of the exception is the bare minimum.
- **DO** use using block as a short-hand for the try-finally pattern with IDisposable object.
```csharp
  // DO 
  using (var dbConnection = new DBConnection())
  {
    dbConnection.Open();
    ...
    // Do not need to explicitly release resource.
  }
```

### 5.3 Exceptions and Performance

- **CONSIDER** the performance implications of throwing exceptions. Throw rates above 100 per second are likely to noticeably impact the performance of most applications.

To improve performance, it is possible to use either the Tester-Doer Pattern or the Try-Parse Pattern as described below:

#### 5.3.1 Tester-Doer Pattern

- **CONSIDER** the Tester-Doer Pattern for members that might throw exceptions in common scenarios to avoid performance problems related to exceptions.
```csharp
  ICollection<int> numbers = ...
  if( numbers != null && !numbers.IsReadOnly ) // Tester
  {
    numbers.Add(1); //Doer
  }
```

#### 5.3.2 Try-Parse Pattern

- **CONSIDER** the Try-Parse Pattern for members that might throw exceptions in common scenarios to avoid performance problems related to exceptions.
- **DO** use the prefix &quot;Try&quot; and Boolean return type for methods implementing this pattern.
- **DO** provide an exception-throwing member for each member using the Try-Parse Pattern.
```csharp
  public struct DateTime
  {
    public static DateTime Parse(string dateTime)
    {
      ...
    }
    public static bool TryParse(string dateTime, out DateTime result)
    {
      ...
    }
  }
```

## 6. Logging

- **DO** use Logger class for logging all error, warning, and traces.
- **DO** use the logger class extensively throughout the code to record errors, warning and even trace messages that can help you trouble shoot a problem.
- **DO** log the actual error with all possible information (e.g. parameters, SQL statement, file data). This will help a lot in diagnosing problems.
- **AVOID** log the critical information (e.g. credit card number, SSN).Consider encrypt critical information in log if the information logging is required.

## 7. Code Comments

- **DO** use // or /// but never /\* ..\*/ or &quot;flowerbox&quot; comment.
```csharp
  // ***********************************
  // This is a bad code comment format
  // ***********************************

  /* This is another bad code comment format */
  
  // This is good code comment format
  ///<summary>
  /// This is event better code comment format.
  ///<summary>
```

- **DO** add comments only when they make sense, don&#39;t add comments for the sake of having some comments. Bad and/or redundant comments are much worse than no comment at all.
```csharp
  // This is code presents the redundant code comment 
  // The window.Open() is to self-describe what it does.
  public void Execute()
  {
    var window = new Window();

    // Open window 
    window.Open();
  }
```

- **DO** write comments which describe what the code does and/or whyit does that, not how the code works.

- Only describe the how when there are inevitable complicated code like multithreading. On other occasions, if the code is too complicated to understand without lots of comment, chance is that the code is poorly written and should be refactored.

- **DO** use English for all code comments.
- **DO** add comments indicating what changes were made and optionally why, when checking in code into Source Control System (SCS).
- **DO** remove unused code from the source file instead of commenting it out.
- **DO** use // TODO: comment to indicate unfinished tasks.
- **DO** use // HACK: comment to indicate any shortcuts taken in the implementation which need to be fixed or improved later.
- **CONSIDER** usually walk throught //TODO comment to complete the unfinished tasks and remove it after completed.

## 8. String Manipulation

- **DO** use [StringBuilder](https://www.assembla.com/wiki/show/pe_gameworld/StringBuilder) whenever multiple concatenations are required.

```csharp
  // DO 
  var queryBuilder = new StringBuilder();
  queryBuilder.AppendLine("SELECT * FROM dbo.Employees");
  queryBuilder.AppendFormat("WHERE FirstName == N'{0}'", firstName);
  ...
  // DO NOT 
  var query = string.Empty;
  query = query + "SELECT * FROM dbo.Employees" + " " ;
  query = query + "WHERE FirstName = N'" + firstName + "'";
  ...

```

- **DO** use string formatting technique to parameterize strings.

```csharp
  // DO 
  var fullName = string.Format("{0} {1}",firstName,lastName);

  // DO NOT
  var fullName = firstName + " " + lastName;

```

- **DO** use string.Empty instead of &quot;&quot;.
```csharp
  // DO 
  var title = string.Empty;

  // DO NOT 
  var tile = "";
```

- **CONSIDER** use the &quot;@&quot; prefix for string literals instead of escaped strings.
```csharp
  // DO
  @"c:\temp"
  // DO NOT 
  "c:\\temp"
```

- **DO** use string. [IsNullOrEmpty](https://www.assembla.com/wiki/show/pe_gameworld/IsNullOrEmpty)()/string.IsNullOrWhitespaces() to detect null or empty string/whitespace.
- **DO** be aware of case sensitive in string comparison. This will ensure the string will match even if the string being compared has a different case.

```csharp 
  string a = ...
  string b = ...
  if( string.Equals(a, b, StringComparison.InvariantCultureIgnoreCase))
  {
    ...
  }
```
## 9. Unit Test

- Although not required, it is recommended that test code is written before production code (i.e. test-first approach). Whether test-first or test-last is applied, never delay the act of writing test code.
- Write one or more unit test cases to reproduce any defect found by QA team.
- Follow these principles when writing unit test code

- **Automatic:** The whole testing process must be automated. Do not rely on any manual process such as data population, environment configuration etc. Test code must do all those things.
- **Complete:** Test anything that can possibly break. When you are in doubt whether something can possibly go wrong or not, write a test.
- **Repeatable:** All test cases must be able to run and rerun repeatedly and produce the same result every time. If it doesn&#39;t, they are not reliable and must be fixed.
- **Independent:** Each test case must be configured and run in isolation from one another. Do not make any assumption that one test must be executed before another.
- **Production-like:** Test code must be treated like production code and subject to strict review. That means each and every coding convention in this document is very well applicable to test code.
- **Fast:** Test cases must run fast. If they do not, mock out the heavy dependencies (like database) to make them run fast.

## 10. Miscellaneous

- Use foreach-style loop instead of for loop when possible.

```csharp
  // DO
  foreach( var person in persons)
  {
    ...
  }

  // DO NOT  
  for (int index=0; index < persons.Count(); index++)
  {
    var person = person[0];
    ...
  }

```
- A switch statement must always contain a default branch which handles unexpected cases.

```csharp
  switch (accessMode)
  {
    case FileAccess.Read:
      ...
      break;
    case FileAccess.Write: 
      ...
      break;
    default:
      throw new NotSupportedException();
  }
```

- Never, ever, use a magic number/string.

```csharp
  // DO 
  const int MaxCount = 300;
  if(totalCount > MaxCount)
  {
    ...
  }

  // DO NOT 
  if(totalCount > 300)
  {
    ...
  }
```

- Use prescribed tools to add loggingcode throughout the application to facilitate debugging.
- Consider using AOP to inject logging code when applicable.
- Fix all issuesreported by static analysis tool(s). An issue can be waived with the authority of Team Lead or Technical Lead.
- Always check Event &amp; Delegate instances for null before invoking.

 ```csharp
    public class Window
    {
      public EventHandler Opening { get;set; }
      public void DoSomething()
      {
        ...
        if(Opening != null)
        {
          Opening(this, new EventArgs());
        }
      }
    }
 ```

- Do not omit access modifiers. Explicitly declare all identifiers with the appropriate access modifier instead of allowing the default.

```csharp
  // DO NOT
  class Window
  {
    string title;
    int width;
    int height;
  } 
  // DO 
  internal class Window
  {
    private string title;
    private int width;
    private int height;
  }
```

- Do not hardcode text in UI. Use resource files.
- Never hardcode a path or drive name in code. Get the application path programmatically and use relative path.
- Never assume that your code will run from drive &quot;C:&quot;. You may never know, some users may run it from network or from a &quot;Z:&quot;.
- In the application start up, do some kind of &quot;self-check&quot; and ensure all required files and dependencies are available in the expected locations. Check for database connection in start-up, if required. Give a friendly message to the user in case of any problems.
- If a wrong value found in the configuration file, application should throw an error or give a message and also should tell the user what are the correct values.
- Avoid having very large files. If a single file has more than 1000 lines of code, it is a good candidate for refactoring. Split them logically into two or more classes.

## 11. ASP.NET Web Form controls naming

|  Control | Prefix | Example |
| --- | --- | --- |
| Label | lbl | lblSurname |
| TextBox | txt | txtSurname |
| DataGrid | dg | dgResults |
| Button | btn | btnSave |
| ImageButton | ibtn | ibtnSave |
| Hyperlink | lnk | lnkHomePage |
| DropDownList | ddl | ddlCompany |
| ListBox | lst | lstCompany |
| DataList | dlst | dlstAddress |
| Repeater | rep | repSection |
| Checkbox | chk | chkMailList |
| CheckBoxList | chk | chkAddress |
| RadioButton | rdo | rdoSex |
| RadioButtonList | rdo | rdoAgeGroup |
| Image | img | imgLogo |
| Panel | pan | panSection |
| PlaceHolder | plh | plhHeader |
| Calender | cal | calMyDate |
| Adrotator | adr | adrBanner |
| Table | tbl | tblResults |
| Validators | val | valCreditCardNumber |
| ValidationSummary | vals | valsErrors |

## 12. Managed Threading Best Practices

Multithreading requires careful programming. For most tasks, you can reduce complexity by queuing requests for execution by thread pool threads. This topic addresses more difficult situations, such as coordinating the work of multiple threads, or handling threads that block.

### 12.1 Understand Deadlocks and Race Conditions

Multithreading solves problems with throughput and responsiveness, but in doing so it introduces new problems: deadlocks and race conditions.

#### 12.1.1 Deadlocks

A deadlock occurs when each of two threads tries to lock a resource the other has already locked. Neither thread can make any further progress.

Many methods of the managed threading classes provide time-outs to help you detect deadlocks. For example, the following code attempts to acquire a lock on the current instance. If the lock is not obtained in 300 milliseconds, Monitor.TryEnter returns false.

```csharp
  if(Monitor.TryEnter(lockObject, 30))
  {
    try
    {
      // Place code protected by the monitor here.
    }
    finally
    {
      Monitor.Exit(this);
    }
  }
```

#### 12.1.2 Race Conditions

A race condition is a bug that occurs when the outcome of a program depends on which of two or more threads reaches a particular block of code first. Running the program many times produces different results, and the result of any given run cannot be predicted.

A simple example of a race condition is incrementing a field. Suppose a class has a private static field (Shared in Visual Basic) that is incremented every time an instance of the class is created, using code such as objCt++; (C#) or objCt += 1 (Visual Basic). This operation requires loading the value from objCt into a register, incrementing the value, and storing it in objCt.

In a multithreaded application, a thread that has loaded and incremented the value might be preempted by another thread which performs all three steps; when the first thread resumes execution and stores its value, it overwrites objCt without taking into account the fact that the value has changed in the interim.

This particular race condition is easily avoided by using methods of the **Interlocked** class, such as **Interlocked.Increment**.

Race conditions can also occur when you synchronize the activities of multiple threads. Whenever you write a line of code, you must consider what might happen if a thread were preempted before executing the line (or before any of the individual machine instructions that make up the line), and another thread overtook it.

### 12.2 General Recommendations

Since the .NET Framework 4, the Task Parallel Library (TPL) and PLINQ provide APIs that reduce some of the complexity and risks of multi-threaded programming. Consider to use TPL and PLINQ instead.

- **DON&#39;T** use Thread.Abort to terminate other threads. Calling Abort on another thread is akin to throwing an exception on that thread, without knowing what point that thread has reached in its processing.
- **DON&#39;T** use Thread.Suspend and Thread.Resume to synchronize the activities of multiple threads. Do use Mutex, ManualResetEvent, AutoResetEvent, and Monitor.
- **DON&#39;T** control the execution of worker threads from your main program (using events, for example). Instead, design your program so that worker threads are responsible for waiting until work is available, executing it, and notifying other parts of your program when finished. If your worker threads do not block, consider using thread pool threads.
- **DON&#39;T** use types as lock objects. That is, avoid code such as lock(typeof(X)) in C# or SyncLock(GetType(X)) in Visual Basic, or the use of Monitor.Enter with Type objects. For a given type, there is only one instance of System.Type per application domain. If the type you take a lock on is public, code other than your own can take locks on it, leading to deadlocks.
- **DO** use in **CAUTION** when locking on instances, for example lock(this) in C# or SyncLock(Me) in Visual Basic. If other code in your application, external to the type, takes a lock on the object, deadlocks could occur.
- **DO** ensure that a thread that has entered a monitor always leaves that monitor, even if an exception occurs while the thread is in the monitor. The C# lock statement and the Visual Basic SyncLock statement provide this behavior automatically, employing a finally block to ensure that Monitor.Exit is called. If you cannot ensure that Exit will be called, consider changing your design to use Mutex. A mutex is automatically released when the thread that currently owns it terminates.
- **DO** use multiple threads for tasks that require different resources, and avoid assigning multiple threads to a single resource. For example, any task involving I/O benefits from having its own thread, because that thread will block during I/O operations and thus allow other threads to execute. User input is another resource that benefits from a dedicated thread. On a single-processor computer, a task that involves intensive computation coexists with user input and with tasks that involve I/O, but multiple computation-intensive tasks contend with each other.
- **CONSIDER** using methods of the Interlocked class for simple state changes, instead of using the lock statement (SyncLock in Visual Basic). The lock statement is a good general-purpose tool, but the Interlocked class provides better performance for updates that must be atomic. Internally, it executes a single lock prefix if there is no contention. In code reviews, watch for code like that shown in the following examples.

**Bad Coding Practice**

 ```csharp
    lock(lockObject)
    {
      myField++;
    }

    Or 

    if( x == null)
    {
      lock(lockObject)
      {
        if(x == null)
        {
          x= y;
        }
      }
    }
 ```


**Good Coding Practice**

 ```csharp
    System.Threading.Interlocked.Increment(myField);

    Or

    System.Threading.Interlocked.CompareExchange(ref x, y, null);
 ```

## 13. SharePoint Best Practices
### 13.1 Best Practices with Event Receivers

- **DON&#39;T** instantiate a SPWeb, SPSite, SPList, or SPListItem object within an event receiver. Event receivers that instantiate these objects instead of using the instances passed via the event properties can cause the following issues:

- Significant additional roundtrips to the database
- Calls to the Update method on these instances can cause subsequent Update calls in other registered event receivers to fail.

**Bad Coding Practice**

Instantiating a SPSite object inside an event receiver

 ```csharp
    public override void ItemDeleting(SPIItemEventProperties properties)
    {
      using (SPSite site  = new SPSite(properties.WebUrl))
      {
        using (SPWeb web = site.OpenWeb())
        {
          SPList list = web..Lists[properties.ListId];
          SPListItem item = list.GetItemByUniqueId(properties.ListItemId);
          // Operate on an item

        }
      }
    }
 ```

**Good Coding Practice**

Using SPItemEventProperties

 ```csharp
    // Retrieve SPWeb and SPListItem from SPItemEventProperties instead of 
    // from a new instance of SPSite
    SPWeb web = properties.OpenWeb();
    // Operate on the SPWeb object
    SPListItem item = properties.ListItems;
    // Operate on an item

 ```

### 13.2 Caching SharePoint Objects That Are Not Thread-Safe

- **DON&#39;T** cache SPListItemCollection object, cache its DataTable instead and remember to apply a lock. For example:

 ```csharp
    private static object _lock = new Object();
    public void CachData()
    {
      DataTable oDataTable;
      SPListItemCollection oListItems;
      lock(_lock)
      {
        oDataTable = (DataTable)Cache["ListItemCacheName"];
        if(oDataTable == null)
        {
          oListItems = DoQueryToReturnItems();
          oDataTable = oListItems.GetDataTable();
          Cache.Add("ListItemCacheName", oDataTable, ...);
        }
      }
    }
 ```

### 13.3 Working with Folders and Lists

- **DON&#39;T** use SPList.Items. SPList.Items selects all items from all subfolders, including all fields in the list. Use the following alternatives for each use case.

- Use SP.GetItems(SPQuery query) when retrieving all items in a list. For example:

 ```csharp
    SPQuery query = new SPQuery();
    SPListItemCollection spListItems;

    string lastItemIdOnPage = null; // Page position.
    int itemCount = 2000

    while (itemCount == 2000)
    {
      // Include only the fields you will use.
      query.ViewFields = "(FieldRef Name=\”ID\"/><FieldRef Name=\”ContentTypeId\”/>";
      query.RowLimit = 2000; // Only select the top 2000.
      // Include items in subfolder (if necessary).
      query.ViewAttributes = "Scope=\"Recursive\"";
      StringBuilder sb = new StringBuilder();
      // To make it order by ID and stop scanning the table, specify the OrderBy override attribute.
      sb.Append("<OrderBy Override=\"TRUE\”><FieldRef Name=\"ID\"/></OrderBy>");
      //.. Append more text as necessary ..
      query.Query = sb.ToString();
      // Get 2,000 more items.

      SPListItemCollectionPosition pos = new SPListItemCollectionPosition(lastItemIdOnPage);
      query.ListItemCollectionPosition = pos; //page info

      spListItems = spList.GetItems(query);

      lastItemIdOnPage = spListItems.ListItemCollectionPosition.PagingInfo;

      // Code to enumerate the spListItems.

      // If itemCount (2000, we finish the enumeration.

      itemCount = spListItems.Count;
    }

 ```

- Use SPList.GetItemById(int id, string field1, params string[] fields) when getting items by identifier.

- **DON&#39;T** enumerate entire SPList.Items collections or SPFolder.Files collection.

|Poor Performing Methods and Properties | Better Performing Alternatives|
|---|---|
|SPList.Items.Count | SPList.ItemCount|
|SPList.Items.XmlDataSchema | Create an SPQuery object to retrieve only the items you want.|
|SPList.Items.NumberOfFields | Create an SPQuery object (specifying the ViewFields) to retrieve only the items you want.|
|SPList.Items[System.Guid] | SPList.GetItemByUniqueId(System.Guid)|
|SPList.Items[System.Int32] | SPList.GetItemById(System.Int32)|
|SPList.Items.GetItemById(System.Int32) | SPList.GetItemById(System.Int32)|
|SPList.Items.ReorderItems(System.Boolean[],System.Int32[],System.Int32) | Perform a paged query by using SPQuery and reorder the items within each page.|
|SPFolder.Files.Count | SPFolder.ItemCount|


### 13.4 Deleting Multiple Versions of a List Item

- **DO** use the DeleteByID method of SPFileVersionCollection; don&#39;t use the Delete method of SPListItemVersion. For example:

```csharp
  SPSite site = new SPSite("site url");
  SPWeb web = site.OpenWeb();
  SPList list = web.Lists["custom list name"];
  SPFile file 1ist.RootFolder.Files[0];
  SPFileVersionCollection collection = file.Versions;
  ArrayList idList = new ArrayList();
  foreach (SPFileVersion ver in collection)
  {
    idList.Add(ver.ID);
  }
  foreach (int verID in idList)
  {
    try
    {
      collection.DeleteByID(verID);
    }
    catch (Exception ex)
    {
      MessageBox.Show(ex.Message);
    }
  }

```

### 13.5 Using SPQuery Object

- **DON&#39;T** use an unbounded SPQuery object. A SPQuery object without a value for RowLimit will perform poorly and fail on large list. Specify a RowLimit between 1 and 2000 and, if necessary, page through the list.
- **DO** use indexed fields. If you query on a field that is not indexed, the query will be blocked whenever it would result in a scan of more items than the query threshold (as soon as there are more items in the list than are specified in the query threshold).
- **DO** use SPWeb.GetListItem(string url, string field1, params string[] fields) if you know the URL of your list item and want to query by FileRef.

### 13.6 Using Disposable Windows SharePoint Services Objects

- **DO** dispose of new created SPSite object.

**Good Coding Practice #1**

 ```csharp
    void CreatingSPSiteExplicitDisposeNoLeak()
    {
      SPSite siteCollection = null;
      try
      {
        siteCollection = new SPSite("http://moss");
      }
      finally
      {
        if(siteCollection != null)
        {
          siteCollection.Dispose();
        }
      }
    }
 ```

**Good Coding Practice #2**

 ```csharp
    CreatingSPSiteWithAutomaticDisposeNoLeak()
    {
      using(SPSite siteCollection = new SPSite("http://moss"))
    } // SPSite object siteCollection.Dispose() is called automatically 

 ```

- **DO** dispose of items created by SharePoint methods (such as SPSite.OpenWeb or SPSite.SelfServiceCreateSite) that return other SPWeb/SPSite objects.

**Bad Coding Practice**

 ```csharp
    void OpenWebLeak()
    {
      using( SPWeb web = new SPSite(SPContext.Current.Web.Url).OpenWeb())
      {
        using(SPWeb web = siteCollection )
        {
          // SPSite leaked !
        } // SPWeb object web.Dispose() automatically called
      }
    }
 ```

**Good Coding Practice**

 ```csharp
    void OpenWebNoLeak()
    {
      using(SPSite siteCollection = new SPSite("http://moss"))
      {
        using(SPWeb web = siteCollection.OpenWeb())
        {

        } // SPWeb object web.Dispose() automatically called.
      } // SPSite object siteCollection.Dispose() automatically called.
    }
 ```

- **DON&#39;T** share any SPRequest object and by extension any object that contains a reference to a SPRequest object (such as SPWeb or SPSite) across threads.
- **DO** dispose of any SPSite object returned from the Add method or index operator of SPSiteCollection.

**Bad Coding Practice #1**

 ```csharp
    void SPSiteCollectionAddLeak()
    {
      SPWebApplication webApp = new SPSite("http://moss").WebApplication;
      SPSiteCollection siteCollections = webApp.Sites;
      SPSite siteCollection = siteCollections.Add("sites/myNewSiteCollection", "DOMAIN\\User",
      "roger.lamb@1itwareinc.com");
      // SPSite siteCollection leak.
    }

 ```

**Bad Coding Practice #2**

 ```csharp
    void SPSiteCollectionIndexerLeak()
    {
      using (SPSite siteCollectionOuter = new SPSite("http://moss"))
      {
        SPWebApplication webApp = siteCollectionOuter.webApplication;
        SPSiteCollection siteCollections = webApp.Sites;
        SPSite siteCollectionInner = sitec 1ections[0];
        // SPSite siteCollectionInner leak.
      } // SPSite object siteCollectionOuter.Dispose() automatically called.
    }

 ```

**Bad Coding Practice #3**

 ```csharp
    void SPSiteCollectionForEachLeak()
    {
      using (SPSite siteCollectionOuter = new SPSite("http://moss"))
      {
        SPWebApplication webApp = siteCollectionOuter.webApplication;
        SPSiteCollection siteCollections = webApp.Sites;
        
        foreach (SPSite siteCollectionInner in siteCollections)
        {
          // SPSite siteCollectionInner leak.
        }
      } // SPSite object siteCollectionOuter.Dispose() automatically called.

    }
 ```


**Good Coding Practice #1**

 ```csharp 
    void SPSiteCollectionAddNoLeak()
    {
      SPWebApplication webApp = new SPSite("http://moss").WebApplication;
      SPSiteCollection siteCollections = webApp.Sites;

      using (SPSite siteCollection = siteCollections.Add("sites/myNewSiteCollection", "DOMAIN\\User",
      "roger.1amb@1itwareinc.com"))
      {

      } // SPSite object siteCollection.Dispose() automatically called.
    }

 ```

**Good Coding Practice #2**

```csharp
    void SPSiteCollectionIndexerNoLeak()
    {
      using (SPSite siteCollectionOuter = new SPSite("http://moss"))
      {
        SPSite siteCollectionInner = null;
        try
        {
          SPWebApplication webApp = siteCollectionOuter.WebApplication;
          SPSiteCollection siteCollections = webApp.Sites;
          siteCollectionInner = siteCollections[0];
        }
        finally
        {
          if (siteCollectionInner != null)
            siteCollectionInner.Dispose();
        }

      } // SPSite object siteCollectionOuter.Dispose() automatically called.
    }

```

**Good Coding Practice #3**

 ```csharp
    void SPSiteCollectionForEachNoLeak()
    {
      using (SPSite siteCollectionOuter = new SPSite("http://moss"))
      {
        SPWebApplication webApp = siteCollectionOuter.WebApplication;
        SPSiteCollection siteCollections = webApp.Sites;
        foreach (SPSite siteCollectionInner in siteCollections)
        {
          try
          {
            // ...
          }
          finally
          {
            if(siteCollectionInner != null)
               siteCollectionInner.Dispose();
          }
        }
      } // SPSite object siteCollectionOuter.Dispose() automatically called.
    }
 ```

- **DO** dispose of any SPWeb object returned from Add method or index operator of SPWebCollection.

**Bad Coding Practice #1**

 ```csharp 
    void AllWebsAddLeak()
    {
      using (SPSite siteCollection = new SPSite("http://moss"))
      {
        SPWeb web = siteCollection.Allﬂebs.Add("site-relative URL");
        // SPweb object leaked.
      } // SPSite object siteCollection.Dispose() automatically called.
    }

 ```

**Bad Coding Practice #2**

 ```csharp
    void AllWebsForEachLeak()
    { 
      using (SPSite siteCollection = new SPSite("http://moss"))
      { 
        using (SPWeb outerweb = siteCollection.Openweb())
        { 
          foreach (SPWeb innerweb in siteCollection.Allwebs)
          { 
            // Explicitly dispose here to avoid out of memory leaks with large number of SPweb objects.
          } 
        } // SPweb object outerweb.Dispose() automatically called.
      } // SPSite object siteCollection.Dispose() automatically called.
    }

 ```

**Good Coding Practice #1**

 ```csharp
    void AllWebsAddNoLeak()
    {
      using (SPSite siteCollection = new SPSite("http://moss"))
      {
        using (SPWeb web = siteCollection.Allﬂebs.Add("site-relative URL"))
        {

        } // SPweb object web.Dispose() automatically called.

      } // SPSite object siteCollection.Dispose() automatically called.
    }

 ```

**Good Coding Practice #2**

 ```csharp
    void AllWebsForEachNoLeakOrMemoryOOM()
    {
      using (SPSite siteCollection = new SPSite("http://moss"))
      {
        using (SPWeb outerweb = siteCollection.Openweb())
        {
          foreach (SPWeb innerWeb in siteCollection.Allwebs)
          {
            try
            {
              // ...
            }
            finally
            {
              if(innerweb != null)
                innerWeb.Dispose();
            }
          }

        } // SPweb object outerﬂeb.Dispose() automatically called.
      } // SPSite object siteCollection.Dispose() automatically called.
    }

 ```

- **DO** dispose of SPWeb object of Area.Web.

**Bad Coding Practice**

 ```csharp
    void AreaWebLeak()
    {
      // AreaManager and Area are obsolete in SharePoint Server, but this
      // should still be noted.
      Area area = AreaManager.GetArea(PortalContext.Current, new Guid("{GUID}"));
      string str = area.Web.Title;
      // SPWeb area.Web leak.
    }

 ```

**Good Coding Practice**

 ```csharp
    public void AreawebNoLeak()
    {
      // AreaManager and Area are obsolete in MOSS but this should still be noted
      Area area = AreaManager.GetArea(PortalContext.Current, new Guid("{GUID}"));
      using (SPWeb areaweb = area.Web)
      {
        string str = areaweb.Title;
      }
    }

 ```

- **DO** dispose of SPWeb object whenever retrieving a SPLimitedWebPartManager object.

**Bad Coding Practice**

 ```csharp
    void SPLimitedWebPartManagerLeak()
    {
      using (SPSite siteCollection = new SPSite("http://moss"))
      {
        using (SPWeb web = siteCollection.OpenWeb())
        {
          SPFile page = web.GetFile("Source_Folder_Name/Source_Page");
          SPLimitedWebPartManager webPartManager =
          page.GetLimitedﬂebPartManager(PersonalizationScope.Shared);
          // SPweb object webPartManager.Web leaked.
        } // SPweb object web.Dispose() automatically called.
      } // SPSite object siteCollection.Dispose() automatically called.
    }

 ```

**Good Coding Practice**

 ```csharp
    void SPLimitedWebPartManagerLeak()
    {
      using (SPSite siteCollection = new SPSite("http://moss"))
      {
        using (SPWeb web = siteCollection.OpenWeb())
        {
          SPFile page = web.GetFi1e("Source_Folder_Name/Source_Page");
          SPLimitedWebPartManager webPartManager = page.GetLimitedWebPartManager(PersonalizationScope.Shared);
          webPartManager.Web.Dispose();
        } // SPweb object web.Dispose() automatically called.
      } // SPSite object siteCollection.Dispose() automatically called.
    }

 ```

- **DON&#39;T** dispose of SPWeb or SPSite object that returned from SPSite.RootWeb, SPControl.GetContextSite and SPControl.GetContextWeb method. For example

**Good Coding Practice #1**

 ```csharp
    public void RootWebBestPractice()
    {
      // New SPSite.
      using (SPSite siteCollection = new SPSite("http://moss"))
      {
          SPweb rootweb1 = siteCollection.Rootweb;
          // No explicit rootweb1 dispose required.
      } // siteCollection automatically disposed by implementing using().
      // rootweb1 will be Disposed by SPSite.

      // SPContext and SPControl
      SPWeb rootweb2 = SPContext.Current.Site.RootWeb;
      // Also would apply to SPControl.GetContextSite(Context);
      // No explicit rootwebz dispose required because it's obtained from SPContext.Current.Site.
    }

 ```

**Good Coding Practice #2**

 ```csharp
    void SPControlBestPractice()
    {
      SPSite siteCollection = SPControl.GetContextSite(Context);
      SPWeb web = SPControl.GetContextWeb(Context);
      // Do NOT call Dispose().
    }
 ```
