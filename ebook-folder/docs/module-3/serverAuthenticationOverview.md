# Overview Of Authentication 

*“I have not failed. I've just found 10,000 ways that won't work.”
― Thomas A. Edison

## What is Authentication?

Hi everyone this section of the text book will focus on the overview of authentication. Authentication is used by a server when the server needs to know exactly who is accessing their app. 

## Why?

It's important to understand authentication because it's necessary for the security of your app and to understand what every app on the internet does when you sign in. When building your fullstack projects at the end of the class, be sure to reference back to here if you need any extra help with building your login. You can also bookmark this lesson to refer back later.

## Visualization of All steps

![stepsOfAuth](./../images/stepsOfAuth.png)

## Steps of Authentication
1.The username and password are sent to the server.
2.The server accesses its database of users that holds the username and password.
3.It checks the provided username and password against the one in the database.
4.If the credentials match, the user's identity is verified, and the application decides what's next.
5.If not, a generic error message is returned.

## Sign-Up

![writeToDatabase](./../images/writeToDatabase.png)

The first step of Authentication is to sign up for the app you're making or using. When you sign up for a web app, it will write to the database being used by the app sending the email/password you used to sign up. It's important to understand this because it will help you visualize how the server is checking for the correct person to log-in. 

When you send the server your sign up information, it will hash or salt the password for security reasons. We will cover more hashing soon but for now just remember the password will be scrambled.

## Example Of A Salted/hashed User Input

```javascript
const express = require('express'),
//require argon for hashing and salt
  argon2i = require('argon2-ffi').argon2i,
  crypto = require('crypto'),
  bodyParser = require('body-parser');

//create express app 
const app = express();
const jsonParser = bodyParser.json();

//post request for when a user signs up for the app
app.post('/signup', jsonParser, function(req, res){
  //if incorrect credentials send status 400
  if(!req.body) return res.sendStatus(400);
//using argon hash the request body that has the password.
  crypto.randonBytes(32, function(err, salt){
    if(err) throw err;
    argon2i.hash(req.body.password, salt).then(hash => {
      console.log(hash);
      //then send a 201 status that it was successful.
      res.sendStatus(201);
    })
  })
})

app.listen(3001, function(){
  console.log("listening on port 3001");
})

```
As you can see from this code the password will now be scrambled like this `password:wkehodjsuekr` from now on. If you want to learn more about hashing and argon take a look at the docs below. We wil also be covering this in more depth soon.

## Step 1

logging in to the app. When you go to log into a webapp it will prompt you for the credentials you entered during the sign up. When you click the login button it will then make a `get` request to the server or API you are trying to access. 

```javascript
axios.get('https://theserverorapiurl.com/user?ID=1')
.then(function (response) {
  //handle success
  //remember to console.log
  console.log(response)
})
```

When you submit a login remember the next steps all happen within seconds but are vital to understand authorization. 

## Step 2

This step once clicked, the login sends the server a call that tells the server to take a look at the database the app is using to verify who is logging in. 

## Step 3

It checks the provided username and hashed password against the one in the database.

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
## Step 4

If the credentials match, the user's identity is verified, and the application decides what's next. After they are successfully authenticated our app will send the user a bearer token to keep with you during the time you are using the app. (once you logout this token will be terminated until you login again). If you didn't receive this token then you would have to re-login every time you wanted to change pages in the app. Its not very user friendly. 

After you are granted authorization to the web app you will now have a cookie attached to your info in the database and this cookie will follow you around the web app keeping you authorized. 

## Cookie code

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

I hope this helps visualize the process of the code being written. If you have trouble with the coming classes reference back here and try to visualize the code being written and why its important. 

## Follow-up Video 
<!-- TODO add video -->
## Additional Resources

- [ ] [ExpressJS Authentication](https://www.tutorialspoint.com/expressjs/expressjs_authentication.htm)
- [ ] [argon tutorial](https://www.veracode.com/blog/secure-development/zero-hashing-under-10-minutes-argon2-nodejs)

## Know Your Docs

- [ ] [MDN Docs - title](https://developer.mozilla.org/en-US/docs/Web/API/Web_Authentication_API)
- [ ] [MDN Cookie docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie)