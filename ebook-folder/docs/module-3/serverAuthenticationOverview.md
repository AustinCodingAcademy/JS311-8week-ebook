# Overview Of Authentication

*“I have not failed. I've just found 10,000 ways that won't work.” ― Thomas A. Edison*

Now that we have a high overview of what authentication and authorization are, let's start zooming in on what the flow of authentication is and what we actually have to do to get it coded in our server!

## Why Authenticate?

Authentication is used by a server to give permission for a user to access the data it serves.

It's important to understand authentication because it's necessary for the security of your app and to understand what every app on the internet does when you sign in. When building your fullstack projects at the end of the program, be sure to reference back here if you need any extra help with building your login.

## The Steps of Authentication

Authentication is the process of comparing passwords to passwords to verify or authenticate the identity of a user.

![stepsOfAuth](./../images/stepsOfAuth.png)

1. The username and password are sent to the server.
2. The server accesses its database of users that holds the username and password.
3. The server checks the provided username & password against the username & password in the database.
4. If the credentials match, the user's identity is verified, and the application decides what's next.
5. If not, a generic error message is returned.

*****

### The Sign-Up Overview

There's a difference between Sign-Up vs Sign-In. We first need to **Sign-up**.

![writeToDatabase](./../images/writeToDatabase.png)

The first step of authentication is to sign up! After all, we can't verify your identity if we don't have credentials to compare with what you provide to confirm you are who you say you are.... When one **signs-up** on any web app, their credentials (username/email & password) will be sent from the front-end to the server and written to the database.

  > *NOTE: It's important to understand this because it will help you visualize how the server will be checking incoming "sign-in" credentials against previously written "sign-up" credentials.*
  
It really is as simple as this:

- [ ] Input and submit email/username & password info on front-end to "sign-up"
- [ ] Front-End sends POST request with the the email/username & password to the server
- [ ] The server receives the credentials and `INSERT`s a new entry in the `users` table
- [ ] The user returns to the app to login by inputting and submitting their email & password on the front-end
- [ ] The front-end sends a POST Request with the credentials to the server
- [ ] The server `SELECTS` the previously written email that matches and checks to see if the passwords match
- [ ] If `true` the next page in the app is sent to the front-end and a **bearer token** is stored in cookies (more on this soon)
- [ ] If `false` another "login" page is sent to the front-end

#### Hashing

There's a small step the summary above excludes called **hashing**. See, when we store passwords in our database we don't want to store **plaintext** because if our database is ever breached(hacked) the passwords will be readable by human-eyes and simple javascript functions. To protect our users we create new Strings that represent the passwords called a **hash**.

A **hash** is a unique and complicated String created by passing a simple String into a mathematical formula (algorithm) that scrambles and generates a unique String. The way it works is highly mathematical ([luckily there are Node packages for it](https://www.npmjs.com/package/argon2)) but in short it could look like this:

| Simple String | The Hashed String |
| - | - |
| pony | 4B3E3C2F99046F92A61BAB6775848577 |
| apple | 1F3870BE274F6C49B3E31A0C6728957F |
| pony | 4B3E3C2F99046F92A61BAB6775848577 |

No matter what, if you pass `pony` through the hashing algorithm is will also produce the `4B3E3C2F99046F92A61BAB6775848577` every time. This is how passwords can be stored as hashes and later compared, **hash** to **hash**. We just use a hashing algorithm in the route on our server between receiving the request to "login" and when the server reads the previously stored hash in the database created during "sign-up".

  > You can play with how the [MD5 hashing algorithm will create unique strings with any common string you put in here](https://passwordsgenerator.net/md5-hash-generator/).

Once the plaintext password has been hashed the new unique String will be stored in the database along with the username/email.

##### The Code for Hashing

Below is a small Express server that has a hashing algorithm added to it called `argon2`. Read over the code and see if you can make sense of what's going on.

=== "Express App with Argon2 Hashing"

    ```javascript
      const express = require('express')
      // import argon for hashing
      const argon2i = require('argon2-ffi').argon2i
      const crypto = require('crypto')
      const bodyParser = require('body-parser')

      // create express app 
      const app = express()
      const jsonParser = bodyParser.json()

      // post request route for when a user signs up for the app
      app.post('/signup', jsonParser, function(req, res){
        // if no data has been sent, send back status 400
        if(!req.body) return res.sendStatus(400)
        // using argon2, hash the request body that has the password.
        crypto.randonBytes(32, function(err, salt){
          if(err) throw err
          argon2i.hash(req.body.password, salt).then(hash => {
            // don't log in production code...for learning purposes only
            console.log(hash) //...replace with code to write the username & password to the database

            // then send a 201 status that it was successful.
            res.sendStatus(201)
          })
        })
      })

      // ...more routes would go here...

      app.listen(3001, function(){
        console.log("listening on port 3001")
      })
    ```

As you might have seen, when someone sends a POST request to `/signup` it should include a `username` and `password`. If it does, the server will run the hashing function `crypto.randonBytes` & `argon2i.hash` on the password. You are probably wondering what `salt` is. `salt` is the number of times the algorithm is supposed to run before the hash is determined "complete".

Hackers have access to run the same algorithm that creates your password hashes. This means, if they get ahold of your list of usernames & passwords they can run them backwards as well and learn the plaintext version of your passwords and then access your user's data. Nevertheless, they will still be guessing at possible inputs to get to the correct password. To break through this barrier they will formulate something called a **Brute Force** attack, where in, they tell a powerful computer to run the same algorithm over and over on the list of hashed passwords attempting to get the right passwords. This is where a **salt round** comes in. A **salt round** is the number of times the algorithm scrambles the plaintext password. 1 salt = 1 time, 5 salts = 5 times. Each time you increase the **salt** you increase the difficulty for the hacker by a factor of about 10! By increasing this number you make it more expensive in both time and energy for the hacker to make it profitable to hack your users. The double-edge of this sword is that it also makes it more expensive for your computers to run the hashing algorithm. The trick is to find a happy medium! Usually 12 is the ideal number; but, some have suggested you [calculate the number with the total amount of time you can stand.](https://security.stackexchange.com/questions/17207/recommended-of-rounds-for-bcrypt)

To get an idea of why salting is so important when hashing password, check out this post from 2011.

![securityStackExchange-saltingGuesses](./../images/securityStackExchange-saltingGuesses.png)

  > SOURCE: [Security StackExchange](https://security.stackexchange.com/questions/3959/recommended-of-iterations-when-using-pbkdf2-sha256/3993#3993)

### The Sign-In Overview

Now that we know passwords will be hashed on **sign-up**, what happens when a user signs-in?

Obviously we don't want our user to have to input a username and password for every page and resource they'd like to access. Instead, we want them to have them sign-in once and then allow them to freely move around their account until they **sign-off**.

The trouble is that our server (just a computer) doesn't know who they are like we humans would if we saw them. So, to make this work we have to give the user a "wristband" that they would show to each part of the server when they wanted to see a new page or resource. This "wristband" is called a **bearer token**.

A **bearer token**, or a **JSON Web Token**/**JWT**, is a unique set of letters and numbers created by the server the represents a successful **sign-in**. Its generated when username & passwords match and sent back to the client (the user) and stored on their device so that it can be sent back to the server with each new subsequent request to see a new page or resource. In this way, the user can move freely about their account without worrying about signing-in over and over; but instead we developers just have to be smart enough to make that front-end client send the **bearer token** back with each new request, and make our server require a **bearer token** to allow the resources to be sent back with the response.

<!-- Let's dive into this, shall we? -->

<!-- ***** new page ***** -->

<!-- 
## Now Build Your Authentication Workflow

In this section we're going to comb over the entire process of authentication, after the user has already **signed-up**, with more granular detail. Use the side menu of this page (>>>) to see the overview and visualize the entire process. -->

<!-- Request from the Front-End
Server Handles the Request
Server Calls the Hashing Algorithm
Server Requests the Password from the DB
Server Compares the Return Values
Server Generates a Bearer Token
Server Sends a Token to the Front-End
Front-End Stores The Token in Cookies
Conclusion

### Request from the Front-End/Client

**Sign-in**. Any web app you use will prompt you for your credentials(username & password). When you click the login button the front-end will then make a POST request to the server sending the credentials.

=== "Request from the Front-End"

```javascript
  // front-end code (NOT SERVER-SIDE)
  const axios = require('axios')

  axios.get('https://theserverorapiurl.com/login', {
    username: 'WFinn',
    password: 'password123'
  });

  .then((response) => {
    console.log(response);
  }, (error) => {
    console.log(error);
  });
```

 > Remember: When you submit a login, the next steps all happen within seconds but are vital to understand authorization.

 > Also, we use Postman to imitate client-side requests so we don't have to build our front-end and back-end, only to have a bug in either one and not know what we're missing. Instead we build our back-end, test it with Postman, then move to building the front-end with the same requests we made in Postman.

### How the Server Handles the Request

Once the server receives the request, it will:

- [ ] Calls the hashing algorithm and run the plaintext password through it,
- [ ] retrieve the hashed password from the database created during sign-up,
- [ ] compare the two hashed Strings,
- [ ] if they don't match (`false`) an error will be sent back the client/front-end;
- [ ] if they match (`true`) a function to create a bearer token will be invoked,
- [ ] the bearer token will be sent back to the client/front-end.

Let's build that process.

=== "**1. In a new `server` folder create an `index.js` file:**"

    ```js
      // server/index.js
      const express = require('express')
      const argon2i = require('argon2-ffi').argon2i
      const crypto = require('crypto')
      const bodyParser = require('body-parser')

      const app = express();
      
      app.listen(3000, function(){
        console.log("Listening on port 3000...");
      });
    ```

=== "TODO cp argon2 file"

    cp argon2 file in to release directory - [https://www.veracode.com/blog/secure-development/zero-hashing-under-10-minutes-argon2-nodejs](https://www.veracode.com/blog/secure-development/zero-hashing-under-10-minutes-argon2-nodejs)

=== "**3. Create the route to hash the password for sign-ups:**"

    ```js
      // server/index.js
      // ...import statements here...

      const app = express();
      const jsonParser = bodyParser.json();
    
      app.post('/signup', jsonParser, function(req, res) {
        if(!req.body) return res.sendStatus(400);
      
        crypto.randomBytes(32, function(err, salt) {
          if(err) throw err;
      
          argon2i.hash(req.body.password, salt).then(hash => {
            console.log(hash); /* in the future, you'll replace this line with a call to a controller that will store the `hash` & `req.body.username` in the Users table in the database */
            
            res.sendStatus(201);
          });
        });
      });
      
      app.listen(3000, function(){
        console.log("Listening on port 3000...");
      });
    ```

=== "**4. Test it with Postman**"

    - [ ] Run the file with Node from the terminal `node index.js`
    - [ ] Open Postman
    - [ ] Create a POST request to `http://localhost:3000/signup`.
    - [ ] Navigate to the `body` of the post request and create two fields: `username` & `password`
    - [ ] Send
    - [ ] You should receive a unique String that looks something like this: `$argon2i$v=19$m=4096,t=3,p=1$rHPRPtbiIVGRVT4dUWDizw$v4jily1SeNYrmDhX9uD8MOePv+9U+2Lqvwc4iUsJOa0`. -->

<!-- #### Server Calls the Hashing Algorithm -->

<!-- ### Server Requests the Password from the DB -->
<!-- TODO @David Fill this out -->
<!-- The server hits the get request route we set up and then runs a function to compare the inputted password with the password stored in the database.

### Server Compares the Return Values -->
<!-- TODO @David Fill this out -->

<!-- ```javascript
  app.post('/login', function(req, res) {
    Parse.User.enableUnsafeCurrentUser();
    Parse.User.logIn(req.body.username, req.body.password).then(function(user) {
      res.redirect('/home');
    }, function(error) {
      res.render('login', { flash: error.message });
    });
  });
``` -->
<!-- ## Step 4 -->

<!-- If the credentials match, the user's identity is verified, and the application decides what's next. After they are successfully authenticated our app will send the user a bearer token to keep with you during the time you are using the app. (once you logout this token will be terminated until you login again). If you didn't receive this token then you would have to re-login every time you wanted to change pages in the app. Its not very user friendly.

After you are granted authorization to the web app you will now have a cookie attached to your info in the database and this cookie will follow you around the web app keeping you authorized.

### Server Generates a Bearer Token

The bearer token is a token created by the server to ensure you are coming from the correct place. Using JWT you'll be able to create a token and then a signature will be in place from now on. More on JWT soon but keep in mind this step.

```javascript
//require sign from jwt
const { sign } = require('jsonwebtoken');

//create a function that will generate a unique bearer token
const createBearerToken = userId => {
  return sign({ userId }, process.env.BEARER_TOKEN_SECRET, {
    expiresIn: '15m',
  }) 
}


// server.post('/register', async (req, res) => {...etc

//  app.post('/login', function(req, res) {...etc
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

### Conclusion -->

<!-- TODO @David Don't write this like it's blog. This is an ebook that has lots of documentation. Encourage and push them toward the next lesson -->
<!-- Take what you learned from this lesson and really take the time to look over the resources below. Authentication is one of the most important parts of learning the back-end flow of applications. Next were going to talk about hashing and tokens in more depth. Refer back here and see how the tokens are being used in the big picture. -->

<!-- ## Follow-up Video  -->
<!-- TODO add video -->

## Additional Resources

- [ ] [Article, TutorialsPoint, ExpressJS Authentication](https://www.tutorialspoint.com/expressjs/expressjs_authentication.htm)
- [ ] [Article, Veracode - Zero to Hashing in 10 minutes](https://www.veracode.com/blog/secure-development/zero-hashing-under-10-minutes-argon2-nodejs)
- [ ] [Video, FreeCodeCamp - What are JWTs?](https://www.freecodecamp.org/news/what-are-json-web-tokens-jwt-auth-tutorial/)
- [ ] [Forum, StackOverflow - Cookie Naming Convention](https://stackoverflow.com/questions/2097843/naming-cookies-best-practices)
- [ ] [YT, Ben Awad - How to Store JWT in Memory](https://youtu.be/iD49_NIQ-R4) 

## Know Your Docs

- [ ] [NPM Docs - Argon2](https://www.npmjs.com/package/argon2)
- [ ] [MDN Docs - Web Authentication](https://developer.mozilla.org/en-US/docs/Web/API/Web_Authentication_API)
- [ ] [MDN Docs - Set Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie)

<!-- The following code example will assume our human-user has already "sign-up" so their email/username and password are already stored in our database.

```javascript
  // middleware function, middleware is just a name for the function that runs between a request and response; in this case we want to check to see if they are authenticated before we respond. When we create this function we can now use it to check all of our routes for the correct user.
  const authenticate = (req, res, next) => {
    const auth = req.headers['authorization']
    if (!auth) return res.sendStatus(401)
    next()
  }

  // middleware applied, now we have the function we can pass in this authenticate function to our route as a parameter and it will run the function before posting. 
  app.post('/', authenticate, (req, res) => {
    res.send(`You sent an authorization header...You're Postin!`)
  })
``` -->

<!-- This is the logic that checks the token and verifies if its valid before sending the request resource back.

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
``` -->

<!-- When we create our server it will have a simple post request, that when we put in our username and password it will call the hashing algorithm to take the password input and hash using argon2.

```javascript
const argon2 = require('argon2')
//1. register(sign-up) user
server.post('/register', async (req, res) => {
  const { email, password } = req.body;

  try {
  //using this code we will hash the password a user inputs.
    const hash = await argon2.hash(password)
    console.log(hash)
  } catch (err) {
    //error code here
    console.log(err)
  }
})
``` -->