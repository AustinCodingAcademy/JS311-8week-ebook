# The SQL CRUD Commands

*Nothing contributes so much to tranquilize the mind as a steady purpose—a point on which the soul may fix its intellectual eye. —Mary Shelley*

## Overview

Last week we learned a lot about databases and SQL. We used SELECT to query data in a lot of different ways and we understand how tables provide relationships to our data. Today we are going to learn about the rest of the CRUD operations in SQL.
<!-- ! Video Contents:  (width="655" height="368", ratio 1.77) -->

Reminder: CRUD is an acronym that stands for:

**C**reate, **R**ead, **U**pdate, **D**elete

These are the basic operations we use to obtain and mutate (change) data. You'll hear this acronym used to reference APIs and, most frequently, database operations. You'll hear often that at the end of your course and by graduation you will have built a full-stack CRUD app.

In terms of CRUD, we've already learned the "R" (read/`SELECT`). Now we will learn about `INSERT`/Create, `UPDATE` and `DELETE`. These operations will give us full control of our datasets.

### INSERT

The `INSERT` command inserts an item (or a group of items) into the specified table. You can see bulk inserts in the `initialize.sql` file of your previous two homework assignments. An `INSERT` statement looks like this:

```sql
  INSERT INTO users
      (firstName, lastName, age)
  VALUES
      ('matt', 'miller', 35);
```

  > Notice how the values match up (in order) with the names of the fields.

| id | firstName | lastName | age |
| - | - | - | - |
| 1 | bob | brandy | 55 |
| 2 | sarah | sassafrass | 75
| 3 | emily | erlanger | 25

Question: There's an "id" field on this table that we don't see in the `INSERT` command. Why doesn't the "id" field need to be written in the `INSERT` statement?

  > Check out/Google the [AUTO_INCREMENT keyword](https://www.w3schools.com/sql/sql_autoincrement.asp){:target="_blank"} for the answer to this question.

### UPDATE

The `UPDATE` command updates a row or set of rows that match a certain criteria. You can change one or more fields in the dataset as long as they aren't `PRIMARY KEYS`.

```sql
  UPDATE
      users
  SET
      first_name = 'Artie'
  WHERE
      id = 3;
```

The statement above changes (SETs) the first name of user 3 to "Artie": `Artie erlanger`.

### DELETE

The `DELETE` command removes a row or group of rows that match a certain condition. It's important to be careful with the `DELETE` command because you could inadvertently remove too many rows if you aren't specific with your `WHERE` clause. When that happens there's no getting that data back, short of a DB backup, and that can be time consuming and also assumes that you backed up your database in the first place. That being said, a `DELETE` command looks like this:

```sql
  DELETE FROM
    users
  WHERE
    id = 3;
```

The statement above `DELETE`s the user from the users table whose (`WHERE`) `id` is equal to `3`.

What if you wanted to `DELETE` multiple users by `id`:

```sql
  DELETE FROM
    users
  WHERE
    id IN (3, 4, 5);
```

That's great! Users 3, 4 and 5 have been deleted. Notice how the `IN()` looks like a function? You can pass multiple parameters to it.

But our deletions are not limited to removing records by their `id`s. Everything we can do with the `WHERE` clause in `SELECT` applies to `DELETE`.

```sql
  DELETE FROM
    users
  WHERE
    firstName LIKE 'a%';
```

The above query deletes **all** users from the database whose first name starts with the letter 'a'. Hopefully we are starting to see how this can become dangerous. **Don't attempt to run queries like this in a production environment. Instead, we would look to see if there is more specific criteria we could use.**

## Practice It - SQL CRUD

- [ ] Follow the link to [open this fiddle](https://www.db-fiddle.com/f/8U1SS2zVjsz9VmjciqJ2Hx/0){:target="_blank"}
- [ ] Work through the `INSERT`, `UPDATE` & `DELETE` statements provided
- [ ] Run each statement one at a time, leaving the others commented out
- [ ] Observe the results
- [ ] Get creative and try some SQL CRUD of your own, altering the statements to your liking
- [ ] Be sure to `INSERT` new data so that you can play longer.

## Additional Resources

- [ ] [YT, the Bad Tutorials - SQL Tutorial 12: Inserting Data into Tables](https://youtu.be/Tet3Z7Yb2gg){:target="_blank"}
- [ ] [YT, the Bad Tutorials - SQL Tutorial 11: UPDATE](https://youtu.be/lyqeLvtlQiA){:target="_blank"}
- [ ] [YT, the Bad Tutorials - SQL Tutorial 22: DELETE](https://youtu.be/iHfDrczm0cU){:target="_blank"}
<!-- - [ ] [YT, tuber - title]() -->

## Know Your Docs

- [ ] [MySQL Docs - INSERT](https://dev.mysql.com/doc/refman/8.0/en/insert.html){:target="_blank"}
- [ ] [MySQL Docs - UPDATE](https://dev.mysql.com/doc/refman/8.0/en/update.html){:target="_blank"}
- [ ] [MySQL Docs - DELETE](https://dev.mysql.com/doc/refman/8.0/en/delete.html){:target="_blank"}
- [ ] [W3S Docs - AUTO INCREMENT](https://www.w3schools.com/sql/sql_autoincrement.asp){:target="_blank"}
- [ ] [W3S Docs - SQL](https://www.w3schools.com/sql/){:target="_blank"}

<!-- ! END OF VIDEO 101.1.3.1 - TITLE-->
<!-- ? Video Numbering and Title system: CourseNumber.ModuleNumber.LessonNumber.VideoNumber -->
<!-- * (VIDEO 101.2.4.3 - "CSS Selectors") === 101 Course, Module 2, Lesson 4, Video 3 - "CSS Selectors" -->

<!-- 

cp workspace/resources/templateFile.md docs/module- 

```javascript

```

| Method      | Description                          |
| ----------- | ------------------------------------ |
| `GET`       | Fetch resource                       |
| `PUT`       | Update resource |
| `DELETE`    | Delete resource |


    `line numbers`
:do you like 'em?


++slash++
https://facelessuser.github.io/pymdown-extensions/extensions/keys/

=== "Javascript"

    ```javascript
    ```

=== "Python"

  ```python
  ```

=== "Example"
    ```console
      .
    ```

=== "Instructions"
    ```markdown
      .
    ```

=== "Result"
    ![PIC](./../images/pic.png)
-->