# Intro to Authentication

*Nothing will ever be attempted if all possible objections must first be overcome. —Samuel Johnson*

## Overview

We've practiced building APIs and analyzing the data behind them. Now it's time to add a level of security to those APIs so that we can restrict access to authorized users.

Authentication is an important part of creating APIs. As I'm sure we can all guess, authentication is used to lock down specific endpoints so that they cannot be freely accessed. To learn how to implement authentication on our server(API) we'll need to understand the process or **workflow** as well as a few new terms. Let's get started.

## Authentication vs Authorization

Let's first clear up the definition of these two words. **Authentication** is the process of verify weather a person-user has access to a resource or not. For instance, you have signed up for API keys with at least two APIs. These keys authenticate your requests for the resources at those APIs; its being sent in the `params` of each of your requests. It's like buying a ticket to a concert and flashing it at the gate(*sign-in*), then you get a wristband(*authenticated*) and you're allowed to go in and enjoy the music!

  > ...but what's a *backstage pass*?

When we build apps with data that needs to be allowed to certain person-users and restricted to others we need to implement **Authorization**. This is the process of assigning **roles** to each person-user.

Maybe you're building a classroom management app for you and your students. All of the data for this app will be stored in the same database and served by the same server but you don't your students to have access to other students' grades and turned-in assignments but still have access to their own assignments and grades. However, for you, the teacher you want to be able to see all of the student's grades. To solve this problem you would assign each user of the app a role when they sign-up. Teachers would get a `teacher` role, students would get a `student` role and maybe parents would get a `parent` role.

In your Express server you add an if statement to each route that asked if they were a `teacher` to access the resources behind the `getAllGrades()` so that `student` and `parent` users would be blocked from this particular resource.

  > ...authorization is a backstage pass. Beyond being admitted to the concert(authentication) you're also allowed to go backstage and maybe meet the artists!

## Authentication Workflow

Now let's talk through the process from a high perspective. You'll be seeing code snippets as we go but just know there may be some modifications to this code in live code bases. But please read the pseudo-code so you picture, for yourself, this process.

The first step in this process is that the client/front-end will make a request to our server/API:

```javascript
  // front-end
  axios.get('https://ourapi.com/user?ID=12345')
  .then(function (response) {
    // handle success
    console.log(response)
  })
```

Just as we've built our serve to do, it will be listening and will return (respond) with the resource that was requested:

```javascript
  // back-end
  app.get('/users', (req, res) => {
    // perform some logic to go get the logic
    // maybe move this function over to a controller file??
    res.json(users)
  })
```

But now we want to see if the user is in our system, aka **authenticate** them, before we let them get to the resource they want... To do this we will ask them to sign-in with their username and password. If they are successful with their sign-in we will send to them a "wristband", or **token**, that proves they are authenticated and will be used on all of their following requests (until they logout) so they don't have to keep entering their username and password. This *token* is called a **bearer token**

```javascript
  // back-end
  const login = (req, res) => {
    const { username, password } = req.body

    // * build and call your own authentication function using our server's secret key
    const jwtSecret = 'secret123'

    app.get('/jwt', (req, res) => {
      const token = jsonwebtoken.sign({ user: 'username' }, jwtSecret)
      
      // the response object has a method on it called` that takes three arguments:
        // * name of the cookie
        // * value of the cookie
        // * parameters of the cookie
      // and sets a cookie on the user's browser/client.
      res.cookie('our_token', token, {httpOnly: true})

      res.json({ token })
    });

    // -or-

    // * send the username & password to a third-party like Auth0, see below:
    axios(`https://${process.env.AUTH0_DOMAIN}/oauth/token`, {
      // ...more on this later...
    })
    .then(response => {
      // if the username & passwords are correct send the token back to the client/front-end
      const token = response.data.access_token 
      res.cookie('our_token', token, {httpOnly: true})

      res.json({ token })
    })
    .catch(e => {
      res.send(e)
  })
```

Once the `res.cookie` method has been called a cookie that is specific to our server's domain has been set on the user's browser/client and it's sent in the headers of each subsequent request:

```javascript
  // front-end

  // create a configuration object with the the correct keys and values
  // the token should be in the headers
  const config = {
    withCredentials: true,
    headers: { Authorization: `Bearer: ${document.cookies.our_token}`}
  }

  // send the config object with the request
  axios('https://ourapi.com/user?ID=12345', { config })
  .then(function (response) {
    // handle success
    console.log(response)
  })
```

  > NOTE: yes `cookies` may be accessed via `document.cookies` but when we build with React we'll need to use a [special React cookie parser](https://www.npmjs.com/package/react-cookie) to access our cookies.

Now we'll build some logic into our server that asks to see that token ("wristband") and verifies if it's valid before sending the requested resources back.

```javascript
  // back-end
  const checkForAuthToken = (req, res, next) => {
    const specialToken = req.headers['our_token']

    if (!checkIsValid(specialToken)) return res.sendStatus(401)
    next()
  }

  // build your own
  const checkIsValid = (token) => {
    // this function would run the RFC 7519 algorithm to see if the token is valid(see below)
      // * if valid return true
      // * if not valid return false
      // * or we could use a third party to handle this like Auth0
  }

  //  -- or --
  // use a third-party like Auth0
```

If this check fails we could choose to send them a 403 or re-route them to the login page, ...or both!

Okay, that's the higher overview of all this authentication stuff. Let's now look more closely at the details of it. Let's start with that **hash** business we just saw above.

## Practice It - Sending a Bearer Token

- [ ] [Express Server Repl.it](https://replit.com/@HippErger/Express-SQLite3-AuthenticationHeaderPractice)

=== "the Server"

    ```javascript
      const express = require('express');
      const bodyParser = require('body-parser');
      const db = require('./db');

      const app = express();

      app.use(bodyParser.json());
      app.use(bodyParser.urlencoded({ extended: true }));

      app.use(express.static('public'));

      // middleware function
      const authenticate = (req, res, next) => {
        const auth = req.headers['authorization']
        if (!auth) return res.sendStatus(401)
        next()
      }

      app.get('/', (req, res) => {
        res.send(`You're gettin' to this server!! Ask for those digits!`);
      });

      // middleware applied
      app.post('/', authenticate, (req, res) => {
        res.send(`You sent an authorization header...You're Postin!`)
      })

      app.listen(3000, () => console.log('server started and listening on port 3000'));
    ```

=== "Create the Database"

    ```javascript
      const sqlite3 = require('sqlite3').verbose();

      // much like the connection pool in mysql (the Node package) this object is used to create a light database with just a blank file: db2.sqlite3 
      // NOTE: .sqlite3 is the suffix)
      let db = new sqlite3.Database('./db2.sqlite3', (err) => {
        if (err) {
          return console.error(err.message);
        }
        console.log('Connected to the db2 SQlite database.');
      });

      module.exports = db;
    ```

=== "the Database in Memory"

    ```sql
      -- CREATE TABLE IF NOT EXISTS books (name TEXT, author TEXT)
    ```

- [ ] Open and fork the Repl.it above.
- [ ] Run the application.
- [ ] Copy the URL at the top right of the screen in the fake browser.
- [ ] Open up Postman and make a GET request to this endpoint. Did you get a response back?
- [ ] Make a POST request to this endpoint. Did you get "Unauthorized"?
- [ ] Under the Headers tab in Postman, add a header to the POST with the key "Authorization" and a value of literally any string of characters and retry. You should now see a response that says "You sent an authorization header...You're Postin!".
- [ ] Play around with the middleware function. Try changing: if (!auth) on ~line 15 to be a different condition so that you must send a specific string in the authentication header.
- [ ] Before moving on make sure you understand how it's being used. Add console.log statements into the authenticate function to see what data is being passed through it and how it's working.

## Additional Resources

- [ ] [Forum, StackOverflow - Cookie Naming Convention](https://stackoverflow.com/questions/2097843/naming-cookies-best-practices)
- [ ] [YT, Ben Awad - How to Store JWT in Memory](https://youtu.be/iD49_NIQ-R4)
  > Also really good overview of security threats
- [ ] [Article, TaniaRascia.com - Full Stack Cookie Storage](https://www.taniarascia.com/full-stack-cookies-localstorage-react-express/)
- [ ] [Article, RyanChenkie@Medium - Storing JWT in Cookie in React App](https://medium.com/@ryanchenkie_40935/react-authentication-how-to-store-jwt-in-a-cookie-346519310e81)
- [ ] [OWASP - Cookie & CSRF, Cross-Site Request Forgery](https://owasp.org/www-community/attacks/csrf)

## Know Your Docs

- [ ] [MDN Docs - Set Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie)
- [ ] [Express Docs - Middleware](https://expressjs.com/en/guide/using-middleware.html)
- [ ] [NPM Docs - React-Cookie](https://www.npmjs.com/package/react-cookie)

