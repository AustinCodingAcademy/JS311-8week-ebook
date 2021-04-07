# Express Controllers

*If you want to succeed in the world you must make your own opportunities as you go on. The man who waits for some seventh wave to toss him on dry land will find that the seventh wave is a long time a-coming. You can commit no greater folly than to sit by the road side until some one comes along and invites you to ride with him to wealth or influence. —John B. Gough*

## Overview

We recently learned about Express and created our first web server. In doing so we learned about routes and how they intercept various types of requests like PUT, POST, GET...etc. We also understand **paths** and **callbacks function** with the parameters `req` and `res`.

<!-- ? TODO cover body-parser? -->
In the last project we were putting all of the logic to get data inside the same file: `index.js`. This technique works and can be used but for large applications, aka, the ones you'll be working on after you graduate, you'll notice there's a different pattern implemented. Instead of keeping the data retrieving logic in the `index.js` file we'll separate it from the routes (`app.get()` ...etc. into a different file and then import that logic into the `index.js` file and call it when the route is called.

In short, we're going to move the parameters (**path** and the **callback function**) into a separate file called **router**.js, then move the **callback function** into a different file called **controller**.js. After that we'll import the logic of the **controller** into the **router**, give it to the appropriate route then import the **router** into the `index.js` file and assign it to the correct method! READY?

  > Try to understand the three files below before moving on. Hint, its not doing anything different than what you've already done; but now, it's separated into 3 different files.

=== "src/index.js"

    ```javascript
      const express = require('express')
      // import the router object and save to a variable called `router`
      const router = require('./routers/')
      const app = express()

      app.use(router.getUsers)

      // ...more code here...blah...blah...app.listen()
    ```

=== "src/router.js"

    ```javascript
      const express = require('express')
      // save the functionality of Express's `router` as a variable called `router`
      const router = express.Router()
      // import the exposed object in `controller.js` and save it to a variable
      const controller = require('./controller.js')

      // define the logic associated with '/users'` as the method: getAllUsers
      router.getUsers('/users', controller.getAllUsers)

      // make the router object available globally to the rest of the app
      module.export = router
    ```

=== "src/controller.js"

    ```javascript
      const getAllUsers = (req, res) => {
          // perform some logic to get user from the database
          res.json(users)
        }
    
      // make the function available globally as a property on this anonymous object
      module.exports = {
        getAllUsers
      }
    ```

  > IMPORTANT: Make sense of this code before moving on. Draw it so you have a visual guide as you learn how to implement this.

## Why Routers and Controllers

Imagine that we have an Express app that has 50 routes in it. Where would you put them all? So far, it has just been our `index.js` (sometimes called `server.js`) file, but is that really sustainable or scalable? Let's see:

```javascript
  // index.js file

  const express = require('express')
  const app = express()

  const port = process.env.PORT || 4000

  app.get('/users', (req, res) => {
    // perform some logic
    res.json(users)
  })

  app.get('/users/:id', (req, res) => {
    // perform some logic
    res.json(user)
  })

  app.post('/users', (req, res) => {
    // perform some logic
    res.send('success')
  })

  // Add in 47 other routes here......
  // .........line 489................
  // ................You get the idea.

  app.listen(port, () =>
    console.log(`Example app listening on port ${port}!`))
```

Just think about how long this file would be! Fortunately, we have ways to get around that, which is where `routers` come in.

## Creating A Router

A "router" is a functionality that is included in Express to make the above process easier for us to organize. Here's how it works. You:

- [ ] Create a new file (ex. `users.js`)
- [ ] Create a new router (this will handle all users routers)
- [ ] Export the router
- [ ] Import the router into `index.js`
- [ ] `.use()` it as middleware (like `body-parser`)
- [ ] Let's see an example:

To keep it organized from the get go we'll make two folder first: `routers/` and `controllers/` In these two folders we'll keep their respective files: `users.js` and `userController.js`...so forth and so forth.

For now, let's create a new folder called `routers` and a file in it called `users.js` and copy/paste the following into it:

```javascript
  // src/routers/users.js
  const express = require('express')
  const router = express.Router()

  // Now we simply use our "router" just like our "app" to create routes.

  router.get('/users', (req, res) => {
    // perform some logic
    res.json(users)
  })

  router.get('/users/:id', (req, res) => {
    // perform some logic
    res.json(user)
  })

  router.post('/users', (req, res) => {
    // perform some logic
    res.send('success')
  })

  // And then we export the router:

  module.exports = router
```

Now . . . we head back to `index.js` and we require this `router`: `const users = require('./users')`

Finally, we use it as middleware like this: `app.use(users)` where "users" is the parameter we just imported above. So now our `index.js` file looks like this:

```javascript
  // src/index.js file
  const express = require('express')
  const users = require('./routers/users')
  const app = express()

  const port = process.env.PORT || 4000

  app.use(users)

  app.listen(port, () =>
    console.log(`Example app listening on port ${port}!`))
```

This now works just as before except we don't have 50 routes defined in our `index.js` file. After we created routes for our other resources we might have a file that looks like this:

```javascript
  // src/index.js file
  //...more code here...

  app.use(users)
  app.use(customers)
  app.use(merchants)
  app.use(admin)

  //...more code here
```

And those routes would all exist in their corresponding files: `routers/customers.js`, `routers/merchants.js`, `routers/admin.js`.

Hopefully we can see how using routers allows us to write cleaner code in our `index.js` file as well as separate the responsibilities of our routes to keep the working parts of our app organized and easily accessible.

## Additional Resources

- [ ] [YT, Hungry Turtle Code - How to Use Express Router](https://youtu.be/paNikhYqdz0)

## Know Your Docs

- [ ] [Express Docs - Routing](https://expressjs.com/en/guide/routing.html)