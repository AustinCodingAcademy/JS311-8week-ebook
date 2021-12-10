# Data Modeling with ER Diagrams

*Strong lives are motivated by dynamic purposes. —Kenneth Hildebrand*

## Overview

At this point we have most of the knowledge needed for creating APIs(servers). We've practiced this numerous times and you should be getting familiar with the process. Now we're going to take a break and take a deeper dive into the **Entity Relationship Diagrams** (ERD) we first looked at last week.

## Why Use Data Modeling?

Data modeling is the process of creating a model that represents the relationships between the different types of data in your database. The data model emphasizes what data is needed and how it should be organized in a visual manner. In a nutshell, we want to make sure all (*or most*) of our data objects are accurately represented well before we write any code! This will save some headaches down the road.

One of the most common ways to do this is through the use of an **ERD** (Entity Relationship Diagram).

You may be thinking to yourself, "Greaaat...but why would I do this?" Here's a couple reasons why to use a data model. Using data models are much easier than changing your real database. It's a lot easier to build a data map than writing SQL queries to change your database. Being able to quickly change, and see the changes in a data model will help keep your new database from becoming disorganized, or incorrect. When creating a database it's easier for you to review a data model than review a a database design. In most cases it is harder to describe a database to your someone than simply showing them a model that represents the database. These data models help improve organization and communication within your team.

A good way to visualize why we do this is by imagining a company entity that owns several dental schools; one in Houston, one in Austin, and one in Dallas. Each of these schools would have similar **properties** to one another but would obviously have different **values**, i.e. they would each have `school_name`, `street_address`, `campus_director`, `phone_number`, `website_URL`, `email`, etc.
 This way we could create a `school` table that would hold each of these schools together as similar data:

=== "School Entity Table "

    | `school_id` | `school_name` | `street_address` | `campus_director` | `phone_number` | `website_URL` | `email` | `school_id` |
    | `001` | - | - | - | - | - | - |
    | `002` | `Austin Dental School` | `123 Main Street` | `058` | `555-123-5520` | `waterloodental.us` | `waterloodental@email.com` |
    | `003` | `Dallas Dental School` | `123 Main Avenue` | `091` | `555-123-2250` | `dfwdental.us` | `dfwdental@email.com` |
    | `004` | `Houston Dental School` | `123 Main Boulevard` | `014` | `555-123-0025` | `htowndental.us` | `htowndental@email.com` |

Then each of the `employee`s that worked at these schools would have different **properties** from the schools but the same **properties** to each other with different **values**. For this reason they would go into a different table:

=== "Employee Entity Table"

  | `employee_id` | `first_name` | `last_name` | `phone_number` | `address` | `email` |
  | - | - | - | - | - | - |
  | `014` | `Alice` | `Walker` | `555-9963` | `900 Finney Street` | `alice@email.com` |
  | `058` | `Lena` | `Heady` | `555-6399` | `900 Comal Street` | `lena@email.com` |
  | `091` | `James` | `Dean` | `555-3699` | `900 Commerce Street` | `james@email.com` |
  | `011` | `Edward` | `Newton` | `555-6936` | `900 Flat Street` | `edward@email.com` |

Notice the `campus_director` property on the School Entity Table. Do you see how it's just a number? This number would relate to an employee in the Employee Entity Table. Since our `employee_id_` property will never changes and will always represent a single employee we can use this property in  other tables to *relate* the pieces of data without having to duplicate the information in both tables. We can have the `employee_id_` in the schools's table and then use it again in our Payroll Table, for example, to maximize efficiency. When creating our data models we want to always be thinking about maximizing the re-use of our properties. Take the time to think about all the individual relationships each entity and property can have for your final project's.

  > NOTE: `employee_id` is an example of a **primary key** (PK) and will follow strict rules to be considered a **PK**. It will never change and can only be assigned to one person. Since it follows these rules we can re-use this throughout our database.

  > NOTE 2: Generally, `id`s are created one at a time in ascending order with each new entity entry. This is default and automatic in mySQL.

*****

## UML Notation

Entity Relationship Diagrams are written in **[UML Notation](https://www.tutorialspoint.com/uml/uml_basic_notations.htm)** to visualize the relationships between tables. **UML** stands for **Unified Modeling Language** and it is basically the go-to for designing object-oriented systems.

Remember our ER Diagram from Week 3 . . .

![er-diagram-example](./../images/er-diagram-example.png)

### Fields & Entities

*In short: each row is an **entity** and each column is a **field**.*

In the diagram above, the rectangles with our **table** names on them `usersContact` are called **entities**. It's just an object that represents some type of data. The table, once saved in the database would accept and store multiple entities with these **fields** (properties) on them.

  > NOTE: Remember, tables are made of rows and columns. In a SQL table, each entry (**entity**) is a row. And each column is a **field** (property/attribute) of the entity. The cells would represent the values stored in each field on each entity.

Inside of the entity we see the **attributes** that correspond to our tables. Those are the **field**/column names and there may be symbols next to those fields. In fact, there is generally a symbol there that gives us some information about the field's responsibility. If it has a key icon, for example, that indicates that the field is the **primary key**(PK). You can see a [list of other field icons here](https://stackoverflow.com/questions/10778561/what-do-the-mysql-workbench-column-icons-mean).

Here's another diagram to look at. Notice the icons on these tables.

![er-diagram-example-icon-highlighting](./../images/er-diagram-example-icon-highlighting.png)

### Cardinality

The last thing we need to talk about in order to understand our ER diagrams is **cardinality**. Cardinality refers to the type of relationships that we maintain between our entities. These types of relationships are how we can enforce data integrity throughout our database. For example, I can't assign a `userId` on a child table like usersContacts to an `id` that DOESN'T EXIST on the parent table users. But what cardinality is really talking about is the maximum or minimum number of relationships that can be maintained between two entities. For example, a `user` can have multiple `userContacts` but only one `usersAddress`.

These relationships are usually described as **"one-to-many"**, **"one-to-one"**, or **"many-to-many"**. The lines between the entities and the small notations at the end of them dictate these relationships.

![cardinality-notation-table](./../images/cardinality-notation-table.png)

*****

## Relationships Explained

- [ ] **One-to-One**: This relationship can be summed up as one table to another table allowing only one connection each. Such as a User table having a One-to-One relationship for a drivers license table. The user can only have one drivers license so it would be applicable to use the One-to-One relationship.

- [ ] **One-to-Many**: An example of a One-to-Many relationship would be a Users table and an Orders table. The User can have as many Orders as they want but each Order could only have one User; using a One-to-Many relationship would work perfectly.

- [ ] **Many-to-One**: this can be understood as the opposite of the previous. Let's say we have a Bank Account table & a Users table. Each User could have many Bank Accounts but each Back Account would have only one User.

- [ ] **Many-to-Many**: An example of this would be a Course table to a Student table. Each Course can have many students and each Student can have many Courses.

### Entity Relationships Further Explained

Let's look at the data from the `employees` database above:  

- [ ] Follow the line between the `employees` table to the `salaries` table. Starting at the `employees` table we see a double hash mark, this means that the relationship an entity in the `employees` table can have **one and only one** relationship with what ever table its connected to on this line.
- [ ] at the other end of that line connected to the `salaries` table we see a trident and a hash mark. This means that each entity in this table can have one or many relationships with entities in the table it's connected to.
- [ ] Summary: Each employee can have one and only one salary. But a salary amount could be given to one or, even, all of the employees.
- [ ] Going further, looking at the `salaries` table we can see that there are `from_date` and `to_date` fields. So it looks like that table holds a history of each salary an employee has had over the course of some time.

Are we starting to understand how to read these? You can see more cardinality symbols on the [bottom of this page](https://www.lucidchart.com/pages/ER-diagram-symbols-and-meaning).

To further illustrate, take a look at the `departments` entity. Notice the double hash and trident lines? This shows that each `department` can have only one `title` but multiple `dept_emp` (department employees).

## Determining Our Data Model

Most of the information above assumes you already have a working database, or at least a couple tables. We've talked about how to read/interpret our diagrams and in our homework assignment today we will work on creating an ER diagram, but let's take a second to talk about modeling the data that these diagrams come from.

  > NOTE: data modeling is a broad subject. We will discuss only what's most important for us at this level.

Let's now assume that we are starting completely from scratch. We do not have a database set up at this point but we know we are going to use MySQL. We will want to take the following actions:

1. **Understand the company's industry**
  We need to know what we are building. Having an understanding of our business model will help us determine what our entities will be.

1. **Identify our entities**
  What tables do we think we will need to create? If I am in the eCommerce space I will probably want a table called `customers`.

1. **Identify our attributes**
  Now that we have our tables it's time to determine what fields should exist on those tables. Every "customer" should definitely have an `id`, but what else? We might want to know the customers' first and last names and probably some contact information.

1. **Identify our relationships**
  We have a "customers" table and because we know that customers will place orders, we've also gone ahead and created an "orders" table. Each table has its own set of attributes but how are they related? What's the cardinality? Well . . . if we assume that any customer can have multiple orders (that would make sense, right?) then we know that we have established a "one-to-many" relationship.

This is the thought process you will go through as you develop MySQL databases on your own. It may seem simple or it may seem complicated but data modeling is an important part of the development process and a good skill to have. Always begin by drawing it out on paper so you have a good visual understanding of your database's needs.

## Practice It

![lucid-chart-erd-example](./../images/lucid-chart-erd-example.png)

- [ ] Re-create the above diagram on [Draw.io](https://www.draw.io/)
- [ ] Find the elements you need under the "Entity Relation" tab on the left toolbar
  
  > Hint: You can use an SQL statement to have the app automatically create the entities (tables) for you . . .

## Additional Resources

- [ ] [YT, LucidChart - ERD Tutorial pt. 2](https://youtu.be/-CuY5ADwn24)
- [ ] [Article, TutorialsPoint - UML Notation](https://www.tutorialspoint.com/uml/uml_basic_notations.htm)
<!-- - [ ] [YT, tuber - title]() -->

## Know Your Docs

- [ ] [LucidCharts Docs - ER Diagrams](https://www.lucidchart.com/pages/er-diagrams)
- [ ] [LucidCharts - ERD Symbols](https://www.lucidchart.com/pages/ER-diagram-symbols-and-meaning)
- [ ] [Forum, StackOverflow - Column Icon Meanings](https://stackoverflow.com/questions/10778561/what-do-the-mysql-workbench-column-icons-mean)
