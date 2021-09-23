# Overview Of Authentication

*“I have not failed. I've just found 10,000 ways that won't work.” ― Thomas A. Edison*

Now that we have high overview of what authentication and authorization is, let's start zooming in on what the flow of authentication is and what we actually have to do to get it coded in our server!

## Why Authenticate?

Authentication is used by a server when the server needs to know exactly who is accessing their app.

It's important to understand authentication because it's necessary for the security of your app and to understand what every app on the internet does when you sign in. When building your fullstack projects at the end of the class, be sure to reference back to here if you need any extra help with building your login.

### Visualization of All steps

![stepsOfAuth](./../images/stepsOfAuth.png)

### General Steps of Authentication

1. The username and password are sent to the server.
2. The server accesses its database of users that holds the username and password.
3. It checks the provided username and password against the one in the database.
4. If the credentials match, the user's identity is verified, and the application decides what's next.
5. If not, a generic error message is returned.

## Sign-Up vs Sign-In

![writeToDatabase](./../images/writeToDatabase.png)

The first step of authentication is to sign up! After all, we can't verify your identity if we don't have credentials to compare with what you provide to confirm you are who you say your are.... When one signs-up on any web app, their credentials (username/email & password) will be sent from the front-end to the server and written to the database. *It's important to understand this because it will help you visualize how the server will be checking incoming "sign-in" credentials against previously written "sign-up" credentials.* It really is as simple as this:

- [ ] Input and submit email & password info on front-end to "sign-up"
- [ ] Front-End sends POST request with the the "sign-up" info to the server
- [ ] The server receives the credentials and `INSERT`s a new entry in the `users` table
- [ ] The user returns to the app to login by inputting and submitting their email & password on the front-end
- [ ] The front-end sends a GET Request with the credentials to the server
- [ ] The server `SELECTS` the previously written email that matches and checks to see if the passwords match
- [ ] If `true` the next page in the app is sent to the front-end and a **bearer token** is stored cookies (more on this soon)
- [ ] If `false` another "login" page is sent to the front-end

### The Hash

There's a small step the summary above excludes called **hashing**. See, when we store passwords in our database we don't want to store **plaintext** because if our database is ever breached/hacked into the passwords will be readable by human-eyes and simple javascript functions. To protect our users we create new strings that represent the password called a *hash*.

A hash is a unique and complicated string created by passing a simple string into a mathematical formula (algorithm) that scrambles and generates a the unique string. The way it works is highly mathematical but in short it could look like this:

| Simple String | The Hash Produced |
| - | - |
| pony | 4B3E3C2F99046F92A61BAB6775848577 |
| apple | 1F3870BE274F6C49B3E31A0C6728957F |
| pony | 4B3E3C2F99046F92A61BAB6775848577 |

No matter what, if you pass `pony` through the hashing algorithm is will also produce the `4B3E3C2F99046F92A61BAB6775848577` every time. This is how passwords can be stored as hashes and later compared, hash to hash. We just use a hashing algorithm in-between our server receiving the request and when it reads the database.

> You can play with how the [MD5 hashing algorithm will create unique strings with any common string you put in here](https://passwordsgenerator.net/md5-hash-generator/).

We will cover more hashing soon but for now just remember the password will be scrambled each time its written and compared against.

#### The Code for Hashing

Below is a small Express server that has a hashing algorithm added to it called `argon2`. Read over the code and see if you can make sense of what's going on.

= "Express App with Argon2 Hashing"

    ```javascript
      const express = require('express'),
      // import argon for hashing
        argon2i = require('argon2-ffi').argon2i,
        crypto = require('crypto'),
        bodyParser = require('body-parser');

      // create express app 
      const app = express();
      const jsonParser = bodyParser.json();

      // post request route for when a user signs up for the app
      app.post('/signup', jsonParser, function(req, res){
        // if incorrect credentials send status 400
        if(!req.body) return res.sendStatus(400);
        // using argon2, hash the request body that has the password.
        crypto.randonBytes(32, function(err, salt){
          if(err) throw err;
          argon2i.hash(req.body.password, salt).then(hash => {
            console.log(hash);
            // then send a 201 status that it was successful.
            res.sendStatus(201);
          })
        })
      })

      app.listen(3001, function(){
        console.log("listening on port 3001");
      })
    ```

As you can see from this code the password will now be scrambled like this `password:wkehodjsuekr` from now on. If you want to learn more about hashing and argon take a look at the docs below. We will also be covering this in more depth soon.

*******

## Write Code of Authentication

The following code example will assume our human-user has already "sign-up" so their email/username and password are already stored in our database.

```javascript
// middleware function, middleware is just a name for the function that checks a user os authenticated. When we create this function we can now use it to check all of our routes for the correct user.
      const authenticate = (req, res, next) => {
        const auth = req.headers['authorization']
        if (!auth) return res.sendStatus(401)
        next()
      }

// middleware applied, now we have the function we can pass in this authenticate function to our route as a parameter and it will run the function before posting. 
      app.post('/', authenticate, (req, res) => {
        res.send(`You sent an authorization header...You're Postin!`)
      })
```
### Request from the Front-End

logging in to the app. When you go to log into a webapp it will prompt you for the credentials you entered during the sign up. When you click the login button it will then make a `get` request to the server or API you are trying to access.

=== "Request from the Front-End"

```javascript
  axios.get('https://theserverorapiurl.com/user?ID=1')
  .then(function (response) {
    //handle success
    //remember to console.log
    console.log(response)
  })
```

When you submit a login remember the next steps all happen within seconds but are vital to understand authorization. 

### Server Handles the Request
The server checks the provided username and hashed password against the one in the database.

credentials you sent => user=username:hashedPassword  ==> checks the database user=myusername:mypassword

This is the logic that checks the token and verifies if its valid before sending the request resource back.

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

### Server Calls the Hashing Algorithm
When we create our server it will have a simple post request, that when we put in our username and password it will call the hashing algorithm to take the password input and hash using argon2. 

```javascript
require argon2 = require('argon2')
//1. register user
server.post('/register', async (req, res) => {
  const { email, password } = req.body;

  try {
//using this code we will hash our password a user inputs.
    const hash = await argon2.hash(password)
    console.log(hash)
  }catch (err) {
//error code here
  }
})
```

following this code we can open postman and run a request to our local host url and our register route like this: POST `http://localhost:4000/register`. navigate to the body of the post request in postman and input two key fields. fist field will be email with a random email of your choosing. The second will be password with any random password you choose. Then kick up your local host in the terminal and run the post request on postman. You should receive a random string that looks like this `$argon2i$v=19$m=4096,t=3,p=1$rHPRPtbiIVGRVT4dUWDizw$v4jily1SeNYrmDhX9uD8MOePv+9U+2Lqvwc4iUsJOa0`.
<!-- TODO @David Fill this out -->

### Server Requests the Password from the DB
<!-- TODO @David Fill this out -->
The server hits the get request route we set up and then runs a function to compare the inputted password with the password stored in the database.
### Server Compares the Return Values
<!-- TODO @David Fill this out -->
```javascript
 app.post('/login', function(req, res) {
  Parse.User.enableUnsafeCurrentUser();
  Parse.User.logIn(req.body.username, req.body.password).then(function(user) {
    res.redirect('/home');
  }, function(error) {
    res.render('login', { flash: error.message });
  });
});
```
<!-- ## Step 4 -->

If the credentials match, the user's identity is verified, and the application decides what's next. After they are successfully authenticated our app will send the user a bearer token to keep with you during the time you are using the app. (once you logout this token will be terminated until you login again). If you didn't receive this token then you would have to re-login every time you wanted to change pages in the app. Its not very user friendly. 

After you are granted authorization to the web app you will now have a cookie attached to your info in the database and this cookie will follow you around the web app keeping you authorized.

### Server Generates a Bearer Token
The bearer token is a token created by the server to ensure you are coming from the correct place. Using JWT you'll be able to create a token and then a signature will be in place from now on. More on JWT soon but keep in mind this step.

```javascript
//require sign from jwt
const { sign } = require('jsonwebtoken');
//create a function
const createBearerToken = userId => {
  return sign({ userId }, process.env.BEARER_TOKEN_SECRET, {
    expiresIn: '15m',
  }) 
}
```
### Server Sends a Token to the Front-End
Once the Token is created we will send it back to our front end. The front end of your code will use the bearer token we created to authenticate a user. The front-end will use a post request to access the bearer token we created in the back-end.
### Front-End Stores The Token in Cookies
We store the token in a cookie for the browser to keep track of. 
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

### Conclusion

<!-- TODO @David Don't write this like it's blog. This is an ebook that has lots of documentation. Encourage and push them toward the next lesson -->
Take what you learned from this lesson and really take the time to look over the resources below. Authentication is one of the most important parts of learning the back-end flow of applications. Next were going to talk about hashing and tokens in more depth. Refer back here and see how the tokens are being used in the big picture.
<!-- ## Follow-up Video  -->
<!-- TODO add video -->

## Additional Resources

<!-- TODO @David fix these titles to match naming convention, see other files to see naming convention -->
<!-- EXAMPLES: 

      TYPE  -- CONTRIBUTOR/SITE -- TITLE
- [ ] [Forum, StackOverflow - Cookie Naming Convention](https://stackoverflow.com/questions/2097843/naming-cookies-best-practices)
- [ ] [YT, Ben Awad - How to Store JWT in Memory](https://youtu.be/iD49_NIQ-R4) 
-->

- [ ] [Artical, ExpressJS Authentication, tutorial](https://www.tutorialspoint.com/expressjs/expressjs_authentication.htm)
- [ ] [Artical, argon tutorial - video and tutorial](https://www.veracode.com/blog/secure-development/zero-hashing-under-10-minutes-argon2-nodejs)
- [ ] [video, jwt - tutorial](https://www.freecodecamp.org/news/what-are-json-web-tokens-jwt-auth-tutorial/)

## Know Your Docs

<!-- TODO @David fix this title. Always use this naming convention -->
- [ ] [MDN Docs - title](https://developer.mozilla.org/en-US/docs/Web/API/Web_Authentication_API)
- [ ] [MDN Docs - Set Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie)