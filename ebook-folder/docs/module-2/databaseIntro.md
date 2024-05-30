# Databases

*Keep steadily before you the fact that all true success depends at last upon yourself. —Theodore T. Hunger*

## Overview

We've spent the last few days learning how to use Express.js to build a server. But as you've probably picked up by now, holding our data in a static folder isn't ideal for large and dynamic apps. We need data to persist and allow multiple users to interact with the same set of data. To do this we need a third element added to our full-stack app: a database

Today we're going to learn what, how, and where to setup [databases](https://en.wikipedia.org/wiki/Database){:target="_blank"}.

<!-- ! Video Contents:  (width="655" height="368", ratio 1.77) -->
## What is A Database

A database is an organized set of data stored and accessed electronically. It helps provide a layer of persistence to our applications. That means, even if our application breaks or is shut down, we can still access its data. Next time the app starts up, it should be able to pick up where it left off.

We can integrate with our database in multiple ways. One of those ways is through our server built with Express. This is how our users will interact with our dataset. We can also use our terminals/command lines and various other visual tools to query this data from outside our application/server. This becomes very useful in debugging, for example.

There are many types of databases available to us but in this course we will focus on one of the most popular, [MySQL](https://www.mysql.com/){:target="_blank"}.

### MySQL

MySQL has many [interesting capabilities](https://www.pluralsight.com/blog/software-development/relational-non-relational-databases){:target="_blank"} including the ability to combine [NoSQL](https://en.wikipedia.org/wiki/NoSQL){:target="_blank"} and [SQL](https://en.wikipedia.org/wiki/SQL){:target="_blank"} (sometimes known as non-relational and relational, respectively) in a single database. We will be focusing on the SQL side of things. This means that all of our data will be structured in "tables" and those tables will have "relationships", hence relational. We will come to understand this more in the coming weeks. For now let's talk about the two types of operations we can perform on our databases, **read** and **write**.

#### Read vs Write

##### Read

A **read** operation means we are fetching or *reading* some data from the database. You can think of this like the GET requests we learned about previously. In MySQL, this manifests itself in the form of `SELECT` statements. We use that keyword (`select`) to retrieve a subset of data based on some criteria that we pass in.

##### Write

A **write** operation is something that *creates*, *updates* or *deletes* data. These could correspond to our **POST**, **PUT** and **DELETE** HTTP request types we've learned and built already. The MySQL keywords that represent these actions are: `INSERT`, `UPDATE`, `DELETE`.

#### How Data is Stored

When we create a database using some flavor of SQL, like mySQL we divided our types of data into **tables**. Using past examples we might have a `users` table and a `cars` table and a `products` table. All of these tables could be in the same database but keeping them in separate tables allows us to keep and organize related data within "categories".

In side the tables we divide our individual **entities** up by **fields**. If you were looking at an spreadsheet the **fields** would be the columns while the rows would be the **entities**. So each user in our `users` table would be an **entity** but their properties/attributes like `id`, `email`, `age`, `name`, `password`, etc... would all be **fields**.

The value in each of these fields of the user is called an **entry**. In the following **table** we see 5 **fields**, 3 **entities**, and 15 **entries**

| id | email | age | name | password |
| - | - | - | - | - |
| 001 | bob@email.com | 55 | Bob B | wonderful55 |
| 002 | sarah@email.com | 75 | Sarah F | turtleLove1955 |
| 003 | emily@email.com |  25 | Emily T | rainbowHearts33 |

  > Make sense?

#### SELECT Statements

Now that down, let's take a deeper look into `SELECT` statements. This will be our first foray into the world of MySQL.

`SELECT` is a keyword that we use when we want to query data from our database. Other keywords were mentioned above (`INSERT`, `UPDATE`) and it's important to note that these keywords are typically written in capital letters. Let's start with an example of `SELECT`:

```sql
SELECT * FROM adminAccounts
```

This query selects everything(*) from the `adminAccounts` table. Let's talk about what's going on here:

1. We are using `SELECT` to tell the database management system (**DBMS**) that we are querying/asking for data.
1. The asterisk , `*`, is known as a wildcard and its role is to include all **fields** in the query.
1. The keyword `FROM` exists in *all* `SELECT` statements and is a precursor to the final argument.
1. The final part/argument of this statement, the word `adminAccounts`, is the name of the **table** in the database that we are querying.

  > Think of `SELECT` as a function and you're passing it two arguments: `*`, and a function `FROM` which itself gets an argument, which in this case is `adminAccounts`. The following code is **NOT** valid!! But may help you start seeing the pattern:

```sql
*/ not valid mysql code
*/ used for illustrative purposes only

SELECT(*, FROM(adminAccounts))
```

**AGAIN, the code above is not valid but may help you see a pattern since you're familiar with JavaScript.**

Let's look at a more complicated example:

```sql
  SELECT SUM(logins) FROM adminAccounts WHERE firstName LIKE 'd%'
```

This query selects the sum of all the logins by users whose first name starts with the letter "d". Let's break it down once again:

1. We start with the `SELECT` keyword.
1. This time we use the `SUM` keyword combined with the field "logins" to get a total of all the logins.
1. We see `FROM` again to help us determine which table to query from.
1. Designate the `adminAccounts` table again.
1. Now we are going to use the `WHERE` keyword which helps us narrow our search to specific result sets.
1. We specify that we want to return only rows/**entities** where the first name starts with the letter `d`. That's what the `LIKE` keyword paired with `d%` does. The percentage sign, `%`, is a **wildcard**. The wildcard allows for anything to come after the `d` like *David, Dana, Devin, Deidre*, all of these would match and be returned.

Now we have two working examples of `SELECT` statements. Check out the full capabilities of `SELECT` statements [here](https://dev.mysql.com/doc/refman/5.6/en/select.html){:target="_blank"}.

## Additional Resources

- [ ] [YT, 365Science - 10 Min Intro to MySQL](https://www.youtube.com/watch?v=2bW3HuaAUcY){:target="_blank"}

## Know Your Docs

- [ ] [MySQL Docs - SELECT](https://dev.mysql.com/doc/refman/5.6/en/select.html){:target="_blank"}
