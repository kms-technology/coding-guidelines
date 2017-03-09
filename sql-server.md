# KMS SQL Server Coding Standards

- [1. Purpose](#1-purpose)
- [2. Naming Convention](#2-naming-convention)
    - [2.1 Summary of Naming Convention](#21-summary-of-naming-convention)
    - [2.2 Tables](#22-tables)
    - [2.3 Columns (incl. PRIMARY, FOREIGN, AND COMPOSITE KEYS)](#23-columns-incl-primary-foreign-and-composite-keys)
    - [2.4 Indexes](#24-indexes)
    - [2.5 Constraints](#25-constraints)
    - [2.6 Views](#26-views)
    - [2.7 Stored Procedures](#27-stored-procedures)
    - [2.8 Functions](#28-functions)
    - [2.9 Triggers](#29-triggers)
    - [2.10 Synonyms](#210-synonyms)
    - [2.11 User-Defined Data Types](#211-user-defined-data-types)
    - [2.12 Variables](#212-variables)
    - [2.13 Use Modular Prefixes](#213-use-modular-prefixes)
- [3. Coding Convention](#3-coding-convention)
    - [3.1 SQL Statements – SELECT](#31-sql-statements--select)
    - [3.2 SQL Statements – INSERT](#32-sql-statements--insert)
    - [3.3 SQL Statements – Formatting](#33-sql-statements--formatting)
    - [3.4 Setting the NOCOUNT Option](#34-setting-the-nocount-option)
    - [3.5 Code Commenting](#35-code-commenting)
    - [3.6 Use Code Headers](#36-use-code-headers)
    - [3.7 Unicode vs. Non-Unicode Data Types](#37-unicode-vs-non-unicode-data-types)
    - [3.8 CHAR vs. VARCHAR Data Types](#38-char-vs-varchar-data-types)
    - [3.9 Very Large Strings](#39-very-large-strings)
    - [3.10 Common Table Expression (CTE) over Sub Query](#310-common-table-expression-cte-over-sub-query)
    - [3.11 Data Access and Transactions](#311-data-access-and-transactions)
    - [3.12 Error Handling](#312-error-handling)
    - [3.13 Foreign Key and Check Constraints](#313-foreign-key-and-check-constraints)
    - [3.14 Cursor Usage](#314-cursor-usage)
    - [3.15 Temporary Tables and Table Variables](#315-temporary-tables-and-table-variables)
    - [3.16 Parameter Sniffing – Be Warned](#316-parameter-sniffing--be-warned)
- [4. Database Design – Best Practices](#4-database-design--best-practices)

## 1. Purpose

This document describes a collection of standards, conventions, and guidelines for designing and writing solid Database code. They are compiled from KMS developers own experiences and sound, proven software engineering principles that lead to code that is easy to understand, to maintain, and to enhance.

Experience shows that by taking the time to write high-quality code right from the start you will have a much easier time modifying it during the development process. Finally, following a common set of coding standards leads to greater consistency, making teams of developers significantly more productive. For the conventions to work, **everyone** writing software must conform to the code conventions.

## 2. Naming Convention

### 2.1 Summary of Naming Convention
			
<table>
<tr>
    <th>Object</th>
    <th>Compliant Names</th>
    <th>Incompliant Names</th>
    <th>Major Rules</th>
</tr>
<tr>
    <td>Table</td>
    <td><pre>
Account
Employee
Product
Order
ProductOrder
</pre></td>
    <td>
    <pre>
Accounts
EMPLOYEE
tblProduct
ORD
Product_Order

</pre>
</td>
    <td>
    <pre>
- Singular name
- Pascal Case
- No prefixes
- Avoid abbreviations
- Avoid underscore, special character
</pre>
</td>
</tr>
<tr>
    <td>Column</td>
    <td></td>
    <td>
    <pre>
ID
EmployeeName
Address (foreign key)
tblValidate
intRunning_Hour
</pre>
</td>
    <td>
    <pre>
- Use Pascal Case
- Don’t repeat table name in column except primary key column
- Don’t use prefixes
- Avoid underscore or special character
</pre>
</td>
</tr>
<tr>
    <td>Index</td>
    <td></td>
    <td>
    <pre>
UIX_EmployeeZone
</pre>
</td>
    <td>
    <pre>
- Keep SQL Server default names unless specific purpose
- Use this pattern: {U/N}IX_{Table Name}{Special Purpose}
</pre>
</td>
</tr>
<tr>
    <td>Constraint</td>
    <td></td>
    <td>
    <pre>
PkProduct_Id
PkOrder_ProductId
</pre>
</td>
    <td>
    <pre>
- Use this pattern: {constraint type}{table name}_{field name}
</pre>
</td>
</tr>
<tr>
    <td>View</td>
    <td><pre>
vwEmployeeForReport
</pre></td>
    <td>
    
</td>
    <td>
    <pre>
- Use prefix “vw”
- Use Pascal Case
- Use the same convention as table name
</pre>
</td>
</tr>
<tr>
    <td>Stored Procedure</td>
    <td><pre>
spEmployeeUpdate
spProductInsert
spOrderInsertUpdate
spEmployeeGet
</pre></td>
    <td>
    
</td>
    <td>
    <pre>
- Use prefix “sp”
- Use action as suffixes
- Use Pascal Case

</pre>
</td>
</tr>
<tr>
    <td>Function</td>
    <td><pre>
fnConvertMileageToRuby
fnFormatZip

</pre></td>
    <td>
    
</td>
    <td>
    <pre>
- Use prefix “fn”
- Start with a verb
- Use Pascal Case
</pre>
</td>
</tr>
<tr>
    <td>Trigger</td>
    <td><pre>
trOrderValiateEmailInsert
trProductParseBarcodeUpdate
trAccountRecycleDelete

</pre></td>
    <td>
    
</td>
    <td>
    <pre>
- Use prefix “tr”
- Use “Insert”, “Update” or “Delete” as suffixes
</pre>
</td>
</tr>
<tr>
    <td>Variable</td>
    <td><pre>
@firstName
@updatedDate

</pre></td>
    <td>
    <pre>
@FirstName
@dtUpdatedDate

</pre>
</td>
    <td>
    <pre>
- Use camelCase
- Don’t use prefix
- Use single @
- Don’t use special character or underscore
- Try to be meaningful
</pre>
</td>
</tr>
</table>

### 2.2 Tables

When naming your database tables, give consideration to other steps in the development process. Keep in mind you will most likely have to utilize the names you give your tables several times as part of other objects, for example, procedures, triggers or views may all contain references to the table name. You want to keep the name as simple and short as possible. Some systems enforce character limits on object names also.

Singular Names:

Table names should be singular, for example, &quot;Customer&quot; instead of &quot;Customers&quot;.Prefixes:

Don&#39;t use prefixes unless they are deemed necessary to help you organize your tables into related groups or distinguish them from other unrelated tables. Do not give your table names prefixes like &quot;tb&quot; or &quot;TBL\_&quot; as these are redundant and wordy.

In some cases, your tables might be sharing a schema/database with other tables that are not related in any way. In this case, it is sometimes a good idea to prefix your table names with some characters that group your tables together. For example, for a healthcare application you might give your tables an &quot;Hc&quot; prefix so that all of the tables for that application would appear in alphabetized lists together. Note that even for the prefix, use PascalCase. Do not use underscores in your prefixes. The last kind of prefix that is acceptable is one that allows you to group logical units of tables. A plausible example could entail a large application (30 to 40+ tables) that handled both Payroll and Benefits data. You could prefix the tables dealing with payroll with a &quot;Pay&quot; or &quot;Prl&quot; prefix and give the tables dealing with benefits data a &quot;Ben&quot; or &quot;Bfts&quot; prefix. The goal of both this prefix and the aforementioned shared schema/database prefix is to allow you to group specific tables together alphabetically in lists and distinguish them from unrelated tables. Lastly, if a prefix is used for this purpose, the shared schema/database prefix is a higher grouping level and comes first in the name, for example, &quot;HcPayClients&quot; not &quot;PayHcClients&quot;.

Notation:

For all parts of the table name, including prefixes (if applicable), use Pascal Case. Using this notation will distinguish your table names from SQL keywords. For example, &quot;SELECT CustomerId, CustomerName FROM MyAppGroupTable WHERE CustomerName = &#39;%S&#39;&quot; shows the notation for the table name distinguishing it from the SQL keywords used in the query. PascalCase also reduces the need for underscores to visually separate words in names.

Special Characters:

For table names, underscores should not be used. Using PascalCase for your table name allows for the upper-case letter to denote the first letter of a new word or name. Thus there is no need to do so with an underscore character.

Do not use numbers in your table names either. Do not use spaces in your table names either. While most database systems can handle names that include spaces, systems such as SQL Server require you to add brackets around the name when referencing it (like [table name] for example) which goes against the rule of keeping things as short and simple as possible.

Abbreviations:

Avoid using abbreviations if possible. Use &quot;Account&quot; instead of &quot;Acct&quot; and &quot;Hour&quot; instead of &quot;Hr&quot;. Not everyone will always agree with you on what your abbreviations stand for - and - this makes it simple to read and understand for both developers and non-developers. Avoid using acronyms as well. If exceptions to this rule are deemed necessary, ensure that the same convention is followed by all project members.

Junction a.k.a Intersection Tables:

Junction tables, which handle many to many relationships, should be named by concatenating the names of the tables that have a one to many relationships with the junction table. For example, you might have &quot;Doctor&quot; and &quot;Patient&quot; tables. Since doctors can have many patients and patients can have many doctors (specialists) you need a table to hold the data for those relationships in a junction table. This table should be named DoctorPatient&quot;. Since this convention can result in lengthy table names, abbreviations sometimes may be used at your discretion.

### 2.3 Columns (incl. PRIMARY, FOREIGN, AND COMPOSITE KEYS)

When naming your columns, keep in mind that they are members of the table, so they do not need the any mention of the table name in the name. When writing a query against the table, you should be prefixing the field name with the table name or an alias anyway. Just like with naming tables, avoid using abbreviations, acronyms or special characters. All column names should use PascalCase to distinguish them from SQL keywords.

Identity Primary Key Fields:

For fields that are the primary key for a table and uniquely identify each record in the table, the name should simply be [tableName] + &quot;Id&quot;(e.g.in a Customer table, the primary key field would be &quot;CustomerId&quot;. A prefix is added mainly because &quot;Id&quot; is a keyword in SQL Server and we would have to wrap it in brackets when referencing it in queries otherwise. Though CustomerId conveys no more information about the field than Customer.Id and is a far wordier implementation, it is still preferable to having to type brackets around &quot;Id&quot;.

Foreign Key Fields:

Foreign key fields should have the exact same name as they do in the parent table where the field is the primary. For example, in the Customers table the primary key field might be &quot;CustomerId&quot;. In an Orders table where the customer id is kept, it would also be &quot;CustomerId&quot;. There is one exception to this rule, which is when you have more than one foreign key field per table referencing the same primary key field in another table. In this situation, it might be helpful to add a descriptor before the field name.

An example of this is if you had an Address table. You might have another table with foreign key fields like HomeAddressId, WorkAddressId, MailingAddressId, or ShippingAddressId.

Composite Keys:

If you have tables with composite keys (more than one field makes up the unique value), it&#39;s recommended that a seeded identity column is created to use as the primary key for the table.

Prefixes:

Do not prefix your fields with &quot;fld\_&quot; or &quot;Col\_&quot; as it should be obvious in SQL statements. Do not use a data type prefix for the field either, for example, &quot;IntCustomerId&quot; for a numeric type or &quot;VcName&quot; for a varchar type. These &quot;clog up&quot; our naming and add little value; most integer fields can be easily identified as such and character fields would have to be checked for length in the Object Browser anyway.

Data Type-Specific Naming:

Bit fields should be given affirmative boolean names like &quot;IsDeleted&quot;, &quot;HasPermission&quot;, or &quot;IsValid&quot; so that the meaning of the data in the field is not ambiguous. If the field holds date and/or time information, the word &quot;Date&quot; or &quot;Time&quot; should appear somewhere in the field name. It is sometimes appropriate to add the unit of time to the field name also, especially if the field holds data like whole numbers (&quot;3&quot; or &quot;20&quot;). Those fields should be named like &quot;RuntimeHours&quot; or &quot;ScheduledMinutes&quot;.

Field Name Length:

Field names should be no longer than 50 characters and all should strive for less lengthy names if possible. You should, however, not sacrifice readability for brevity and avoid using abbreviations unless it is absolutely necessary.

Special Characters:

Field names should contain only letters and numbers. No special characters, underscores or spaces should be used.

### 2.4 Indexes

Indexes will remain named as the SQL Server default, unless the index created is for a special purpose. All primary key fields and foreign key fields will be indexed and named in the SQL Server default. Any other index will be given a name indicating it&#39;s purpose.

Naming Convention:

Indexes will remain named as the SQL Server default, unless the index created is for a special purpose, in which case the naming convention for special-purpose indexes follows this structure:

 {U/N}IX\_{TableName}{SpecialPurpose}

where &quot;U/N&quot; is for unique or non-unique and &quot;IX\_&quot; matches the default prefix that SQL Server assigns indexes.

Prefixes and Suffixes:

Avoid putting any prefix or suffix unless it&#39;s for special purpose in certain cases.

### 2.5 Constraints

Constraints are at the field/column level so the name of the field the constraint is on should be used in the name. The type of constraint (Check, Referential Integrity a.k.a Foreign Key, Primary Key, or Unique) should be noted also. Constraints are also unique to a particular table and field combination, so you should include the table name also to ensure unique constraint names across your set of database tables.

Naming Convention:

The naming convention syntax for constraints looks like this:

 {constraint type}{table name}\_{field name}

 Examples:

1. PkProduct\_Id - primary key constraint on the Id field of the Products table

2. FkOrder\_ProductId - foreign key constraint on the ProductId field in the Orders table

3. CkCustomer\_AccountRepId - check constraint on the AccountRepId field in the Customers table

The reason underscores are used here with Pascal Case notation is so that the table name and field name are clearly separated. Without the underscore, it would become easy to get confused about where the table name stops and the field name starts.

Prefixes:

A two letter prefix gets applied to the constraint name depending on the type

Primary Key: Pk

Foreign Key: Fk

Check: Ck

Unique: Un

### 2.6 Views

Views follow many of the same rules that apply to naming tables. There are only two differences that were mentioned below. If your view combines entities with a join condition or where clause, be sure to combine the names of the entities that are joined in the name of your view.

Prefixes:

While it is pointless to prefix tables, it can be helpful for views. Prefixing your views with &quot;vw&quot; is a helpful reminder that you&#39;re dealing with a view, and not a table.

View Types:

Some views are simply tabular representations of one or more tables with a filter applied or because of security procedures (users given permissions on views instead of the underlying table(s) in some cases). Some views are used to generate report data with more specific values in the WHERE clause. Naming your views should be different depending on the type or purpose of the view. For simple views that just join one or more tables with no selection criteria, combine the names of the tables joined. For example, joining the &quot;Customer&quot; and &quot;StateAndProvince&quot; table to create a view of Customers and their respective geographical data should be given a name like &quot;vwCustomerStateAndProvince&quot;. Views created expressly for a report should have an additional prefix of Report applied to them, e.g. vwReportDivisionSalesFor2008.

### 2.7 Stored Procedures

Unlike a lot of the other database objects discussed here, stored procedures are not logically tied to any table or column. Typically though, stored procedures perform one or more common database activities (Read, Insert, Update, and/or Delete) on a table, or another action of some kind. Since stored procedures always perform some type of operation, it makes sense to use a name that describes the operation they perform. Use a verb to describe the type of operation, followed by the table(s) the operations occur on.

Prefixes or Suffixes:

The way you name your stored procedures depends on how you want to group them within a listing. It is recommended that you have your procedures ordered by the table/business entity they perform a database operation on, and adding the database activity &quot; Get, Save, or Delete&quot; as a suffix, e.g., &quot;spProductInfoGet&quot; or &quot;spOrderSave&quot;.

If your procedure returns a scalar value, or performs an operation like validation, you should use the verb and noun combination. For example, &quot;spValidateLogin&quot;.

The use of the &quot;sp&quot; prefix is required. This will help developers identify stored procedures and differentiate them from other non prefixed objects such as tables when viewing a listing of database objects.

Bad Prefixes:

Do not prefix your stored procedures with something that will cause the system to think it is a system procedure.

For example, in SQL Server, if you start a procedure with &quot;sp\_&quot;, &quot;xp\_&quot; or &quot;dt\_&quot; it will cause SQL Server to check the master database for this procedure first, causing a performance hit.

### 2.8 Functions

Functions follow many of the same rules that apply to naming stored procedures. There are only two differences that exist so the user of the function knows they are dealing with a function and not a stored procedure and all of the details that involves (value returned, can be used in a select statement, etc.).

Prefixes:

Use &quot;fn&quot; as prefix for your Functions as a helpful reminder that you&#39;re dealing with a function, and not a stored procedure.

Function Purpose:

Functions should be named as a verb, because they will always return a value (e.g. &quot;fnGetOpenDate&quot;, &quot;fnParseTableToString&quot;, &quot;fnFormatZip&quot;, etc.).

### 2.9 Triggers

Triggers have many things in common with stored procedures. However, triggers are different than stored procedures in two important ways. First, triggers don&#39;t exist on their own. They are dependent upon a table. So it is wise to include the name of this table in the trigger name. Second, triggers can only execute when an Insert, Update, or Delete happens on one or more of the records in the table.

We should avoid using trigger whenever possible. There are more troubles than benefits a trigger may bring us, especially, debugging and maintenance efforts. If they are deemed necessary, do it and follow rules below.

Prefixes and Suffixes:

To distinguish triggers from other database objects, it is helpful to add &quot;tr&quot; as a prefix, e.g. &quot;trProductInsert&quot;. Follow the &quot;tr&quot; is the table name, the operation that executes the trigger are suffixes (Insert, Update, or Delete)

For example:

- --trProductValidateBarcodeInsert
- --trProductValidateBarcodeUpdate

Multiple Operations:

If a trigger handles more than one operation (both INSERT and UPDATE for example) then include both operation abbreviations in your name. For example, &quot;trProductInsertUpdate&quot; or &quot;trProductUpdateDelete&quot;

Multiple Triggers:

Some systems allow multiple triggers per operation per table. In this case, you should make sure the names of these triggers are easy to distinguish between, e.g. &quot;trUserValidateEmailAddressInsert&quot; and &quot;trUserMakeActionEntriesInsert&quot;.

### 2.10 Synonyms

Synonym is a data object that provides an alias or alternate name for another database object referred to as the base object that can exist on a local or remote server. It is typically used for abstracting the base objects, their name or location, from client application.

Prefixes and Suffixes

As synonym definition, its name should be descriptive for its referred base object. To distinguish the base object and other database objects from synonym, use &quot;syn\_&quot; as prefix of base object name. For example:

- &quot;syn\_spOrderSave&quot; is the synonym of &quot;spOrderSave&quot; store procedure.
- &quot;syn\_fnGetOpenDate&quot; is the synonym of &quot;fnGetOpenDate&quot; function.
- &quot;syn\_vwOutStockProduct&quot; is the synonym of &quot;vwOutStockProduct&quot; view.
- &quot;syn\_Product&quot; is the synonym of &quot;Product&quot; table.

Linked Objects in Other Database

In some case of synonym object refers to the object in other database, not the local database where the synonym object resides, use &quot;syn\_&lt;DatabaseName/DatabaseNameAbbreviation&gt;\_&quot; as prefix. For example, we create a synonym object for other object in HRM database, and then its name should be:

- &quot;syn\_HRM\_spEmployeeSave&quot; is the synonym of &quot;spEmployeeSave&quot; store procedure in HRM database.
- &quot;syn\_HRM\_Employee&quot; is the synonym of &quot;Employee&quot; table in HRM database.

### 2.11 User-Defined Data Types

User-defined data types should be avoided whenever possible. They are an added processing overhead whose functionality could typically be accomplished more efficiently with simple data type variables, table variables, or temporary tables.

Prefixes and Suffixes:

To distinguish a user-defined data type from other database objects, it is helpful to add &quot;ud&quot; as a prefix.

Special Characters:

User-defined data type names should contain only letters, numbers and underscores. No special characters or spaces should be used.

### 2.12 Variables

In addition to the general naming standards regarding no special characters, no spaces, and limited use of abbreviations and acronyms, common sense should prevail in naming variables; variable names should be meaningful and natural.

Name length limit:

Variable names should describe its purpose and not exceed 50 characters in length.

Prefixes:

All variables must begin with the &quot;@&quot; symbol. Do NOT user &quot;@@&quot; to prefix a variable as this signifies a SQL Server system global variable and will affect performance.

Case:

All variables should be written in camelCase, e.g. &quot;@firstName&quot; or &quot;@city&quot; or &quot;@siteId&quot;.

Special Characters:

Variable names should contain only letters and numbers. No special characters or spaces should be used.

### 2.13 Use Modular Prefixes

When the scope of the database is expected to be enterprise level or scalability is a great concern consider using a modular object naming convention for primary database objects such as stored procedures and views. This methodology involves identifying primary modules of the system and assigning each of those modules a prefix. When these prefixes are applied to the names of database objects this allows us to easily locate module specific procedures and database objects for easier modification and debugging.

Example 1:

We have a modular system that deals with students and teacher data separately. We have defined these modules as such:

| Module | Prefix |
| --- | --- |
| Student | STU |
| Teacher | TEA |

As we implement naming conventions for our new objects processing specific to each module we create an easier way to find and view module specific functionality.

spSTUAttendanceInserUpdate

spTEACredentialsDelete

spSTUValidateStudentID

spTEAAddressInsertUpdate

spSTUAddressInsertUpdate

vwSTUAllStudents

## 3. Coding Convention
### 3.1 SQL Statements – SELECT

Use the more readable ANSI-Standard Join clauses (SQL-92 syntax) instead of the old style joins (SQL-89 syntax). The older syntax (in which the WHERE clause handles both the join condition and filtering data) is being phased out SQL Server 2005 and higher versions. This &quot;old style&quot; way of joining tables will NOT be supported in future versions of SQL Server.

The first of the following two queries shows the old style join, while the second one shows the new ANSI join syntax:

```sql
    SELECT
    a.AuthorId,
    t.Title
    FROM Titles t, Authors a, TitleAuthor ta
    WHERE
    a.AuthorId = ta.AuthorId AND
    ta.TitleId = t. TitleId AND
    t.Tit1e LIKE '%Computer%'

    SELECT
    a.AuthorId,
    t.Title
    FROM dbo.Authors a
    INNER JOIN dbo.TitleAuthor ta ON
    a.AuthorId = ta.AuthorId
    INNER JOIN dbo.Titles t ON
    ta.TitleId = t.Tit1eId
    WHERE
    t.Title LIKE '%Computer%'
```


Do not use the &quot;SELECT \*&quot; convention when gathering results from a permanent table, instead specify the field names and bring back only those fields you need; this optimizes query performance and eliminates the possibility of unexpected results when fields are added to a table.

Prefix all table name with the table owner (in most cases &quot;dbo.&quot;). This results in a performance gain as the optimizer does not have to perform a lookup on execution as well as minimizing ambiguities in your T-SQL.

Use aliases for your table names in most T-SQL statements; a useful convention is to make the alias out of the first or first two letters of each capitalized table name, e.g. &quot;Site&quot; becomes &quot;s&quot; and &quot;SiteType&quot; becomes &quot;st&quot;.

Capitalize all keyworks.

### 3.2 SQL Statements – INSERT

Always use a column list in your INSERT statements. This helps in avoiding problems when the table structure changes (like adding or dropping a column).

### 3.3 SQL Statements – Formatting

SQL statements should be arranged in an easy-to-read manner. When statements are written all to one line or not broken into smaller easy- to-read chunks, more complicated statements are very hard to decipher. By doing this and aliasing table names when possible, you will make column additions and maintenance of queries much easier.

Refer to the examples below.

Confusing SQL:

```sql
    SELECT dbo.DealUnitInvoice.DealUnitInvoiceID,
    dbo.DealUnitInvoice.UnitInventoryID, dbo.UnitInventory.UnitID,
    dbo.UnitInventory.StockNumber AS [Stock Number], dbo.UnitType.UnitType
    AS [Unit Type], ISNULL(dbo.Make.Description, '') AS Make,
    ISNULL(dbo.Model.Description, '') AS Model, DATEPART(YEAR,
    dbo.Unit.ProductionYear) AS [Year], dbo.UnitType.UnitTypeID,
    dbo.MeterType.Description AS MeterType, dbo.UnitInventory.MeterReading,
    dbo.UnitInventory.ECMReading, '$' + LTRIM(CONVERT(nvarchar(18),
```

Now look at the same SQL Statement but organized in an easy to read and more maintainable format:

```sql
    SELECT
    dui.DealUnitInvoiceID,
    dui.UnitInventoryID,
    ui.UnitID,
    ui.StockNumber [Stock Number],
    ut.UnitType AS [Unit Type],
    COALESCE(mk.Description, '') Make,
    COALESCE(ml.Description, '') Model,
    DATEPART(YEAR,u.ProductionYear) [Year],
    ut.UnitTypeID,
    mt.Description AS MeterType,
    ui.MeterReading,
    ui.ECMReading,
```
 Note how the tables are aliased and joins are clearly laid out in an organized manner.

### 3.4 Setting the NOCOUNT Option

Use SET NOCOUNT ON at the beginning of your SQL batches, stored procedures for report output and triggers in production environments, as this suppresses messages like &#39;(1 row(s) affected)&#39; after executing

INSERT, UPDATE, DELETE and SELECT statements. This improves the performance of stored procedures by reducing network traffic.

SET NOCOUNT ON is a procedural level instructions and as such there is no need to include a corresponding SET NOCOUNT OFF command as the last statement in the batch. Refer to the example below.

```sql
    CREATE PROCEDURE dbo.spDoStuff AS
    SET NOCOUNT ON
    SELECT * FROM MyTable
    INSERT INTO MyTable(Col1,Col2,Col3)
    SELECT 'One','Two','Three'
```

### 3.5 Code Commenting

Important code blocks within stored procedures and user defined functions should be commented. Brief functionality descriptions should be included where important or complicated processing is taking place.

Stored procedures and functions should include at a minimum a header comment with a brief overview of the batches functionality.

Comment syntax:

```sql
    -- single line comment use 2 dashes (--)
    /*
    block comments use ( /* ) to begin
    and ( */ ) to close
    */
```

Block comments are preferred to single line comments (even for commenting a single line) as cut and paste operations may dislocate the double-dash single line comment, whereas the block comments can never be dislocated.

### 3.6 Use Code Headers

Important code blocks within stored procedures and user defined functions should be commented. Brief functionality descriptions should be included where important or complicated processing is taking place.

```sql
    CREAIE PROCEDURE [dbo].[spGBLValidateConcurrency]
    @tablenane varchar(255),
    @recordID int,
    @lastUpdate datetine,
    @isValid bit OUTPUT
    AS
    /*****************************************************************
    This procedure validates the concurrency or a record update by taking
    the LastUpdate date passed in and checking it against the current
    LastUpdate date of the record. If they do NOT match the record is not
    updated because someone has updated the record out from under the user.
    ---------------------------
    Parameter defination
    ---------------------------
    @tableName - Table to be validated.
    @recordId - Record ID of the current record to be validated.
    @lastUpdate - The Last Update Date passed by app to compare with
    current date value for the record.
    @isvalid - Returns the following back to the calling app.
        1 - Record is valid. No concurrency issues.
        0 - Record is NOT concurrent.
    *****************************************************************/
```

### 3.7 Unicode vs. Non-Unicode Data Types

Use Unicode data types, like NCHAR, NVARCHAR, or NTEXT, ONLY if your database is going to store not just plain English characters, but a variety of characters used all over the world. Use these data types only when they are absolutely needed as they use twice as much space as non-Unicode data types.

### 3.8 CHAR vs. VARCHAR Data Types

Use the CHAR data type for a column only when the column is non-nullable. If a CHAR column is nullable, it is treated as a fixed length column in SQL Server 7.0+. So, a CHAR(100), when NULL, will eat up 100 bytes, resulting in space wastage. So, use VARCHAR(100) in this situation. Of course, variable length columns do have a very little processing overhead over fixed length columns. Carefully choose between CHAR and VARCHAR depending up on the length of the data you are going to store.

### 3.9 Very Large Strings

If you don&#39;t have to store more than 8KB of text, use CHAR(8000) or VARCHAR(8000) data types. If, however, (and only if) you find that you need to create a field to be sized to accommodate string or binary data &gt; 8KB, then use the VARCHAR(MAX) or VARBINARY(MAX) data types respectively. They are fully integrated with native T-SQL functions and do not require special functions like the old TEXT data types did.

### 3.10 Common Table Expression (CTE) over Sub Query

The Common Table Expression (CTE) is a construct that was introduced in SQL Server 2005. It allows you to define a SELECT statement outside of your main query and then reference it within the query. It&#39;s a great replacement for sub-queries, which can be difficult to debug and maintain especially once their nested. You can think of CTEs as SQL views that exist only within the scope of a particular SQL statement.

A common table expression can be used to:

- Create a recursive query.
- Substitute for a view when the general use of a view is not required.
- Enable grouping by a column that is derived from a scalar sub select, or a function.
- Reference the resulting table multiple times in the same statement.

Using a CTE offers the advantages of improved readability and ease in maintenance of complex queries. The query can be divided into separate, simple, logical building blocks. These simple blocks can then be used to build more complex, interim CTEs until the final result set is generated.

The following example shows both sub-query and CTE that produce the same result:

```sql
    /* Sub query */
    SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear
    FROM (
        SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear
        FROM Sales.Sale30rderHeader
        WHERE SalesPersonID IS NOT NULL
    ) sale
    GROUP BY SalesYear, SalesPersonID
    ORDER BY SalesPersonID, SalesYear;

    /* Common Table Expression */
    WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)
    AS
    -- Define the CTE query.
    (
        SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear
        FROM Sales.Sale30rderHeader
        WHERE SalesPersonID IS NOT NULL
    )
    -- Define the outer query referencing the CTE name.
    SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear
    FROM Sales_CTE
    GROUP BY SalesYear, SalesPersonID
    ORDER BY SalesPersonID, SalesYear;
```

### 3.11 Data Access and Transactions

Always access tables in the same order in all your stored procedures and triggers consistently. This helps to avoid deadlocks. Other things to keep in mind to avoid deadlocks are: Keep your transactions as short as possible. Touch as little data as possible during a transaction.

Always access tables in the same order in all your stored procedures and triggers consistently. This helps to avoid deadlocks. Other things to keep in mind to avoid deadlocks are: Keep your transactions as short as possible. Touch as little data as possible during a transaction.

Always check the global variable @@ERROR immediately after executing a data manipulation statement (like INSERT/UPDATE/DELETE), so that you can rollback the transaction in case of an error (@@ERROR will be greater than 0 in case of an error).

This is important, because, by default, SQL Server will not rollback all the previous changes within a transaction if a particular statement fails. Executing SET XACT\_ABORT ON can change this behavior. The @@ROWCOUNT variable also plays an important role in determining how many rows were affected by a previous data manipulation (also, retrieval) statement, and based on that you could choose to commit or rollback a particular transaction.

Sample transaction:

```sql
    DECLARE @sqlError INT
    SET @sqlError = 0
    BEGIN TRANSACTION
    UPDATE dbo.tbCacLic
    SET
    licCapacity = SOURCE.newLicCapacity,
    lastUpdtId = 'myLogin',
    lastUpdatedDate = GETDATE()
    FROM
    dbo.tbCacLic AS TARGET
    INNER JOIN #dcfsOldLic as SOURCE
    ON TARGET.applySiteId = SOURCE.applySiteId

    SELECT @sqlError = @@ERROR
    
    IF @sqlError = 0
    BEGIN
        COMMIT TRANSACTION
        DROP TABLE #dcfsOldLic
    END
    ELSE
    BEGIN
        ROLLBACK TRANSACTION
    END
```

The SQL Server 2008 or greater has added Try/Catch functionality to be able to catch error in a more natural way. See example in Error Handling section below for more info and if you&#39;re working with SQL Server 2008 or later, it is recommended to use the Try/Catch for catching error.

### 3.12 Error Handling

Although some procedural processes may not require additional error handling, as shown above in the Data Access and Transactions section there may be instances within your stored procedures you wish to handle errors more gracefully. You can use error handling to rollback entire transactions if one piece fails, report a single failed process within a procedure back to the calling application…etc. There are some examples below of proper implementation of error handling within a SQL Server stored procedure.

SQL Server 7.0 – 9.0(2005) – Use this methodology to handle errors in versions previous to SQL 2008 (10.0).

Tally errors. Rollback if failure occurs anywhere in proc.

```sql
    CREATE PROCEDURE dbo.spDoStuff
    @var1 INT
    AS
    SET NOCOUNT ON
    -- declare/initia1ize error counter

    DECLARE @err INT
    SELECT @err = 0

    BEGIN TRAN

    DELETE FROM dbo.MyTable
    WHERE Col1 = @var1
    SET @err = @err + @@ERROR

    INSERT INTO dbo.MyOtherTable(Col1)
    SELECT @var1
    SET @err = @err + @@ERROR

    IF @err = 0
    BEGIN
        COMMIT TRAN
        RETURN 0
    END
    ELSE
    BEGIN
        ROLLBACK TRAN
        RETURN @err
    END
```

End processing when error is reached and return error to application.

```sql
    CREATE PROCEDURE dbo.spDoStuff
    @var1 INT
    AS

    SET NOCOUNT ON

    -- declare error counter
    DECLARE @err int

    BEGIN TRAN

    DELETE FROM dbo.MyTab1e
    WHERE Col1 = @var1
    SET @err = @err + @@ERROR

    IF @err > 0 GOTO ERROR_HDLR

    INSERT INTO dbo.MyOtherTable(Col1)
    SELECT @var1
    SET @err = @err + @@ERROR

    IF @err > 0 GOTO ERROR_HDLR
    GOTO END_PROC

    -- Handle Errors
    ERROR_HDLR:
        ROLLBACK TRANSACTION
        RETURN @err

    -- Return & Exit
    END_PROC:
    COMMIT TRANSACTION
    RETURN 0
```

SQL Server 10.0(2008) and greater – SQL version 10.0 has added Try/Catch functionality and new functions to report error status to enhance error handling. You may implement this methodology when developing in SQL 10.0 or higher.

```sql
    CREATE PROCEDURE dbo.spDoStuff
    @var1 INT
    AS

    SET NOCOUNT ON
    BEGIN TRY
    BEGIN TRAN
        DELETE FROM dbo.MyTable
        WHERE Col1 = @var1

        INSERT INTO dbo.MyOtherTab1e(Col1)
        SELECT @var1

        COMMIT TRANSACTION

    END TRY
    BEGIN CATCH
        SELECT
        ERROR_NUMBER() as ErrorNumber,
        ERROR_NESSAGE() as ErrorMessage
        -- Test XACT_STATE for 1 or -1.
        -- XACT_STATE - 0 means there is no transaction and
        -- a commit or rollback operation would generate an error.
        -- Test whether the transaction is uncommittable.
        IF (XACT_STATE()) = -1
        BEGIN
            PRINT N'The transaction is in an uncommittable state. ' +
            'Rolling back transaction.'

            ROLLBACK TRAN
        END
        -- Test whether the transaction is active and valid.
        IF (XACT_$TATE()) = 1
        BEGIN
            PRINT N'The transaction is committable. ' +
            'Committing transaction.'
            COMMIT TRAN
        END
    END CATCH
```

### 3.13 Foreign Key and Check Constraints

Unique foreign key constraints should ALWAYS be enforced across alternate keys whenever possible. Not enforcing these constraints will compromise data integrity.

Perform all your referential integrity checks and data validations using constraints (foreign key and check constraints) instead of triggers, as they are faster. Limit the use triggers only for auditing, custom tasks and validations that cannot be performed using constraints. Constraints save you time as well, as you don&#39;t have to write code for these validations, allowing the RDBMS to do all the work for you. And remember, avoid using trigger whenever possible as aforementioned.

### 3.14 Cursor Usage

Try to avoid server side cursors as much as possible. Always stick to a &#39;set-based approach&#39; instead of a &#39;procedural approach&#39; for accessing and manipulating data. Cursors can often be avoided by using SELECT statements instead or at worst, temporary tables and/or table variables.

Should the need arise where cursors are the only option, avoid using dynamic and update cursors. Make sure you define your cursors as local, forward only to increase performance and decrease overhead.

### 3.15 Temporary Tables and Table Variables

Use temporary tables (e.g. #NslClaims) only when absolutely necessary. When temporary storage is needed within a T-SQL statement or procedure, it&#39;s recommended that you use local table variables (e.g. @NslClaims) instead if the amount of data stored is relatively small. This eliminates unnecessary locks on system tables and reduces the number of recompiles on stored procedures. This also increases performance as table variables are created in RAM, which is significantly faster than physical disk. You can increase performance on temporary tables and table variables in some instances by applying indexes. However, SQL 2005 and greater handles indexes on temp tables and variables much better than SQL 2000. Also keep in mind that when using indexes it can decrease performance on inserts and updates so use caution when choosing indexed columns.

### 3.16 Parameter Sniffing – Be Warned

With SQL Server version 9.0 and greater the database engine has enhanced parameter sniffing capability according to Microsoft. This functionality should be monitored with caution as we found that it has bugs. Parameter sniffing cannot be turned off...and has been deemed a &quot;feature&quot; of SQL Server. It basically sniffs the values of incoming stored procedure and function parameters and tries to adjust the query optimization plan accordingly. The problem is under many scenarios it adjusts it for the worse and severely affects the performance of the procedure.

There is, however, a work around. See the example below. By using this method you will in effect bypass parameter sniffing. I would suggest only using this where you find problems with parameter sniffing. And of course, avoid as much as possible the situation in which we have to deal with parameter sniffing.

```sql
    CREATE PROCEDURE dbo.spDoStuff
    @var1 int,
    @var2 varchar(20)
    AS
    SET NOCOUNT 0N

    -----Bypass parameter sniffing--
    DECLARE @var1a int,
    @var2a varchar(20)

    SELECT @var1a = @var1,
    @var2a = @var2
    ------end bypass-----------

    SELECT *
    FROM MyTable
    WHERE col1 = @var1a
    and col2 = @var2a
```

## 4. Database Design – Best Practices

Using SQL Servers RDBMS platform to its fullest potential is encouraged. Below are a few tips to aide in maximizing the built in features of relational database structures.

- Utilize enforced relationships between tables to protect data integrity when possible. Always remember... garbage in… garbage out. The data will only ever be as good as the integrity used to store it.
- Take care to normalize data as much as possible while still achieving peak performance and maintainability. Over-normalization can also be an issue as it can have a severe effect on performance and data maintenance and cause un-needed overhead. Entities and their proposed uses should be studied to formulate a data model that can balance integrity, scalability and performance.
- Make use of auto-numbered surrogate keys on all tables. This can reduce data storage where compound primary and foreign keys are prevalent and simplify relationships between data when normalizing data structures and writing queries.
- Always use primary keys on tables! Even if you are enforcing integrity through other means (i.e. business layer, unique table index) always put a primary key on a table. Tables with no primary key are a problem waiting to happen.
- Utilize indexes and fill factors correctly. Nothing can speed up data throughput more than correct utilization of clustered indexes, regular indexes and fill factors. This can be tricky business but SQL Server has a small host of tools that can assist. Nothing better than experience when it comes to optimizing queries and insert/update performance. If you are unsure how to proceed with optimizations consult the DBA.
- Database security is always a concern. ISBE has implemented functionality to increase security by obscuring server and database connectivity information using CIAM and IWAS as well as disabling SQL Server functionality that can be used maliciously or used to gain control of a database server. Close attention must be paid when developing front end applications and stored procedures to protect against SQL injection attacks. Make sure to consult the DBA when establishing your database security model.
