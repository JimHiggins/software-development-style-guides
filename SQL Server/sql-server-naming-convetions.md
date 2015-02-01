##SQL Server Naming Conventions

###Introduction

Naming conventions generate long debate friendly, and not so friendly. Conventions go in an out of fashion, and are subject to corporate mandates, and personal preferences. The naming conventions documented here represents a meeting point between a best guess at consensus and personal preference.

**Note:** Notice the word "avoid" being used over and over. These conventions are guideline, not absolutes.

####General Rules

**Avoid object names that require quotes**

Generally this means names with white spaces. Naming a table `Order Detail`, instead of `OrderDetail` can lead aggravated hours debugging.

**Avoid using reserved keywords for object names**

One can use [reserved keywords](https://msdn.microsoft.com/en-us/library/ms189822.aspx) as object names, but it falls into the category of just because you can, doesn't mean you should. At best, this will cause performance issues, at worst errors will get thrown.

**Avoid using data types as object names**

Like reserved keywords, naming objects like `text` or `timestamp` can cause confusion and errors.

**Avoid abbreviations**

SQL Server allow 128 characters for column names. Abbreviations, no matter how obvious they may seem, can cause confusion for a new person on the development team.

###Tables and Views

**Use Singular Nouns**

This is the stuff of drawn out debates, and used consistently pluralized objects work. But singular nouns provide a higher level of clarity.

_Example: `Person` vs `Persons` or `People`._

**Avoid Prefixes and Suffixes**

This is mostly pointed at prefixing object names with their function. Older guidelines might have you name tables `tbl_foo` and views `vw_bar`. This redundant and makes reading a list of object more difficult as your eyes scan in three characters to determine that the object really is. 

Avoiding prefixes also aids refactoring. An example is splitting a table in two, and then creating a view using the original name. The refactored objects could be completed with modifying application code.

**Note:** If you want to logically organize objects by application in the database, defining a schema is a good approach.


###Keys

**Primary Keys**

Name single column primary keys `id`. At the heart of a good naming is limiting ambiguity and aid the ability of programmer to intuit the nature of an object.

**Foreign Keys**

Name foreign keys a combination of the referencing table and `id`. In the name of the column one succinctly communicates the data stored, its function, and what it references.

_Example: `PersonId`_

Exceptions to this rule might include multiple columns that reference the same table. For example, one might have columns that record a project start and end date. In this example, both date columns reference a date dimension table. Generally speaking name these columns as a combination of a description and `id`. This will describe the data data stored, and indicate it is a key field.

_Example: `StartDateId` and `EndDateId`

###Indexes

Name as a combination of a prefix, underscore, table name, and column(s).

List of index prefixes:

- IX: Non clustered index
- UIX: Unique non clustered index
- CLIX: Clustered index (most of the time that will be the primary key)
- COVIX: Covering index

Do not to list the column names in a covering index. The nature of covering index would make the name too verbose.

###Constraints

Name constraints a combination of a prefix, underscore, table name, and column(s) name. 

For the primary key index there is not need to list the column. Unless the primary key is a compound key, the column, by convention, will be `Id`.

List of index prefixes:

- PK: Primary key
- DF: Default
- CK: Check constraint
- FK: Foreign Key

This is where the key naming convention is useful. If you have an `Order` table that references the `Customer table`, name the constraint `FK_Order_CustomerId`. This name explains the object is a foreign key constraint on the `Order` table's `CustomerId` column. The column name explains the `Customer` table is the reference.


### Stored Procedures & User Defined Functions

Name stored procedures and user defined functions with an object verb combination, separated by an underscore. A good argument can be made to use the PowerShell verb noun combination. But a object verb combination help group procedures and UDFs to related objects.

_Example: `Customer_Insert`, `Custoemr_GetAll`





