# Controllers

## Overview

**Controller** is just industry jargon for the files that hold the logic of our routes. The logic in those files is just plain JavaScript that uses Axios to fetch data. We create a folder called `controllers/` and then put files in it called `users.js`, `customers.js`, etc.

But first, why controllers?

### Why Controllers

After we create Routers it makes sense to create controller files so as to separate and organize our code even more. Just like we talked about having clean code and separation of responsibilities in the routers section, the same applies here. Since we've already covered routers, let's start there. Take a look at the following code (and keep in mind that it is pseudo-code, not all syntax is exact):

```javascript
  // users.js file

  router.get('/users', (req, res) => {
    const users = []
    if (req.body.query) {
      // go find users that match that query
      const users = await db.find(query)
    }
    if (!users.length) {
      // no users, throw error
      res.status(404).send('No users found')
    }
    res.json(users)
  })
```

What we are looking at here is the size of the function. You might think this looks perfectly reasonable and I would agree with you in this specific example, but if we had a function that was 100 lines long then suddenly this does not seem so reasonable. Just like we don't want 50 routes in one file, we also don't want multiple routes that are 50-100 lines long. It becomes hard to understand what each is supposed to do. This is where the concept of **controllers** comes in.

  > Again, a "controller" is not something specific to Express, it's just plain JavaScript we happen to call **controller**.

## Creating a Controller

Let's create a folder called `controllers/` and another file inside it called `users.js`.

Our file structure will now start to look like this:

```console
src/
  - index.js
  - controllers/
    - users.js
  - routers/
    - users.js
    - customers.js
    - merchants.js
    - admins.js
```

Now, in `controllers/users.js` we are going to take the code we saw above and put it in it's own function (to be exported):

```javascript
  // controllers/users.js file

  const findWithQuery = () => {
    const users = []
    if (req.body.query) {
      // go find users that match that query
      const users = await db.find(query)
    }
    if (!users.length) {
      // no users, throw error
      res.status(404).send('No users found')
    }
    res.json(users)
  }

  // exports each of the functions/methods we build as an object
  module.exports = {
    findWithQuery
    // other methods could be listed here with a ',' after each.
  }
```

In this way we create a `findWithQuery` method on the users controller object we can call and use later with dot-notation. (You'll see in the next example.)

Go back into our router (`routers/users.js`) and import the above controller so that the function/**method** can be used in the router.

```javascript
  // routers/users.js file

  const UsersController = require('../controllers/users.js')

  router.get('/users', UsersController.findWithQuery)
```

Look how much simpler that route is! Every time `"/users"` is hit, the attached function will be called. This is what we are looking for. As we mentioned previously, we will have controllers for all types of routes, so as our application grows so will our use of our "controllers" directory, which will look like this eventually:

```console
- controllers/
  - users.js
  - customers.js
  - merchants.js
  - admin.js
```

## Additional Resources

- [ ] [YT, Academind - Adding Controllers](https://youtu.be/ucuNgSOFDZ0){:target="_blank"}
- [ ] Look ahead to the [Questions for Student Led Discussion](./../additionalResources/questionsForDiscussion/qfd-class-4.md)

## Know Your Docs

- [ ] [MDN Docs - Express Routes](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/routes){:target="_blank"}

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