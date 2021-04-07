# Intro to Express

*There is only one definition of success—to be able to spend your life in your own way. —Christopher Morley*

## Overview

Recently we've re-familiarized ourselves with Node and NPM and developed an understanding of axios as an alternative to fetch. We've also practiced consuming APIs with both Postman and Axios. So far, the APIs we've interacted with are programs that someone else has built. With Express, we will start to understand how to build our own APIs.

## What is Express.js

Express is a (very popular) NPM package that turns our Node.js applications into a web server. Express can help us serve static files (images, etc) or create routes to build API endpoints. We will use Express to build the "backend" of our application.

Why do we need a web server (or backend), anyway? There are several reasons. One key reason is for the protection of sensitive content. On our front-ends (HTML, CSS, JavaScript, React), everything we code into the app will be visible from the browser in one way or another. That means that if you store an API key or some other sensitive token in a variable, eventually someone will be able to inspect the website (through the console) and obtain that information. This inspection is not possible with a web server built with Express. Another reason we use a server is that it is how we integrate with a database. We will become more familiar with databases in the following chapters but it's good to know that in the software industry (as a best practice) we don't connect to a database directly from the frontend, a React app for example. Most database systems don't even allow this interaction. So a web server helps us account for this as well.

Express is an amazing tool that helps us quickly accomplish these tasks. Fortunately for us, there is a wealth of information available on Express and we will see some of that soon. For now, feel free to check out the [Express Homepage](https://expressjs.com/).

A breakdown of concepts:

### Initiating the Server

The first thing we typically do after we import express is to instantiate the server. The first few lines of our server usually look like this:

```javascript
// index.js
// import the Express package
const express = require('express')

// create a variable to hold the value of all of the server's functions/methods
const app = express()

// Middleware: this block is where authorization logic goes. We're not going to worry about it too much right now. We'll get into the details of authorization in a few weeks.
app.use((req, res, next) => {
  //authorization logic would go here, after the check it calls the next() method to all the request to go to the next phase: get, put, post, etc...
  next()
})

// at the bottom of the index.js file you'll tell the server `app` to listen give you feed back in the console when it is.
// use this method to give you feedback as to when the server is successfully spun up (up and running)!
app.listen(8080, () => {
  console.log('Server is listening on port 8080.')
})
```

  > If this was in an `npm init`ed folder with Express installed (`npm i express`) you could run `npm start` or `node index.js` and get `'Server is listening on port 8080.'` on your console.

### Creating Routes

After that we are free to start creating **routes**. The `app` object has properties on it already that include: `.get`, `.put`, `.post` and `.delete` (among others). These properties correspond to the HTTP request methods you learned about in 101, 211, and now in 311.

  > [Remember when we used `fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch), the default request method was `get` so when we wanted to post form data we had to write the attribute `method="POST"`
  > NOTE: in this use of the word *method* we mean something different than when we say an object's *method*. The method of `fetch` refers to the type of HTTP Request that will be sent.
  > In our Express app we'll define *methods* on the `app` object that will act as routes to handle these types of/*method*ical requests. Whew...moving on...

So, while we're building our server we have to think about the potential requests types that may & will come to it from our front-end or some other developer using our API. They'll be sending POST types, GET types, PUTs and DELETEs. To design and build for those types of requests we use these built in methods: `.get`, `.put`, `.post` and `.delete` (that correspond to those types of request), by simply defining their value with the functionality we want them to do.

To start doing this we begin writing them like this:

```javascript
  // index.js
  const express = require('express')

  const app = express()

  app.use((req, res, next) => {
    next()
  })

  // the GET Method
  app.get()

  // the POST Method
  app.post()

  // the PUT Method
  app.put()

  // the DELETE Method
  app.delete()

  app.listen(8080, () => {
    console.log('Server is listening on port 8080.')
  })
```

To continue defining the functionality of these methods we'll be putting some parameters inside each of these...

### The 1st Argument: the Path

The path is a string that determines what route should be used. For example, all of our data will come through this one server so it needs to be pass through one **root** path: `"http://localhost:4000/"`. But if we wanted to serve user data and car data we'd need to define them at different paths. To do this we'd say that cars are at `"http://localhost:4000/cars"` and users are at `"http://localhost:4000/users"`.

Therefore the **path** is `"/cars"` or `"/users"`. To define them you'd write it like this:

```javascript
  `app.get('/cars')`
  `app.get('/users')`
```

We only need to define the last segment of the path: `/users` or `/cars` because our server lives at `https://localhost:4000/`. Once our request from either Postman or our front-end app finds the server at the URL: `https://localhost:4000/`, (*or any other URL it sits on once we host it remotely*), the path tells Express where to direct the request so that it finds the right route to get the expected resource (cars or users).

  > if you look at the APIs we've worked with in 101 and 211 you'll see this same pattern used in those servers...`/posts/`, `/images`, `/products`, `/users`, etc.

Paths can also accept variables. Say that we wanted to obtain a specific user by their `id`, say `543`. In that case the full URL would be `http://localhost:4000/users/543`. This will get the user whose id is equal to "543". But then someone might want user: 106, or user: 201, etc.

To design for all of these potential request in our server we would write that route with a variable: `:id`. As in,

```javascript
  app.get('/users/:id')`
```

This is what our app starts to look like with that logic:

```javascript
  // index.js
  const express = require('express')

  const app = express()

  app.use((req, res, next) => {
    next()
  })

  // GET all users. Usually known as "get all"
  app.get("/users")

  // GET just one user by id. Usually known as "get one"
  app.get("/users/:id")

  // the POST Method
  app.post()

  // the PUT Method
  app.put()

  // the DELETE Method
  app.delete()

  app.listen(8080, () => {
    console.log('Server is listening on port 8080.')
  })
```

### The 2nd Argument: a Callback Function

After the **path** we have to define a second parameter that tells the server what's supposed to happen when this route is called.

This second parameter is a callback function; meaning that this is what is suppose to happen when the method is called. In order for these callbacks to work they themselves need at least two argument passed into them: `req`(request) and `res`(response).

#### The Req Parameter

`req` represents the request object. This is the message that is sent from the frontend to our backend server. This object includes two main properties: `headers` and `body`. If you used Postman to submit a request with a body of `{ user: 'John' }` then we could access that by referring to `req.body`. There are other properties of the incoming request that we can access as well, such as `req.params`, `req.headers` and `req.cookies`.

  > NOTE: you must use a [Cookie parser](https://www.npmjs.com/package/cookie-parser) to do that last one.

`res` represents the response object. This is what we will send back to the end user (client) on the frontend from the backend. We can send responses in a variety of formats but the two most popular are plain text and JSON.

For example, let's say you want to send the text `"success"` to a user once an operation is complete. In that case you would complete whatever functionality you wanted inside of the callback and then call a the `send` method on the `res` object: `res.send("success")`. The user will see this message after executing the specified action with our API.

More commonly we are sending **data payloads**(data about a specific item: user or car, whatever) back to the user. On a GET request we might send the entire data object of a user back so that the client(front-end app/Postman). In that case, we called the `json` method on the `res` object to convert & package the data payload into a JSON string before we send it back to the client: `res.json(user)`.

  > This `user` parameter could be anything we wanted but naming it this way helps us developers know what's supposed to be in there. The same logic would go for our car data: `res.json(car)`

We will become more familiar with `req` and `res` as we practice more. However, now that we have our parameters and have a visual for the callback function we can put it all together. We mentioned previously that the first parameter is the **path** and the second parameter is the **callback function**, so when we write it all together we arrive at a variation of the following:

```javascript
  // index.js
  const express = require('express')

  const app = express()

  // ...more code here...

  // GET method to get all users with the second argument including req & res that will resolve to a 'success' message being sent to the client/frontend
  app.get('/users', (req, res) => {
    // ...perform some logic in here like getting the user data from the database...

    // then send back to the client a message saying 'success'
    res.send('success')
  })

  // GET method to get only one user by their id
  app.get('/users/:id', (req, res) => {
    // ...store the id of the user request using the params of the req object coming from the client...
    const userId = req.params.id
    // ...get the user data from the database using the `userId` variable...

    // send the back to client a message saying 'success'
    res.send(`We'll be sending you user ${userId} shortly.`)
  })

  // ...more code here... 
  // ...app.listen()...
```

What you see above is a couple of routes/**endpoints**. We will create many like these throughout this course. Take some time to understand how these methods work and the arguments that are being passed into them and what they are doing. In the coming sections we'll be adding on to these **endpoints to actually get data from a database so we can return actual data!!

## Practice It

Before playing in the sandbox below, be sure to [read this blog](https://blog.codeanalogies.com/2017/11/03/understanding-the-basics-of-express-js/) first!

<iframe width="920" height="640" src="https://www.codeanalogies.com/express-playground" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

- [ ] In the Express Playground above, hover over different sections of the code to get more info.
- [ ] [Read the article](https://blog.codeanalogies.com/2017/11/03/understanding-the-basics-of-express-js/) to get a better understand of how this playground operates and what Express is meant to do.

## Additional Resources

- [ ] [YT, SelfTuts - Pt. 1 What is Express in Node.js](https://youtu.be/pyKOM1whPfM)
- [ ] [Article, Code Analogies - The Basics of Express.js](https://blog.codeanalogies.com/2017/11/03/understanding-the-basics-of-express-js/)
- [ ] Look ahead to the [Questions for Student Led Discussion](./../additionalResources/questionsForDiscussion/qfd-class-3.md)

## Know Your Docs

- [ ] [Geeks4Geeks Docs - Express & Cookie-Parser](https://www.geeksforgeeks.org/express-js-req-cookies-property/)
- [ ] [Express Docs - Basics Routing](https://expressjs.com/en/starter/basic-routing.html)

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