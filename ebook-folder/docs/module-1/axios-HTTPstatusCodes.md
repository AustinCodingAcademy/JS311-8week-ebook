# Axios and HTTP(S) Status Codes

*The only way of finding the limits of the possible is by going beyond them into the impossible. —Arthur C. Clarke*

## Overview

In the last lesson we refreshed our knowledge of Node and NPM. Now we are going to add another npm package to our repertoire: [axios](https://www.npmjs.com/package/axios){:target="_blank"}. We are also going to get familiar with the common HTTP protocols and status codes.

## Axios

Axios works just like `fetch()` but is a more robust. It's also a replacement because `fetch()` is only available in the browser. When we're working in Node, we're on the server so we have a need for an HTTP client, therefore we use a package like Axios. In the past, fetch has served our needs just fine and it may continue to do so for many people, but our goal here is to introduce a popular alternative.

Some notable differences:

* No more `response.json()`
* More configurable
* Custom error handling

Axios can be installed via NPM (`npm i axios`) and called just like fetch: `axios('https://someurl')`.

No matter which HTTP client you use, you will always have to deal with the same web standards/protocols for APIs:

*Before you continue, [read about HTTP requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages#HTTP_Requests){:target="_blank"}. We need to understand the methods, headers and body.*

## HTTP Requests

Each API request (using `fetch()` or `axios()`) will contain a method. These methods help computers (and humans) determine how the request is intended to function. There are four main methods:

### GET

A `GET` request tells an application that we are requesting some sort of information. This could include reading data from a database or a text file. It could also include returning a random number. It depends on what is applicable for the system. A key differentiator for this type of request is that a GET request contains no body.

```javascript
  axios.get('/user?ID=12345')
    .then(function (response) {
      // handle success
      console.log(response);
    })
```

### POST

A POST request tells an application that it needs to create something. A POST request sends along some sort of payload in the HTTP request body and the application can read that to determine what needs to be inserted into a database, saved to a file, etc.

```javascript
  axios.post('/user', {
      firstName: 'Fred',
      lastName: 'Flintstone'
    })
```

### PUT

A PUT request is an update. This method tells the application/server that something needs to be changed or updated. PUT requests will also send along a body to help the application decide what needs to be altered.

```javascript
  axios.put('/user?ID=12345', {
      firstName: 'Fred',
      lastName: 'Touchstone'
    })
```

### DELETE

A DELETE request may or may not have a body but its purpose is to remove something from an application, hence the keyword "delete".

```javascript
  axios.delete('/user?ID=12345')
    .then(function (response) {
      // handle success
      console.log(response);
    })
```

When you build an app for graduation and to get a job with these 4 methods you will have built a CRUD app: Create, Read, Update, Delete.

* [YT, Telusko - HTTP Requests](https://youtu.be/guYMSP7JVTA){:target="_blank"}

## HTTP Status Codes

Each time we send a request we will get a response back and that response will include a status code. The objective of the status code is to tell us the results of the request. For instance, a request could have been successful, failed to find information or couldn't find the desired resource/server. These codes tell us what went right and what went wrong.

* *200* - There are multiple variations of the 200 status code including 201 and 204, but generally anything in the 200 range indicates a successful response. Things went according to plan.
* *300* - Status codes in the 300s are used for caching, proxy or SEO purposes. The main one is a 301 redirect which means a resource was "moved permanently". We won't run into these codes much in this class. In fact, you won't run into them that often in your career unless you do a lot of networking related tasks.
* *400* - 400 status codes mean something went wrong with the request. There are lots of variations of these so we will cover a few. The main ones are:

  * *400* - Bad Request_: This is a generic "something is wrong" status code. You will need to change your request and try again.

  * *401* - Unauthorized_: You've likely forgotten an API key or some other Authorization header required to complete the request. This is usually temporary.

  * *403* - Forbidden_: Similar to a 401, this indicates that the server understands the request but is going to block it anyway. This is more permanent. For example: incorrect access rights.

  * *404* - Not Found_: You may have seen this one before! This means that the requested resource could not be found.

* *500* - Status codes in the 500s mean something is really wrong. A 500 (Internal Server Error) could be an uncaught exception in your code. A 502 (Bad Gateway) or a 503 (Service Unavailable) may indicate an infrastructure problem. Perhaps your server is down.

### Status Code Summary

A lot to take in? Don't worry, you'll learn these as you go. Like most things repetition helps. For this course, the two things we should take away from status codes are:

We are generally looking for a 200 (OK)
Typically the higher the number, the worse of an issue it is

## Practice It

Use [AustinCodingAcademy.com](https://austincodingacademy.com){:target="_blank"} as your request with Axios example:

<iframe width="900" height="300" src="https://austincodingacademy.com/" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen=""></iframe>

### Instructions

- [ ] On your computer, create a new folder called `sampleHTTP` and navigate to it: `cd sampleHTTP`.
- [ ] Run the command `npm init` to initialize your project. **READ THE WORDS PRINTED ON YOUR SCREEN!!**
- [ ] Accept all the default options by hitting ++enter++ over and over all the way through the last step: "Is this OK? (yes)".
- [ ] `cd sampleHTTP`: into the `sampleHTTP` folder
- [ ] `npm i axios`. Axios is the HTTP client we'll be using for this little project.
- [ ] Create a file called `index.js` in your project folder: `touch index.js`.
- [ ] Open this new directory in your text editor: `code .`
- [ ] Import axios on the first line: `const axios = require('axios')`.
- [ ] On the third line make a call to axios with the URL of ACA: `axios('https://austincodingacademy.com/')`.
- [ ] Use `.then()` to get the `response` and `console.log` it.

    ```javascript
      axios('https://austincodingacademy.com/')
        .then(function (response) {
          console.log(response)
        })
    ```
- [ ] Run the program (`node index.js`)
- [ ] What is the status code? What is the response?

  > NOTE: You're going to get a very long response, and you might not be able to scroll all the way to the top to see the status code. Try the following to get ONLY the response headers:

    ```javascript
      axios.head('https://austincodingacademy.com/')
        .then(function (response) {
          console.log(response)
        })
    ```

## Additional Resources

- [ ] [YT, Duomly - Fetch vs Axios](https://www.youtube.com/watch?v=x3yiq4bDoV4){:target="_blank"}
- [ ] [YT, Traversy Media - Axios Crash Course](https://www.youtube.com/watch?v=6LyagkoRWYA){:target="_blank"}
- [ ] [Article, LogRocket - How to Make HTTP Requests with Axios.js](https://blog.logrocket.com/how-to-make-http-requests-like-a-pro-with-axios/){:target="_blank"}
- [ ] Look ahead to the [Questions for Student Led Discussion](./../additionalResources/questionsForDiscussion/qfd-class-2.md)
- To be a successful developer you need to have the curiosity and passion to problem solve. Start practicing each night with the puzzles given to you in the [Interview Challenges](./../additionalResources/interviewChallenges.md) and start looking for others at places like [HackerRank](https://www.hackerrank.com/){:target="_blank"}, [GeeksForGeeks](https://www.geeksforgeeks.org/){:target="_blank"}, [CodeWars](https://www.codewars.com/), and [LeetCode](https://leetcode.com/){:target="_blank"}.

## Know Your Docs

Be sure to reference the Axios documentation on [NPM](https://www.npmjs.com/package/axios).

- [ ] [GitHub Repo - Axios.js](https://github.com/axios/axios){:target="_blank"}
