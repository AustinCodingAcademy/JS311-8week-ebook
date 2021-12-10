# Advanced SELECT

*The thing always happens that you really believe in; and the belief in a thing makes it happen. —Frank Loyd Wright*

## Overview

Last class we set up a database, connected our Workbench Tool to it and learned how we can run some simple queries to retrieve the data we want. That's a huge step and we should be very proud of that! We're quickly learning how to become a "back-end" developer.

Today we are going to build on that knowledge and talk about data relationships and how they can help us achieve even more impressive results. We will learn more about **tables**, **rows**(**entities**) as well as the **keys** that help form relationships between them, hence **relational database**. We will end with more advanced `SELECT` statements that `JOIN` tables together to achieve more complex results.

We're going to discuss a few topics today and then end with practice `JOIN`ing tables together. So first we need to understand how relationships work between our data.

## Tables/Rows

We saw this in our last lesson but didn't touch on it in too much detail. Basically, all of the data we store in our database will exist in **tables**. Tables are logical groupings of data based on shared characteristics. For example, all users (in our last example) had a `first_name`, `last_name`, `address`, etc. The same would be true for cars or products, we would put them in their own table because the share similar characteristics or properties. These "properties", known as **fields** are the columns of the table and the rows are each individual **entity** within our **dataset**. Remember this table from last lesson?

| id | email | age | first_name | password |
| - | - | - | - | - |
| 001 | bob@email.com | 55 | Bob B | wonderful55 |
| 002 | sarah@email.com | 75 | Sarah F | turtleLove1955 |
| 003 | emily@email.com |  25 | Emily T | rainbowHearts33 |

The value in each of these cells of the user is called an **entry**. In the **table** above we see 5 **fields**, 3 **entities**, and 15 **entries**

The rows, or **entities** represent each item in our table. For example, there is one row for each "user". When we query our data we are looking to return the rows that match our criteria. In the "users" example we may look for each row ("user") that has a `first_name ` that starts with `S`.

```sql
  SELECT * FROM users WHERE first_name LIKE 'S%'
```

  > This query would return all the fields of user 002: `| 002 | sarah@email.com | 75 | Sarah F | turtleLove1955 |` because their `first_name` begins with an `S`.

How do we know how many rows exist in my table? Try running the following SQL command:

```sql
  SELECT COUNT(*) FROM users
```
  
  > If you do this on the "users" table from last class you should see the number 500.

  > NOTE: MySQL has many commands built into the language and all you have to do is read them, play with them, and move them into your server's codebase when you build the query that returns what you're looking for. That's why we use MySQL Workbench!!

## Keys

**Keys** are indexes in MySQL, just like indexes in JavaScript Arrays. What does that mean? Well . . . it's simply the way in which MySQL works to organize data. There are three types of keys that we need to be concerned with. They are **primary**, **unique** and **foreign**.

### Primary Key

A **primary key** is a **field** that identifies each row in the table. **It could technically be a group of columns but we won't talk about that now as that technique is out of fashion** What we need to remember is the three rules of **primary keys**:

  1. It must be **unique** to each row;
  2. and cannot be `null`.
  3. Also, these keys are almost always numbers, not strings, since MySQL naturally works faster with numbers and speed will eventually be a concern if we have a big dataset.
  
In many cases, the **primary key** is an `auto-increment`ing number like 1, 2, 3, 4, etc. or like the table above: `001`, `002`, `003`, and so forth.

  > It's important to note: a table can only have one **primary key**.

### Unique Key

A **unique key** enforces uniqueness on specific columns of your data. There can be many unique keys on a table. An easy example of this will be referencing our "users" data again. Let's say that we have a bunch of user data but no two users should have the same email address. In this case we have to place a `unique key` on the `email` column and MySQL will prevent us from inserting duplicates.

### Foreign Key

**Foreign keys** help us manage the relationship between tables. These fields have the same meaning in different tables and help us reduce redundancy. Let's say our "users" data is split up into two tables. One is called "users" and one is called "userContacts". 

| users table |
| id | first_name |
| - | - |
| 001 | emily |
| 002 | erica |
| 003 | beverly|

| usersContacts table |
| user_id | email | street_address | phone
| - | - | - | - |
| 001 | emily@email.com | 123 Michigan Street | 555-555-5555 |
| 002 | erica@email.com | 34 Miracle Street | 555-555-5555 |
| 003 | beverly@email.com | 123 Magic Street | 555-555-5555 |


The first table contains users `id`s and `first_name`s and the second contains their `phone` numbers and `email` & `street_addresses`. We would  put the user `id` on the "usersContacts" table as a foreign key which helps relate that data to the first table ("users"). It also prevents us from adding to "usersContacts" without first adding to "users" since we would want to avoid an **orphaned record** in "usersContacts" that has no "user". Foreign keys are also used frequently to `JOIN` tables. A more [visual example might help](https://logicalread.com/mysql-foreign-keys-mc13/#.XQESlNNKh24) here.

  > Note: Foreign keys are the most difficult to understand so don't worry if you can't visualize it in your mind just yet. The practice and homework will help enforce this principle

### JOIN

Ok, we've done all the hard work of getting our tables set up with the appropriate keys and you're scratching your head because it only partially makes sense(*or none at all...*). That's fine. Here comes the fun part (*hopefully*)! If you had fun understanding `SELECT` and realizing how powerful it is to perform queries, just wait. Now we are going to start combining tables together.

Because we've used foreign keys to form relationships between our data, we can now `SELECT` data from multiple tables that meets our criteria. Check this out:

```sql
  SELECT
    users.first_name,
    usersContact.email
  FROM users
  JOIN usersContact
  WHERE
      users.id = usersContact.user_id;
```

So what's going on here? `first_name` only exists on the users table and `email` only exists on the `usersContact` table but because we've created a relationship between the two tables (via the **foreign_key**, `user_id` on the "usersContact" table) we can now `SELECT` data from both and know that we are guaranteed to have a usersContact for each "user".

### Why split the data?

You might be asking yourself: "Why did we take the original 'users' table and split the data into two tables?" There are a few answers to this including **normalization** but what I'd like to touch on here is business impact. We might want to get a list of all user emails in the system. But we don't necessarily care what the users names or addresses are we just want to email everyone something. In this case it's beneficial to our system that we don't have to retrieve unnecessary information. The dataset would be a lot larger with all the additional fields included. Also, it might be possible for a user to have multiple contacts (phones, emails). If that's the case it's great that the data is split up so that we can just create a new entry in the "usersContact" table and not have to create a whole new user entirely. We'll take a look at our new data in the homework.

Check out the [Addition Resources](#addition-resources)!

### Practice It - JOIN

- [ ] Follow the link to [open this DBfiddle](https://www.db-fiddle.com/f/4FrW3HufzsNq74KAbSpnpn/1)
- [ ] Alter the SQL fiddle:
    * [ ] In the schema SQL, change the "firstName" column to be "seller" instead (*There are two instances to find and change*).
    * [ ] Change your Query SQL to ask for the correct field name "seller"
    * [ ] Move the price to be before the items' names and descriptions in the query return.

## GROUP BY

The `GROUP BY` statement does pretty much what its name implies. It allows us to group data by a certain criteria. The caveat is that you can only display the fields that appear in the `GROUP BY` clause when you are viewing the data. That is, unless we specify an aggregate function such as COUNT or SUM for the rest of the data. It's very common to use COUNT with `GROUP BY` so let's see an example:

```sql
  SELECT
    county,
    count(*)
  FROM
    users
  GROUP BY county;
```

The above will display a list of all the counties and a count of the users in each one. If we try to add an additional field into the select, such as "phone1" we get:

```sql
SELECT
  county,
  phone1
  count(*)
FROM
  users
GROUP BY county;
```

```console
Error Code: 1055. Expression #2 of SELECT list is not in GROUP BY clause and contains non-aggregated column 'admin.users.phone1' which is not functionally dependent on columns in GROUP BY clause; this is incompatible with sql_mode=only_full_group_by
```

That is because there are multiple options for "phone1" and SQL doesn't know how to group them as we haven't specified that. We could sum the phone numbers (`SUM(phone1)`) and that would work but it would show us useless information. Why would we ever want the "sum" of a phone number?

### HAVING

The `HAVING` clause is a lot easier. It's basically a `WHERE` clause for the `GROUP BY`. It allows us to display only aggregated information that matches our criteria. For example, show me a list of all the counties and the number of users who live in each one, but only if there are more than 5 users in it. We would write that like this:

```sql
  SELECT
    county,
    count(*) AS tally
  FROM
    users
  GROUP BY county
  HAVING tally > 5;
```

You may notice the word `tally` in there. We've simply renamed the `count(*)` field to "tally" so that we don't have to keep specifying it in the previous manner. Now this query will show me all counties where the tally is greater than 5.

We will practice with this more in the upcoming project. Be sure to read ahead, read the docs below, and answer the Questions for Discussion for yourself before class.

## Additional Resources

- [ ] [YT, theNewBoston - MySQL 22: How to JOIN Tables](https://youtu.be/6BfofgkrI3Y)

## Know Your Docs

- [ ] [MySQL Tutorial - Primary Key](http://www.mysqltutorial.org/mysql-primary-key/)
- [ ] [MySQL Tutorial - Unique Key](http://www.mysqltutorial.org/mysql-unique/)
- [ ] [Arcticle, LogicalRead - Foreign Key](https://logicalread.com/mysql-foreign-keys-mc13/#.XQESlNNKh24)
