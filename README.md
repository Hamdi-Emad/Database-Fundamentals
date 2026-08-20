# 🗄️ Database Fundamentals 🐱‍👤

> **Database Fundamentals --- Complete Study Reference**\
> A structured guide to understand how databases work, how to model them
> with ERD, how to map ERD into relational tables, and how to normalize
> those tables up to 3NF.

------------------------------------------------------------------------

## 📚 Table of Contents

1.  [Database Fundamentals Overview](#1--database-fundamentals-overview)
2.  [Before Databases --- File Processing
    Systems](#2--before-databases--file-processing-systems)
3.  [Why Do We Need Databases?](#3--why-do-we-need-databases)
4.  [What Is a Database?](#4--what-is-a-database)
5.  [Database Advantages](#5--database-advantages)
6.  [How a Database System Works](#6--how-a-database-system-works)
7.  [Database System Components](#7--database-system-components)
8.  [Database Lifecycle & Roles](#8--database-lifecycle--roles)
9.  [Conceptual vs Physical
    Database](#9--conceptual-vs-physical-database)
10. [Relational Terminology](#10--relational-terminology)
11. [ERD --- Entity Relationship
    Diagram](#11--erd--entity-relationship-diagram)
12. [Entities](#12--entities)
13. [Attributes](#13--attributes)
14. [Keys](#14--keys)
15. [Relationships](#15--relationships)
16. [Cardinality](#16--cardinality)
17. [Participation](#17--participation)
18. [Relationship Attributes](#18--relationship-attributes)
19. [Strong & Weak Entities](#19--strong--weak-entities)
20. [ERD Thinking Process](#20--erd-thinking-process)
21. [Mapping ERD to Relational
    Tables](#21--mapping-erd-to-relational-tables)
22. [Mapping a Strong Entity](#22--mapping-a-strong-entity)
23. [Mapping a Weak Entity](#23--mapping-a-weak-entity)
24. [Mapping 1:M Relationships](#24--mapping-1m-relationships)
25. [Mapping M:M Relationships](#25--mapping-mm-relationships)
26. [Mapping 1:1 Relationships](#26--mapping-11-relationships)
27. [Mapping Ternary Relationships](#27--mapping-ternary-relationships)
28. [Mapping Cheat Sheet](#28--mapping-cheat-sheet)
29. [Normalization](#29--normalization)
30. [Why Normalize?](#30--why-normalize)
31. [Functional Dependency](#31--functional-dependency)
32. [0NF --- Unnormalized Form](#32--0nf--unnormalized-form)
33. [1NF --- First Normal Form](#33--1nf--first-normal-form)
34. [2NF --- Second Normal Form](#34--2nf--second-normal-form)
35. [3NF --- Third Normal Form](#35--3nf--third-normal-form)
36. [Normalization Workflow](#36--normalization-workflow)
37. [Complete Normalization
    Example](#37--complete-normalization-example)
38. [Database Fundamentals Mental
    Map](#38--database-fundamentals-mental-map)
39. [Final Revision Checklist](#39--final-revision-checklist)

------------------------------------------------------------------------

# 1. 🧭 Database Fundamentals Overview

Database Fundamentals is the foundation for understanding how data is:

``` text
Collected
   ↓
Organized
   ↓
Stored
   ↓
Related
   ↓
Retrieved
   ↓
Maintained
```

The main idea is not just **storing data**.

It is about designing data in a way that makes it:

-   Organized
-   Consistent
-   Accessible
-   Related correctly
-   Easy to maintain
-   Less repetitive

The three major stages covered in this reference are:

``` text
              DATABASE FUNDAMENTALS
                       │
          ┌────────────┼────────────┐
          │            │            │
         ERD         Mapping    Normalization
          │            │            │
      Model the     Convert      Improve the
       system      ERD → Tables  table design
```

------------------------------------------------------------------------

# 2. 📁 Before Databases --- File Processing Systems

Before database systems became the standard approach, organizations
commonly stored information using **file processing systems**.

The basic idea was:

``` text
Application
    │
    ▼
Data Files
```

Different applications could have their own files.

For example:

``` text
Student Application
      │
      └── Students.txt

Library Application
      │
      └── Students.txt

Finance Application
      │
      └── Students.txt
```

The same student information could therefore appear in multiple places.

------------------------------------------------------------------------

## Problems with File Processing

### 1. 🔁 Data Redundancy

The same information may be stored repeatedly.

``` text
Students File
Ahmed | Cairo | 20

Library File
Ahmed | Cairo | 20

Finance File
Ahmed | Cairo | 20
```

The same data exists in multiple files.

------------------------------------------------------------------------

### 2. ⚠️ Data Inconsistency

If duplicated information is changed in one file but not another:

``` text
File A → Ahmed | Cairo
File B → Ahmed | Giza
```

Which value is correct?

The system can end up containing conflicting information.

------------------------------------------------------------------------

### 3. 🔒 Data Isolation

Data is distributed across separate files and applications.

This makes it harder to combine information.

For example:

``` text
Employee File
      +
Department File
      +
Project File
```

A system may need to manually combine information from different files.

------------------------------------------------------------------------

### 4. 🧩 Difficult Data Sharing

When every application manages its own files, sharing data between
applications becomes harder.

------------------------------------------------------------------------

### 5. 🔧 Program--Data Dependence

Applications are often tightly connected to the structure of their
files.

Changing the file structure may require changing the application.

------------------------------------------------------------------------

### 6. 🚫 Difficult Data Integrity

It becomes harder to enforce rules such as:

``` text
Every Employee must have a valid ID
Department ID must exist
Salary cannot be negative
```

------------------------------------------------------------------------

### 7. 🔐 Difficult Security Management

Controlling exactly who can access which pieces of information becomes
more difficult when data is spread across independent files.

------------------------------------------------------------------------

### 8. 🔄 Difficult Concurrent Access

Multiple users or applications may try to access or modify the same
information at the same time.

Managing this safely is difficult without a dedicated database system.

------------------------------------------------------------------------

### 9. 💾 Difficult Backup and Recovery

Maintaining reliable backup and recovery across many independent files
becomes more complicated.

------------------------------------------------------------------------

# 3. 🚀 Why Do We Need Databases?

The problems of file processing lead to the need for a centralized and
organized way to manage data.

A database system helps us:

``` text
Reduce Redundancy
       ↓
Improve Consistency
       ↓
Connect Related Data
       ↓
Control Access
       ↓
Maintain Integrity
       ↓
Support Multiple Users
       ↓
Retrieve Data Efficiently
```

------------------------------------------------------------------------

# 4. 🗃️ What Is a Database?

A **database** is an organized collection of related data that can be
stored, managed, and accessed efficiently.

Think of it as:

``` text
                 DATABASE
                     │
       ┌─────────────┼─────────────┐
       │             │             │
    Students      Courses       Employees
       │             │             │
       └─────────────┼─────────────┘
                     │
               Related Data
```

A database is not simply a collection of random information.

The data is structured according to a defined model.

------------------------------------------------------------------------

# 5. ⭐ Database Advantages

A database system helps provide:

### 🔹 Reduced Redundancy

Avoid unnecessary duplication of the same information.

### 🔹 Better Consistency

A controlled data source reduces conflicting copies.

### 🔹 Data Sharing

Multiple applications and users can work with the same database.

### 🔹 Data Integrity

Rules can be used to keep data valid.

Examples:

``` text
PRIMARY KEY
FOREIGN KEY
NOT NULL
UNIQUE
CHECK
```

### 🔹 Security

Access can be controlled according to users and privileges.

### 🔹 Efficient Retrieval

Users can retrieve specific information without manually searching
through files.

### 🔹 Concurrent Access

Multiple users can work with the database while the system manages
access.

### 🔹 Backup & Recovery

Database systems provide mechanisms for protecting and recovering data.

------------------------------------------------------------------------

# 6. ⚙️ How a Database System Works

A simplified database system can be understood as:

``` text
             USERS
               │
               ▼
       APPLICATION / SQL
               │
               ▼
             DBMS
               │
      ┌────────┴────────┐
      │                 │
      ▼                 ▼
   Database         Metadata
      │
      ▼
 Tables / Relationships
```

### Step-by-step

### 1️⃣ User

A user needs information or wants to modify data.

### 2️⃣ Application / SQL

The request is sent through an application or directly using SQL.

### 3️⃣ DBMS

The **Database Management System** processes the request.

### 4️⃣ Database

The DBMS reads or modifies the required data.

### 5️⃣ Result

The requested information is returned to the user or the requested
modification is performed.

------------------------------------------------------------------------

# 7. 🧩 Database System Components

A complete database environment can be viewed as:

``` text
                    DATABASE SYSTEM
                          │
      ┌────────────┬──────┼──────┬────────────┐
      │            │      │      │            │
   Hardware      DBMS  Database Applications Users
```

## Hardware

The physical infrastructure used to run the database system.

Examples:

-   Servers
-   Storage
-   Network devices
-   Client machines

------------------------------------------------------------------------

## DBMS

**Database Management System**

The software layer responsible for managing the database.

It provides services such as:

-   Data storage management
-   Data retrieval
-   Security
-   Integrity
-   Concurrency
-   Backup and recovery
-   Transaction management

------------------------------------------------------------------------

## Database

The actual organized collection of data.

It contains structures such as:

``` text
Tables
Relationships
Constraints
Indexes
Views
```

------------------------------------------------------------------------

## Application Programs

Applications provide interfaces through which users interact with the
database.

``` text
User
  ↓
Application
  ↓
DBMS
  ↓
Database
```

------------------------------------------------------------------------

## Users

Different people interact with the system for different purposes.

Examples include:

-   End Users
-   Application Programmers
-   Database Administrators
-   Database Designers
-   System Analysts

------------------------------------------------------------------------

# 8. 👥 Database Lifecycle & Roles

The course material describes a lifecycle involving several roles:

``` text
System Analyst
      ↓
Requirements
      ↓
Database Designer
      ↓
Database Design
      ↓
Database Administrator
      ↓
Implementation
      ↓
Application Programmer
      ↓
Application Development
      ↓
End User
```

### 🧑‍💼 System Analyst

Focuses on understanding requirements.

``` text
What does the organization need?
```

------------------------------------------------------------------------

### 🧑‍💻 Database Designer

Focuses on database design.

``` text
How should the data be structured?
What entities exist?
How are they related?
```

------------------------------------------------------------------------

### 🛡️ Database Administrator

Responsible for implementation and database administration.

------------------------------------------------------------------------

### 👨‍💻 Application Programmer

Develops applications that interact with the database.

------------------------------------------------------------------------

### 👤 End User

Uses the final system.

------------------------------------------------------------------------

# 9. 🧠 Conceptual vs Physical Database

The database lifecycle distinguishes between conceptual and physical
perspectives.

## Conceptual Level

Focuses on:

``` text
What data exists?
What does it mean?
How is it related?
```

This is where **ERD** is especially important.

------------------------------------------------------------------------

## Physical Level

Focuses on how the database is actually implemented.

``` text
Tables
Columns
Keys
Indexes
Storage
```

### Mental Model

``` text
REAL WORLD
    ↓
REQUIREMENTS
    ↓
CONCEPTUAL MODEL
    ↓
ERD
    ↓
RELATIONAL MODEL
    ↓
TABLES
    ↓
PHYSICAL DATABASE
```

------------------------------------------------------------------------

# 10. 🔄 Relational Terminology

The course material uses equivalent terms:

  Database Concept   |Relational Term|
  ------------------ |-----------------------------
  Entity             |Table / Relation
  Attribute          |Column / Field
  Record             |Row / Tuple
  Cell               |Single value / Domain value


### Important Rule

> A cell should contain **a single value**.

``` text
❌ Phone
01012345678, 01198765432

✅ Phone
01012345678

✅ Phone
01198765432
```

This idea becomes particularly important when studying **1NF**.

------------------------------------------------------------------------

# 11. 🧩 ERD --- Entity Relationship Diagram

**ERD = Entity Relationship Diagram**

It is a conceptual model used to represent:

``` text
Entities
+
Attributes
+
Relationships
+
Constraints
```

The ERD helps us understand the system **before converting it into
relational tables**.

------------------------------------------------------------------------

# 12. 📦 Entities

An **Entity** represents a real-world object or concept that we want to
store information about.

Examples:

``` text
Student
Employee
Department
Course
Project
Customer
```

------------------------------------------------------------------------

## Strong Entity

A strong entity:

-   Can exist independently.
-   Has its own Primary Key.
-   Does not depend on another entity for identification.

Example:

``` text
STUDENT
────────────
Student_ID  PK
Name
Age
```

------------------------------------------------------------------------

## Weak Entity

A weak entity:

-   Cannot be uniquely identified using its own attributes alone.
-   Depends on a strong entity.
-   Has a Partial Key.
-   Uses the strong entity's PK as part of its own PK.

Example:

``` text
EMPLOYEE
   │
   │ identifies
   ▼
DEPENDENT
```

The weak entity becomes identifiable through the combination of:

``` text
Strong Entity PK
+
Weak Entity Partial Key
```

------------------------------------------------------------------------

# 13. 🏷️ Attributes

An **Attribute** describes a property of an entity.

Example:

``` text
STUDENT
   │
   ├── Student_ID
   ├── Name
   ├── Age
   └── Address
```

The course material covers several attribute types.

------------------------------------------------------------------------

## Simple Attribute

Cannot be divided into smaller meaningful parts.

Example:

``` text
Age
```

------------------------------------------------------------------------

## Composite Attribute

Can be divided into smaller components.

Example:

``` text
Address
   ├── Street
   └── City
```

------------------------------------------------------------------------

## Single-Valued Attribute

Has one value for each entity.

Example:

``` text
Student_ID
```

------------------------------------------------------------------------

## Multi-Valued Attribute

Can have multiple values for one entity.

Example:

``` text
Student
   │
   └── Phone
        ├── 010...
        └── 011...
```

------------------------------------------------------------------------

## Derived Attribute

Calculated from other attributes.

Example:

``` text
Date_of_Birth
      ↓
    Age
```

The derived value can be calculated instead of storing it directly.

------------------------------------------------------------------------

## Key Attribute

An attribute used to uniquely identify an entity.

Example:

``` text
Student_ID
```

------------------------------------------------------------------------

# 14. 🔑 Keys

## Primary Key --- PK

A Primary Key uniquely identifies a record.

Properties:

-   Unique
-   Cannot contain `NULL`
-   Identifies one record

Example:

``` text
STUDENT
──────────────
Student_ID PK
Name
Age
```

------------------------------------------------------------------------

## Foreign Key --- FK

A Foreign Key references the Primary Key of another table.

Example:

``` text
DEPARTMENT
────────────
Department_ID PK

EMPLOYEE
────────────
Employee_ID PK
Department_ID FK
```

The FK establishes the relationship between the tables.

> 💡 A Foreign Key can contain duplicate values because many rows may
> reference the same parent row.

------------------------------------------------------------------------

# 15. 🔗 Relationships

A **Relationship** represents an association between entities.

Examples:

``` text
Student ── enrolls in ── Course

Employee ── works for ── Department
```

------------------------------------------------------------------------

## Degree of Relationship

The course identifies:

### Unary / Self Relationship

An entity relates to itself.

``` text
EMPLOYEE
   │
   └── supervises ── EMPLOYEE
```

------------------------------------------------------------------------

### Binary Relationship

Relationship between two entities.

``` text
STUDENT ── enrolls ── COURSE
```

------------------------------------------------------------------------

### Ternary Relationship

Relationship among three entities.

``` text
EMPLOYEE
    \
     \
    WORKS_ON
     /    \
PROJECT   DEPARTMENT
```

The relationship itself involves three participating entities.

------------------------------------------------------------------------

# 16. 🔢 Cardinality

**Cardinality** describes how many instances of one entity can be
associated with another entity.

The course covers:

``` text
1 : 1
1 : M
M : M
```

------------------------------------------------------------------------

## 1 : 1 --- One-to-One

One instance of Entity A is related to one instance of Entity B.

``` text
A ───── 1 : 1 ───── B
```

Example:

``` text
Person ─── has ─── Passport
```

------------------------------------------------------------------------

## 1 : M --- One-to-Many

One instance on one side can be related to many instances on the other
side.

``` text
A ───── 1 : M ───── B
```

Example:

``` text
Department
     │
     └──────< Employees
```

One department can have many employees.

------------------------------------------------------------------------

## M : M --- Many-to-Many

Many instances of A can relate to many instances of B.

``` text
A ───── M : M ───── B
```

Example:

``` text
Student
   ↕
Course
```

A student can take many courses, and a course can contain many students.

------------------------------------------------------------------------

# 17. 🔘 Participation

Participation answers a different question from cardinality.

### Cardinality asks:

> **How many?**

### Participation asks:

> **Is participation required or optional?**

The course uses:

``` text
MAY
MUST
```

------------------------------------------------------------------------

## MUST --- Total Participation

Every entity must participate in the relationship.

``` text
Minimum cardinality = 1
```

Meaning:

``` text
Every instance MUST participate.
```

------------------------------------------------------------------------

## MAY --- Partial Participation

An entity may or may not participate.

``` text
Minimum cardinality = 0
```

Meaning:

``` text
Participation is optional.
```

------------------------------------------------------------------------

## 🧠 Cardinality vs Participation

Do not mix them.

``` text
CARDINALITY
How many?
   │
   ├── 1:1
   ├── 1:M
   └── M:M

PARTICIPATION
Required or optional?
   │
   ├── MUST
   └── MAY
```

### Another way to remember it

``` text
1 / M → Number
0 / 1 → Minimum participation
```

------------------------------------------------------------------------

# 18. 🏷️ Relationship Attributes

A **Relationship Attribute** describes the relationship itself rather
than one of the entities.

Example:

``` text
STUDENT ─── ENROLLS ─── COURSE
                  │
                 Grade
```

`Grade` belongs to the **Enrolls** relationship because the grade
depends on the specific Student--Course combination.

It is not simply a property of the student or the course.

------------------------------------------------------------------------

# 19. 💪 Strong & Weak Entities --- Quick Comparison

  -----------------------------------------------------------------------
  Strong Entity                       Weak Entity
  ----------------------------------- -----------------------------------
  Independent existence               Depends on a strong entity

  Has its own PK                      Uses strong entity PK as part of PK

  Does not need another entity for    Cannot be uniquely identified alone
  identification                      

  No partial key required             Has a partial key
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 20. 🧠 ERD Thinking Process

When you receive a database problem, think in this order:

``` text
1. Identify Entities
        ↓
2. Identify Attributes
        ↓
3. Identify Primary Keys
        ↓
4. Identify Relationships
        ↓
5. Determine Relationship Degree
        ↓
6. Determine Cardinality
        ↓
7. Determine Participation
        ↓
8. Identify Relationship Attributes
        ↓
9. Identify Strong / Weak Entities
```

### Example

Requirement:

> A department employs many employees.

Think:

``` text
Entities:
Department
Employee

Relationship:
Employs

Cardinality:
1 : M

Participation:
Determine from the requirements.
```

------------------------------------------------------------------------

# 21. 🔄 Mapping ERD to Relational Tables

**Mapping** means converting the conceptual ERD into relational tables.

``` text
ERD
 │
 │ Mapping
 ▼
Relational Schema
 │
 ├── Tables
 ├── PKs
 ├── FKs
 └── Relationship Tables
```

The course material covers six major mapping cases:

1.  Regular / Strong Entity
2.  Weak Entity
3.  Binary / Unary `1:M`
4.  Binary / Unary `M:M`
5.  Binary / Unary `1:1`
6.  Ternary Relationship

------------------------------------------------------------------------

# 22. 🏗️ Mapping a Strong Entity

A regular/strong entity becomes a table.

## Simple Attribute

Map it directly as a column.

``` text
ERD:

Student
 ├── Student_ID
 └── Name

        ↓

Student(
    Student_ID,
    Name
)
```

------------------------------------------------------------------------

## Derived Attribute

Do **not** map the derived attribute.

Example:

``` text
DOB ───────► Age
```

Store:

``` text
DOB
```

and calculate:

``` text
Age
```

when needed.

------------------------------------------------------------------------

## Composite Attribute

Break the composite attribute into its components.

``` text
Address
 ├── Street
 └── City
```

becomes:

``` text
Student(
    Student_ID,
    Street,
    City
)
```

------------------------------------------------------------------------

## Multi-Valued Attribute

Create a new table.

The new table contains:

``` text
Entity PK → FK
Multi-valued Attribute
```

The PK is a composite key made from:

``` text
Entity PK
+
Multi-valued Attribute
```

### Example

``` text
Employee
 └── Phone {multiple values}
```

becomes:

``` text
Employee
──────────────
Employee_ID PK
Name

Employee_Phone
──────────────
Employee_ID PK/FK
Phone       PK
```

------------------------------------------------------------------------

# 23. 🧱 Mapping a Weak Entity

For a weak entity:

1.  Add the strong entity's PK to the weak entity as an FK.
2.  Use the strong entity PK + weak entity partial key as the weak
    entity's composite PK.

### Example

``` text
EMPLOYEE
Employee_ID PK
     │
     │ identifies
     ▼
DEPENDENT
Dependent_Name
```

Mapping:

``` text
Employee
──────────────
Employee_ID PK
Name

Dependent
──────────────
Employee_ID      PK/FK
Dependent_Name   PK
Relation
```

### Composite PK

``` text
PK = Employee_ID + Dependent_Name
```

------------------------------------------------------------------------

# 24. 🔀 Mapping 1:M Relationships

For a binary/unary `1:M` relationship:

> Add the PK of the **1-side** to the **M-side** as an FK.

### Example

``` text
DEPARTMENT 1 ─────── M EMPLOYEE
```

Mapping:

``` text
Department
──────────────
Department_ID PK
Department_Name

Employee
──────────────
Employee_ID PK
Name
Department_ID FK
```

### 🧠 The Rule

``` text
1-side PK
    ↓
M-side FK
```

This is one of the most important mapping rules.

------------------------------------------------------------------------

## Relationship Attributes in 1:M

Relationship attributes are added to the M-side table.

Example:

``` text
Department 1 ─── employs ─── M Employee
                         │
                       Since
```

Then:

``` text
Employee(
    Employee_ID,
    Department_ID,
    Since
)
```

------------------------------------------------------------------------

# 25. 🔗 Mapping M:M Relationships

For an `M:M` relationship:

> Create a new table for the relationship.

Then:

1.  Add the PK of Entity A as an FK.
2.  Add the PK of Entity B as an FK.
3.  Combine them into a composite PK.
4.  Add relationship attributes to the new table.

### Example

``` text
STUDENT M ───── ENROLLS ───── M COURSE
```

Mapping:

``` text
Student
────────────
Student_ID PK
Name

Course
────────────
Course_ID PK
Course_Name

Enrollment
────────────
Student_ID PK/FK
Course_ID PK/FK
Grade
```

### Composite PK

``` text
PK = Student_ID + Course_ID
```

### 🧠 The Rule

``` text
M:M
 ↓
New Table
 ↓
PK(A) + PK(B)
 ↓
Both are FKs
 ↓
Together = Composite PK
```

------------------------------------------------------------------------

# 26. ↔️ Mapping 1:1 Relationships

The course distinguishes three participation combinations:

``` text
MAY – MUST
MAY – MAY
MUST – MUST
```

------------------------------------------------------------------------

## MAY -- MUST

Add the PK of the **MAY** side to the **MUST** side as an FK.

``` text
May Side
   │
   │ PK
   ▼
Must Side
   │
   └── FK
```

------------------------------------------------------------------------

## MAY -- MAY

Add the PK of either side to the other side as an FK.

``` text
A PK → B FK
```

or:

``` text
B PK → A FK
```

------------------------------------------------------------------------

## MUST -- MUST

Merge the two tables into one table.

``` text
A + B
  ↓
One Table
```

------------------------------------------------------------------------

## Relationship Attributes

Add relationship attributes to the table containing the FK.

------------------------------------------------------------------------

# 27. 🔺 Mapping Ternary Relationships

A ternary relationship involves three participating entities.

For mapping:

1.  Create a new table for the relationship.
2.  Add the PK of each participating entity as an FK.
3.  Determine the new table's PK according to the cardinality
    constraints.
4.  Add relationship attributes to the new table.

### Concept

``` text
Entity A
    \
     \
    Relationship
     /       \
Entity B    Entity C
```

becomes:

``` text
Relationship_Table
────────────────────
A_ID FK
B_ID FK
C_ID FK
Relationship_Attribute
```

The exact PK depends on the relationship's cardinality constraints.

------------------------------------------------------------------------

# 28. 📋 Mapping Cheat Sheet

  ERD Case                 Mapping Rule
  ------------------------ ----------------------------------------
  Strong Entity            Entity → Table
  Simple Attribute         Direct Column
  Composite Attribute      Split into components
  Derived Attribute        Do not map
  Multi-valued Attribute   New table + Entity PK/FK
  Weak Entity              Strong PK + Partial Key → Composite PK
  `1:M`                    1-side PK → M-side FK
  `M:M`                    New table + both PKs as FKs
  `1:1` MAY--MUST          MAY PK → MUST FK
  `1:1` MAY--MAY           PK of either side → FK on other
  `1:1` MUST--MUST         Merge tables
  Ternary                  New relationship table + three FKs

------------------------------------------------------------------------

# 29. 🧹 Normalization

**Normalization** is the process of organizing relational data to reduce
problematic redundancy and dependency issues.

The course focuses on:

``` text
0NF
 ↓
1NF
 ↓
2NF
 ↓
3NF
```

The goal is to transform a poorly structured relation into
better-structured tables.

------------------------------------------------------------------------

# 30. 🎯 Why Normalize?

Normalization helps us:

-   Reduce unnecessary repetition.
-   Separate independent facts.
-   Avoid update anomalies.
-   Make dependencies clearer.
-   Improve data organization.
-   Produce a cleaner relational design.

### Common Problems

Without proper normalization, we may face:

``` text
INSERT Anomaly
UPDATE Anomaly
DELETE Anomaly
```

------------------------------------------------------------------------

## 🔄 Update Anomaly

The same fact appears in multiple rows.

Changing it requires updating many records.

------------------------------------------------------------------------

## ➕ Insert Anomaly

We cannot insert one piece of information without also inserting
unrelated information.

------------------------------------------------------------------------

## ➖ Delete Anomaly

Deleting one record may accidentally remove another useful fact.

------------------------------------------------------------------------

# 31. 🧠 Functional Dependency

Functional dependency describes a dependency between attributes.

If:

``` text
A → B
```

it means:

> The value of `A` determines the value of `B`.

Example:

``` text
Student_ID → Student_Name
```

A student's ID determines that student's name.

------------------------------------------------------------------------

## Full Dependency

An attribute depends on the **entire Primary Key**.

This becomes especially important in `2NF`.

------------------------------------------------------------------------

## Partial Dependency

A non-key attribute depends on only **part of a composite Primary Key**.

This violates `2NF`.

------------------------------------------------------------------------

## Transitive Dependency

A non-key attribute depends on another non-key attribute.

Example:

``` text
Student_ID → Faculty_Code
Faculty_Code → Faculty_Name
```

Therefore:

``` text
Student_ID → Faculty_Name
```

through another non-key attribute.

This is the problem addressed by `3NF`.

------------------------------------------------------------------------

# 32. 🟤 0NF --- Unnormalized Form

0NF represents data before normalization.

It may contain:

-   Multi-valued attributes
-   Repeating groups
-   Composite attributes
-   Repeated information

Example:

``` text
Student
────────────────────────────────────────────
Student_No
Student_Name
Address(Street, City)
Tel
Faculty_Code
Faculty_Name
Major
Department_Name
Department_Desc
Admission_Grade
Comments
```

The address is composite, and phone numbers may be multi-valued.

------------------------------------------------------------------------

# 33. 🟢 1NF --- First Normal Form

A relation is in **1NF** when the course requirements are satisfied:

``` text
1. No Multi-valued Attributes
2. No Repeating Groups
3. No Composite Attributes
```

------------------------------------------------------------------------

## 1NF Rule #1 --- No Multi-Valued Attribute

Bad:

``` text
Student
────────────────
Student_ID
Phone
```

where Phone contains:

``` text
010...
011...
012...
```

Instead:

``` text
Student
────────────
Student_ID
Name

Student_Tel
────────────
Student_ID
Tel
```

The original PK becomes an FK in the new table.

------------------------------------------------------------------------

## 1NF Rule #2 --- No Repeating Groups

Bad:

``` text
Student_ID
Phone_1
Phone_2
Phone_3
```

Instead:

``` text
Student_Tel
────────────
Student_ID
Tel
```

Each phone becomes a separate row.

------------------------------------------------------------------------

## 1NF Rule #3 --- No Composite Attributes

Bad:

``` text
Address
  ├── Street
  └── City
```

Instead:

``` text
Street
City
```

------------------------------------------------------------------------

## 1NF Transformation

``` text
0NF
 │
 ├── Remove multi-valued attributes
 ├── Remove repeating groups
 └── Split composite attributes
 │
 ▼
1NF
```

------------------------------------------------------------------------

# 34. 🟡 2NF --- Second Normal Form

A relation must:

``` text
1. Be in 1NF
2. Have no Partial Dependency
3. Every Non-Key Attribute must depend on the whole PK
```

### Core Idea

``` text
Non-Key Attribute
       ↓
Must depend on
THE WHOLE PK
```

------------------------------------------------------------------------

## Partial Dependency Example

Suppose:

``` text
Project_Employee
────────────────────────────
Project_No      PK
Employee_No     PK
Employee_Name
Job_Class
CHG_HOUR
Hours_Billed
```

The PK is:

``` text
(Project_No, Employee_No)
```

But:

``` text
Project_No → Project_Name
Employee_No → Employee_Name
Employee_No → Job_Class
Employee_No → CHG_HOUR
```

Some attributes depend on only part of the composite key.

That is **Partial Dependency**.

------------------------------------------------------------------------

## How to Achieve 2NF

Move partially dependent attributes to their appropriate tables.

Example:

``` text
Project
────────────────
Project_No PK
Project_Name
```

``` text
Employee
────────────────
Employee_No PK
Employee_Name
Job_Class
CHG_HOUR
```

``` text
Project_Employee
────────────────
Project_No PK/FK
Employee_No PK/FK
Hours_Billed
```

Now:

``` text
Employee attributes
→ depend on Employee_No

Project attributes
→ depend on Project_No

Hours_Billed
→ depends on the whole combination
   (Project_No, Employee_No)
```

------------------------------------------------------------------------

# 35. 🟠 3NF --- Third Normal Form

A relation must:

``` text
1. Be in 2NF
2. Have no Transitive Dependency
3. Non-Key attributes must not depend on another Non-Key attribute
```

### Core Idea

``` text
Non-Key
   ↓
must NOT determine
another Non-Key
```

------------------------------------------------------------------------

## Transitive Dependency Example

Suppose:

``` text
Employee
────────────────────────
Employee_No PK
Employee_Name
Job_Class
CHG_HOUR
```

If:

``` text
Job_Class → CHG_HOUR
```

then:

``` text
Employee_No
    ↓
Job_Class
    ↓
CHG_HOUR
```

`CHG_HOUR` depends on another non-key attribute.

That is a **Transitive Dependency**.

------------------------------------------------------------------------

## How to Achieve 3NF

Separate the determining non-key attribute and the attribute that
depends on it.

``` text
Employee
────────────────
Employee_No PK
Employee_Name
Job_Class
```

``` text
Job_Class
────────────────
Job_Class PK
CHG_HOUR
```

Now:

``` text
Employee_No → Job_Class
Job_Class → CHG_HOUR
```

and the `CHG_HOUR` dependency is stored in its own relation.

------------------------------------------------------------------------

# 36. 🔄 Normalization Workflow

The easiest way to think about normalization is:

``` text
              0NF
               │
               ▼
        ┌───────────────┐
        │ Remove:       │
        │ • Multi-value │
        │ • Repeating   │
        │ • Composite   │
        └───────────────┘
               │
               ▼
              1NF
               │
               ▼
        ┌───────────────┐
        │ Remove:       │
        │ Partial       │
        │ Dependencies  │
        └───────────────┘
               │
               ▼
              2NF
               │
               ▼
        ┌───────────────┐
        │ Remove:       │
        │ Transitive    │
        │ Dependencies  │
        └───────────────┘
               │
               ▼
              3NF
```

------------------------------------------------------------------------

# 37. 🧪 Complete Normalization Example

The course material provides normalization examples involving students,
customers/rentals, and project billing.

A useful project-billing structure starts with:

``` text
Project_Employee
──────────────────────────────────────────────
Project_Num
Project_Name
Employee_Number
Employee_Name
Job_Class
CHG/HOUR
Hours_Billed
```

------------------------------------------------------------------------

## Step 1 --- 0NF

The original data mixes project, employee, job-class, and billing facts.

``` text
Project_Employee
────────────────────────────────────────────
Project_Num
Project_Name
Employee_Number
Employee_Name
Job_Class
CHG/HOUR
Hours_Billed
```

------------------------------------------------------------------------

## Step 2 --- 1NF

Remove repeating/multi-valued structures and ensure attributes are
atomic.

The course's project example reaches a structure such as:

``` text
Project
────────────────
Project_Num
Project_Name
```

``` text
Project_Employee
────────────────
Project_Num
Employee_Number
Employee_Name
Job_Class
CHG/HOUR
Hours_Billed
```

------------------------------------------------------------------------

## Step 3 --- 2NF

Identify partial dependencies.

Project information depends on:

``` text
Project_Num
```

Employee information depends on:

``` text
Employee_Number
```

Hours billed depends on the combination:

``` text
Project_Num + Employee_Number
```

So separate the independent facts:

``` text
Project
────────────────
Project_Num PK
Project_Name
```

``` text
Employee
────────────────
Employee_Number PK
Employee_Name
Job_Class
CHG/HOUR
```

``` text
Project_Employee
────────────────
Project_Num PK/FK
Employee_Number PK/FK
Hours_Billed
```

------------------------------------------------------------------------

## Step 4 --- 3NF

Now inspect non-key → non-key dependencies.

If:

``` text
Job_Class → CHG/HOUR
```

then:

``` text
Employee_Number
      ↓
   Job_Class
      ↓
   CHG/HOUR
```

This is transitive dependency.

Separate it:

``` text
Employee
────────────────
Employee_Number PK
Employee_Name
Job_Class
```

``` text
Job_Class
────────────────
Job_Class PK
CHG/HOUR
```

Final structure:

``` text
Project
────────────────
Project_Num PK
Project_Name
```

``` text
Employee
────────────────
Employee_Number PK
Employee_Name
Job_Class FK
```

``` text
Project_Employee
────────────────
Project_Num PK/FK
Employee_Number PK/FK
Hours_Billed
```

``` text
Job_Class
────────────────
Job_Class PK
CHG/HOUR
```

------------------------------------------------------------------------

# 38. 🧠 Database Fundamentals Mental Map

``` text
                       DATABASE
                           │
             ┌─────────────┴─────────────┐
             │                           │
        OLD APPROACH                DATABASE SYSTEM
       File Processing                    │
             │                            │
       ┌─────┴─────┐              ┌─────┴─────┐
       │           │              │           │
   Redundancy  Inconsistency    DBMS      Database
       │           │              │           │
       └─────┬─────┘              └─────┬─────┘
             │                          │
             ▼                          ▼
        Need for DB              Organized Data
                                      │
                                      ▼
                                    DESIGN
                                      │
                    ┌─────────────────┼─────────────────┐
                    │                 │                 │
                   ERD              MAPPING        NORMALIZATION
                    │                 │                 │
               Model Reality      ERD → Tables      Improve Tables
                    │                 │                 │
                    ▼                 ▼                 ▼
                Entities            PK / FK          1NF
                Attributes          Relationships     2NF
                Relationships       Tables            3NF
                Cardinality
                Participation
```

------------------------------------------------------------------------

# 39. 🎯 Final Revision Checklist

## Database Fundamentals

-   [ ] Explain what a database is
-   [ ] Explain what was used before database systems
-   [ ] Explain file processing systems
-   [ ] Explain data redundancy
-   [ ] Explain data inconsistency
-   [ ] Explain data isolation
-   [ ] Explain data sharing problems
-   [ ] Explain program--data dependence
-   [ ] Explain why databases are needed
-   [ ] List major database advantages
-   [ ] Explain what a DBMS does
-   [ ] Explain database system components
-   [ ] Explain the database lifecycle
-   [ ] Know the role of the System Analyst
-   [ ] Know the role of the Database Designer
-   [ ] Know the role of the Database Administrator
-   [ ] Know the role of the Application Programmer
-   [ ] Know the role of the End User
-   [ ] Distinguish conceptual and physical levels

## ERD

-   [ ] Define Entity
-   [ ] Distinguish Strong and Weak Entities
-   [ ] Define Attribute
-   [ ] Identify Simple Attributes
-   [ ] Identify Composite Attributes
-   [ ] Identify Single-Valued Attributes
-   [ ] Identify Multi-Valued Attributes
-   [ ] Identify Derived Attributes
-   [ ] Identify Key Attributes
-   [ ] Define Primary Key
-   [ ] Define Foreign Key
-   [ ] Define Relationship
-   [ ] Identify Unary / Self Relationships
-   [ ] Identify Binary Relationships
-   [ ] Identify Ternary Relationships
-   [ ] Understand `1:1`
-   [ ] Understand `1:M`
-   [ ] Understand `M:M`
-   [ ] Understand MAY participation
-   [ ] Understand MUST participation
-   [ ] Distinguish Cardinality from Participation
-   [ ] Identify Relationship Attributes

## Mapping

-   [ ] Map a Strong Entity
-   [ ] Map Simple Attributes
-   [ ] Map Derived Attributes
-   [ ] Map Composite Attributes
-   [ ] Map Multi-Valued Attributes
-   [ ] Map Weak Entities
-   [ ] Map `1:M`
-   [ ] Map `M:M`
-   [ ] Map `1:1`
-   [ ] Handle MAY--MUST
-   [ ] Handle MAY--MAY
-   [ ] Handle MUST--MUST
-   [ ] Map Ternary Relationships
-   [ ] Place Relationship Attributes correctly
-   [ ] Identify Composite Primary Keys

## Normalization

-   [ ] Explain the purpose of normalization
-   [ ] Understand 0NF
-   [ ] Understand 1NF
-   [ ] Remove multi-valued attributes
-   [ ] Remove repeating groups
-   [ ] Remove composite attributes
-   [ ] Understand 2NF
-   [ ] Understand partial dependency
-   [ ] Make non-key attributes depend on the whole PK
-   [ ] Understand 3NF
-   [ ] Understand transitive dependency
-   [ ] Remove non-key → non-key dependencies
-   [ ] Trace a table from 0NF → 1NF → 2NF → 3NF
-   [ ] Identify the PK at every stage
-   [ ] Identify the FK created during decomposition

------------------------------------------------------------------------

# 🧠 One-Minute Revision

``` text
DATABASE
→ Organized collection of related data

DBMS
→ Software that manages the database

ERD
→ Describes the real-world system

ENTITY
→ Becomes a table

ATTRIBUTE
→ Usually becomes a column

PK
→ Uniquely identifies a row

FK
→ References another table's PK

CARDINALITY
→ How many?

1:1
→ One-to-One

1:M
→ One-to-Many

M:M
→ Many-to-Many

PARTICIPATION
→ MAY or MUST?

MAPPING
→ ERD → Relational Tables

1:M
→ 1-side PK goes to M-side as FK

M:M
→ Create a new table

1:1
→ Mapping depends on participation

WEAK ENTITY
→ Strong PK + Partial Key

NORMALIZATION
→ Improve table structure

1NF
→ No Multi-value / Repeating / Composite attributes

2NF
→ 1NF + No Partial Dependency

3NF
→ 2NF + No Transitive Dependency
```

------------------------------------------------------------------------

# 🏁 The Big Picture

``` text
REAL-WORLD PROBLEM
        │
        ▼
   REQUIREMENTS
        │
        ▼
       ERD
        │
        ├── Entities
        ├── Attributes
        ├── Relationships
        ├── Cardinality
        └── Participation
        │
        ▼
     MAPPING
        │
        ├── Tables
        ├── PKs
        ├── FKs
        └── Relationship Tables
        │
        ▼
   NORMALIZATION
        │
        ├── 1NF
        ├── 2NF
        └── 3NF
        │
        ▼
   CLEAN RELATIONAL
      DATABASE
```



### *Written with all my heart, in the hope of striving toward and reaching the goal someday. ❤*