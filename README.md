# Database Fundamentals 🐱‍👤

A structured summary of the main Database Fundamentals concepts, including Database Lifecycle, ERD, Mapping, Keys, Relationships, and Normalization.

---


# 🔴 1... Database Lifecycle

The Database Lifecycle consists of several stages involving different roles:

| Role                             | Responsibility          |
| -------------------------------- | ----------------------- |
| **System Analyst**               | Requirements            |
| **Database Designer**            | Database Design         |
| **Database Administrator (DBA)** | Implementation          |
| **Application Programmer**       | Application Development |
| **End User**                     | Uses the system         |

### Database Design Levels

* **Conceptual**
* **Physical**

---

# 🔴 2. Relational Model

| Concept    | Relational Model        |
| ---------- | ----------------------- |
| **Table**  | Entity / Relation       |
| **Column** | Field / Attribute       |
| **Row**    | Record / Tuple          |
| **Cell**   | Contains a single value |

> A cell should carry only a single value.

---

# 🔴 3. ERD — Entity Relationship Diagram

An **Entity Relationship Diagram (ERD)** is a graphical representation of the entities, attributes, and relationships within a database.

---

## 🔰 1. Entity

An **Entity** represents a real-world object or concept that can be identified and about which data can be stored.

Examples:

- **Student**
- **Employee**
- **Department**

### Types of Entities

#### Strong Entity

- Can exist independently.
- Has its own **Primary Key**.
- Does not depend on another Entity for identification.

#### Weak Entity

- Cannot be uniquely identified by its own attributes.
- Depends on a **Strong Entity**.
- Has a **Partial Key**.
- Uses the Strong Entity's **PK** as part of its own PK.

---

## 🔰 2. Attribute

An **Attribute** describes a property or characteristic of an Entity.

Examples:

- **Student_ID**
- **Name**
- **Age**

### Types of Attributes

- **Simple Attribute:** Cannot be divided into smaller parts.
- **Composite Attribute:** Can be divided into smaller components.
- **Single-valued Attribute:** Has one value for each Entity.
- **Multi-valued Attribute:** Can have multiple values for one Entity.
- **Derived Attribute:** Calculated from other Attributes.
- **Key Attribute:** Uniquely identifies each Entity.

---

## 🔰 3. Relationship

A **Relationship** represents an association between Entities.

### Examples

- Student **enrolls in** Course.
- Employee **works for** Department.

### Degree of Relationship

#### Unary

An Entity relates to itself.

Example:

**Employee supervises Employee**

#### Binary

A Relationship between two Entities.

Example:

**Employee works for Department**

#### Ternary

A Relationship among three Entities.

Example:

**Nurse gives Drug to Patient**

---

## 🔰 4. Relationship Attributes

A **Relationship Attribute** describes the Relationship itself rather than any participating Entity.

### Example

**Student — Enrolls — Course**

The following Attribute:

**Grade**

belongs to the **Enrolls Relationship**, because the grade depends on the specific Student–Course combination.

> Relationship Attributes are especially important when mapping M:M and Ternary Relationships.

---

## 🔰 5. Cardinality

Cardinality defines **how many instances** of one Entity can be associated with instances of another Entity.

| Cardinality | Meaning |
|---|---|
| **1:1** | One-to-One |
| **1:M** | One-to-Many |
| **M:M** | Many-to-Many |

### Examples

- **1:1:** Person — Passport
- **1:M:** Department — Employee
- **M:M:** Student — Course

---

## 🔰 6. Participation / Optionality

Participation defines whether an Entity **must** or **may** participate in a Relationship.

### Must — Total Participation

- Every Entity **must participate** in the Relationship.
- Minimum cardinality = **1**

### May — Partial Participation

- Entity **may or may not participate** in the Relationship.
- Minimum cardinality = **0**

> **Cardinality and Participation are different concepts.**
>
> **Cardinality:** How many?
>
> **Participation:** Must or may?

---

# 🔑 Keys

## Primary Key (PK)

- A **unique identifier** for each record.
- Must be **Unique**.
- Cannot contain **NULL** values.
- An Entity normally has one **Primary Key**.
- A Primary Key can consist of more than one Attribute, forming a **Composite Primary Key**.

## Foreign Key (FK)

- An Attribute that references the **PK of another table**.
- Used to establish a **Relationship between tables**.
- Can contain **Duplicate Values**.
- Can be **NULL** depending on the Relationship and constraints.

---

# 🔴 4. Mapping in ERD

## Mapping Types

1. Mapping of Regular / Strong Entity
2. Mapping of Weak Entity
3. Mapping of Binary / Unary 1:M Relationship
4. Mapping of Binary / Unary M:M Relationship
5. Mapping of Binary / Unary 1:1 Relationship
6. Mapping of Ternary Relationship

---

## 🔰 1. Mapping of Regular / Strong Entity

* **Simple Attribute:** Map it directly as a column.
* **Derived Attribute:** Do not map it.
* **Composite Attribute:** Decompose it into its components and map them separately.
* **Multi-valued Attribute:** Create a new table containing the entity's PK as a FK. The new table has a Composite PK consisting of the entity's PK and the multi-valued attribute.

---

## 🔰 2. Mapping of Weak Entity

* Add the **PK of the Strong Entity** to the Weak Entity as a FK.
* The PK of the Weak Entity is a **Composite PK**, consisting of:

  * The PK of the Strong Entity.
  * The Partial Key of the Weak Entity.

---

## 🔰 3. Mapping of Binary / Unary 1:M Relationship

* Add the **PK of the 1-side** to the M-side as a FK.
* Add the **Relationship Attributes** to the M-side table.

---

## 🔰 4. Mapping of Binary / Unary M:M Relationship

* Create a **new table** for the Relationship.
* Add the PKs of both Entities as FKs.
* The PK of the new table is a **Composite PK** consisting of both PKs.
* Add the **Relationship Attributes** to the new table.

---

## 🔰 5. Mapping of Binary / Unary 1:1 Relationship

### May – Must

* Add the PK of the **May side** to the **Must side** as a FK.

### May – May

* Add the PK of either side to the other side as a FK.

### Must – Must

* Merge the two tables into one table.

### Relationship Attributes

* Add the Relationship Attributes to the table containing the FK.

---

## 🔰 6. Mapping of Ternary Relationship

* Create a **new table** for the ternary relationship.
* Add the PK of each participating Entity to the new table as FKs.
* The PK of the new table is determined by the **cardinality constraints** of the ternary relationship.
* Add the **Relationship Attributes** to the new table.

---

# 🔴 5. Normalization

Normalization is the process of organizing relations to eliminate unwanted dependencies and improve the structure of the database.

## 🔰 1. 1NF — First Normal Form

### Requirements

* A relation must contain **no Multivalued Attributes**.
* No **Repeating Groups**.
* No **Composite Attributes**.

### To Achieve 1NF

* **Repeating Group:** Move it to a new table + add the original PK as a FK.
* **Multi-valued Attribute:** Move it to a new table + add the original PK as a FK.
* **Composite Attribute:** Split its subparts into separate columns.

---

## 🔰 2. 2NF — Second Normal Form

### Requirements

* Must be in **1NF**.
* No **Partial Dependency**.
* Every Non-Key Attribute must depend on the **whole PK**.

### To Achieve 2NF

* Move the partially dependent Non-Key Attributes to a new table.
* Add the **part of the PK they depend on** as the new table's PK/FK.

> **Key Idea:** In 2NF, every Non-Key Attribute must depend on the **whole Primary Key**, not just part of it.

---

## 🔰 3. 3NF — Third Normal Form

### Requirements

* Must be in **2NF**.
* No **Transitive Dependency**.
* A Non-Key Attribute must not depend on another **Non-Key Attribute**.

### To Achieve 3NF

* Move the dependent Non-Key Attributes to a new table.
* Keep the Non-Key Attribute they depend on in the new table.
* Keep that determining Non-Key Attribute in the original table as well.

> **Key Idea:** In 3NF, Non-Key Attributes should not depend on other Non-Key Attributes.

---

# Quick Revision

```text
ERD
│
├── Entity
├── Attribute
├── Relationship
├── Cardinality
└── Participation

Mapping
│
├── Strong Entity
├── Weak Entity
├── 1:M
├── M:M
├── 1:1
└── Ternary

Normalization
│
├── 1NF → No Multivalued / Repeating / Composite
├── 2NF → No Partial Dependency
└── 3NF → No Transitive Dependency
```

---

## 📁 Practical Tasks

This repository also contains practical tasks covering:

* **ERD**
* **ERD Mapping**
* **Normalization**

Each task demonstrates the concepts covered in this summary.

### *Written with all my heart, in the hope of striving toward and reaching the goal someday. ❤*