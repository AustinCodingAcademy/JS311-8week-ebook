# Hashing and Tokens

Now that we have the whole process fresh in our minds let's dive into the details.

## Checking the Password

While it may seem like we could simply compare the password they put into the field to the one we stored in the database for them, its actually not that easy. The reason we can't do this is for security reason.

### Store Hash, not Plaintext

We don't store **plaintext** passwords in databases in case our data is ever breach. If a hacker was able to get these usernames and **plaintext** passwords they'd have access to all of our users information immediately!

  > Solution: To prevent this we run their plaintext password through an algorithm called [MD5](https://en.wikipedia.org/wiki/MD5) to create what's called a **hash**. This process turns `password` into `5F4DCC3B5AA765D61D8327DEB882CF99`.

The way we use this hash to check against the plaintext password they send to our server when signing inD is to pass it through the MD5 algorithm(function) and compare that function's return value to the **hash** stored in our database.

## Creating the Bearer Token

Once their password has been compared against the hash in the database and verified we will need to send them that **bearer token** to use on all of their future requests.
  
  > This is their "wristband" to the concert
  
The **bearer token** is a special set of numbers and letters created with another algorithm called [RFC 7519](https://docs.authlib.org/en/latest/specs/rfc7519.html) that uses our server's **key signature** to prove that the token came from our server and our server alone, and that it wasn't falsely manufactured by another server or someone else's computer.

  > This "signature" is really just a password we keep secret on our server that gets used only when tokens need to be signed.

So far we've been using the term **bearer token** but this really refers to the token when it's being presented by the client/user to the server in the request. The other name for this special key is **JWT**, or [JSON Web Token](https://en.wikipedia.org/wiki/JSON_Web_Token).

## Creating a JWT

A JWT might look like this:

```console
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

Look closely and you'll see two `.` These separate the token into three parts:

| Part Name | Example | Definition |
| - | - | - |
| Header | eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9 | includes information about the `type`, as in JWT, and the algorithm, `alg`, used to created it. |
| Payload | eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ | the actual data stored in it, like the `username` & `iat` (issued at) which tells the time the token was issued. |
| Signature | SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c | contains the hash of our server's key |

The provider of the Node package we'll be using to generate our signed JTWs has a really clear example on their homepage, [JWT.io](https://jwt.io/).

### Storing and Using the JWT

As mentioned above, our server will send a response to the client that stores the token on the client's cookie storage. Then it will be up to the client(our 411 React Front-end app) to add the JWT as a bearer token in the requests.

### Reading the JWT

Here is where we check for "wristbands". Once the request comes to our server it's going to be routed to the appropriate route but we only want *authenticated* users to access our resources so we'll add a function called something like `checkForAuthToken` or just `checkAuth`; then we'll tell our Express server to `.use()` it to `checkAuth`entication. If the check passes (the token is there and valid) then we'll allow them to do the `next()` step, *the route they requested*.

```javascript

  app.use(checkAuth()
  )
  const checkAuth = (req, res, next) => {
    // some logic here
    if (failed) res.status(401).json({ msg: "invalid authentication" })
    const payload = <DECODED TOKEN>
    req.user = payload
    next()
  }
```

This would **protect** ALL routes in our server. The `next` parameter tells the function to continue on to the `next()` function in the request.

If we want to **protect** only some routes with authentication we would place it as the second argument in the route:

```javascript

  app.get("/users", checkAuth, (req, res) => {
    // only gets here if authenticated
    // retrieve all users from the database
  })
```

  > The above function is pseudo-code but it is essentially saying, "I'm looking for an Authorization header. If I don't find one then I'm going to return an un-authorized message. Otherwise I'm going to decode the token sent with the header and attach the contents to the request (req.user) so I know who made the request". Calling the "next()" function is a successful end to the middleware function.

This type of "check" is called **middleware**. Its meaning is in the word. We tell our server to `.use()` a function(software) in-between(middle) of the request and the resource. There are all sorts of types and purposes of middleware but this authentication check is the most commonly used technique.

## But Why?

This is a good question! Why do we need to a JWT with a header, payload and signature? The answer to this question is security.

Think way back to when we first learned about HTTP(S) and how the internet is possible because computers are all built to read the same language and use the same protocol(HTTP). This means that all information sent over wifi, fiber, coax, satellite or copper is available to all computers in-between you and the server you're talking to across the country.

This space between you and that server or other computer is a very vulnerable space because it can be intercepted and read by many computers without you evening knowing. For this reason we have to **encrypt** the data we need to be private. **Encryption** is the act of "scrambling" the information in a mathematical way with a key only the sender and the receiver have. ...And this is the foundation of [Cyber Security](https://en.wikipedia.org/wiki/Computer_security).

With this in mind you might be thinking that creating your password hashes and bearer tokens is very difficult. It's actually not because we just use Node packages to generate them and we just tie them together to make them work for our app.

```javascript
  const jwksRsa = require('jwks-rsa')
  const jwt = require('express-jwt')
  const bcrypt = require('bcrypt')
```

In the next lesson we'll talk about lower level techniques of implementing these process.

## Additional Resources

- [ ] [YT, Chris Courses - Hashing Passwords with Bcrypt](https://youtu.be/lMSM-95XH2E)

  > NOTE: Industry standard is no longer bcrypt. Instead use [Argon-2](https://www.npmjs.com/package/argon2). The process is the same.