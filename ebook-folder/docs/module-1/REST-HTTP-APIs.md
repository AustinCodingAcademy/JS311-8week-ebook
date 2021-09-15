# Intro to RESTful APIs

*Take calculated risks. That is quite different from being rash. —George S. Patton*

## Overview

In this course, we're going to learn how to build an `API` using `Node.js` and `Express`. If you don't know exactly what an "API" is, why you'd want to build one, or how `Express` fits in, don't worry! That's why we're here.

## What's an API?

A traditional software application has a user interface(**UI**): a mechanism that allows a person to interact with the software. It may be a graphical user interface, a web-based user interface, a text-based user interface, or a voice interface. Whatever form it takes, the user interface is a way for a person to tell the software what they want to do. But what if we want to let other software interact with our application, rather than a person? A user interface built for human interaction isn't well-suited for programmatic interaction. That's where APIs come in.

**API** is an acronym that stands for **A**pplication **P**rogramming **I**nterface. In its most general sense, an API is a well-defined way for one computer program to interact with another program. More technically, an API is a set of functions and data structures that allow other application developers to leverage the functionality and/or data of your software within their own applications.

There are many different ways to implement an API, so the term can be somewhat ambiguous. There are high-level APIs and low-level APIs, internal APIs and public APIs, and so on, but in all cases they help different programs interact. Let's look at two examples.

### Example One - Native API

If you are building a desktop application that runs on macOS or Windows, you will likely want your app to have menus and buttons and windows and other familiar user interface elements. You could build these things from scratch, drawing each pixel and handling every keystroke and mouse click in your code in order to make it look and act like other software, but that's a *LOT of work*! Fortunately, the creators of macOS and Windows provided APIs that make your life as an application developer much easier. These APIs provide many functions (methods) that can help you create menus and buttons, respond to mouse clicks, etc. Other functions might help you interact with the file system or determine who is currently logged in. These APIs are building blocks that make it easier for application developers to create new software by giving your application well-defined ways to interact with the features of the operating system.

### Example Two - Web API

The HTML APIs you learned in Web 101 like Canvas, Geolocation and Drag and Drop. These are also APIs because they provide the developer(you) with functionality that can be accessed through property names like `.getContext()` or `isdraggable=`. These are built into the HTML language but not implicitly used or required, yet are available by simply knowing their property names. Pretty cool, right?

### Example Three - REST API

Let's say you're building a tourism mobile app with detailed information about the historical sites in your city. You'd also like to provide the traveler with a list of highly-rated restaurants that are near each site. You could gather this information yourself and include it in your app, but restaurants come and go, ratings change, and it's somewhat outside of the main scope of your app. Besides, other apps like Yelp already have this pretty well covered. Fortunately, Yelp provides an API that you can use to leverage their business data and ratings. Using their API, your app can search for nearby restaurants that are rated 4 stars or higher and conveniently display them alongside the site the traveler is currently viewing.

### Which Are We Building?

There's a subtle difference between the examples we just covered. In the first, your desktop app is running on a computer right alongside the operating system. Your app and the operating system can interact directly. In the second, you are accessing objects built-into the language itself. In the third example, your app is running on a smart phone. Does the person using your app need to have the Yelp app installed? Is your tourism app talking directly to the Yelp mobile app? No, it's not. Your app is using a **remote API**. It communicates with a remote server located somewhere in "the cloud". More precisely, your app communicates over the internet with server software made by Yelp, which is running on a computer in some data center, and that software was specifically designed to allow other programs to interact with it in a well-defined way.

Each of these examples can be termed APIs, but it is APIs in the third example, a remote **RESTful APIs**, that we will be building in this course, using a specific architectural style known as a REST API. We'll get into the details of **REST** APIs later. For now, just be aware that when many people say "API" they often mean this specific kind of remote API known as a **RESTful API**. But APIs come in many forms and you'll undoubtedly become familiar with many different types in your career.

Following is a short video that explains the concept of APIs and how they enable the connectivity that we have become accustomed to in modern applications.

### See It - What's An API?

<!-- !Video Content: MuleSoft Videos - What is an API? -->
<iframe width="655" height="368" src="https://www.youtube.com/embed/s7wmiS2mSXY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Practice - Explore the Star Wars API

Go to the [Star Wars API](https://swapi.dev/) site and experiment with it. The site gives you a simple UI and hints so you can try different API requests. Be sure to use the hints and see what the return values are. Visit the documentation page for a full explanation of what it offers and will allow you to do.

Here are a few things to try:

- [ ] Try retrieving a few different people by changing the id value.
- [ ] What happens if you put in an invalid id value, such as 9999?
- [ ] Can you retrieve a list of all people?
- [ ] Discover other types of information you can access, besides people.
- [ ] Do you notice any common pattern for how you use the API?

*You can [fork this CodePen](https://codepen.io/austincoding/pen/RzNaOw) or create your own repo to play with.*

## What is REST

**REST** stands for **RE**presentational **S**tate **T**ransfer. It is an architectural style—a set of guiding principles—for building distributed systems. [This site](https://restfulapi.net/) provides an overview of these principles and the history of REST. Systems that adhere to these principles are commonly said to be **RESTful**.

We're not going to focus too much on the theory behind REST. Instead, we'll focus on the practical application of REST to APIs, using common industry patterns. Still, there are a few terms and concepts that we must review.

### What is a Resource?

A **resource** is key concept in REST. It's a general term that represents any information that can be named. Resources are often the basic data entities that our APIs work with, but they can also be more abstract concepts or processes. In the Star Wars API, the resources are things like "people", "starships", and "planets".

Resources are commonly named using plural nouns. For example, to access information about the people in Star Wars, we use "people" rather than the singular "person".

By convention, resource names are usually expressed as nouns rather than verbs or actions. E.g., planets rather than `getPlanet`, or `StudentEnrollment` rather than `EnrollStudent`.

Occasionally, resources can also be more abstract concepts or processes. For example, a "StudentEnrollment" resource might be a multi-step process that updates Student and Class resources, while also enforcing rules about which classes a student can enroll in, sending notifications, and so on.

#### The URI Part

Resources are accessed using **U**niform **R**esource **I**dentifiers, or **URI**s. URIs are very similar to the familiar URL(UR Locator)) that we use on the web. There are [subtle theoretical differences between URIs and URLs that we will not concern ourselves with, but you can read more about](https://danielmiessler.com/study/url-uri/) if you're interested.

Let's revisit the URI that we used to access information about Luke Skywalker:

[`https://swapi.dev/api/people/1`](https://swapi.dev/api/people/1?format=json)

| Part| 	Explanation| 
| --- | --- |
| `https://swapi.dev/api`	| The base URL for accessing the API. This includes the protocol that will be used (https), the location of the API (swapi.dev), and a base path (/api).|
| `/people`	| The resource we're accessing, "people"|
| `/1`	| An identifier that tells the API which person we're interested in|

Here's another example.

  > Note that we don't specify an ID for any particular person. Instead, we're accessing all people.

[https://swapi.dev/api/people](https://swapi.dev/api/people?format=json)

| Part	| Explanation|
| --- | --- |
| `https://swapi.dev/api`	| The base URL for accessing the API|
| `/people`	| The resource we're accessing, "people"|

### Client-Server

You're going to hear the terms `client` and `server` a lot, so let's make sure we understand what they mean.

The client-server model is a way of distributing work among multiple parts of a software system, with the parts often (but not necessarily) running on separate computers and communicating over a network.

For example, when we click the [https://swapi.dev/api/people/1](https://swapi.dev/api/people/1?format=json) link, our web browser is the **client**. The computer at swapi.dev that sends back the data about Luke Skywalker is the **server**.

In general, software making a request is a **client**. Software that listens for requests and sends back a response is a **server**. **Request** and **response** are important concepts that we'll be working with as we build APIs.

### HTTP/HTTPS

**HTTP** is the protocol that clients and servers use to communicate on the web. HTTPS is a more secure version of HTTP in which the information being exchanged is encrypted. The first part of a URI (e.g., HTTP:) indicates which protocol is being used so the client and server know how to talk to each other—*it sets the rules for the conversation*. Technically, a REST API can use any protocol to communicate, but in practice they usually use HTTP or HTTPS.

HTTP has two types of messages: **requests** and **responses**. We won't necessarily be creating request and response messages from scratch—we have frameworks and other tools to help with that—but we will be working with some of their parts and it is good to have a mental picture of what these messages look like.

A **request** message/object is made up of the following parts:

| Part	| Explanation|
| --- | --- |
| Request Method	| Also commonly called the verb, the request method indicates what type of action we're requesting. Some commonly used methods are GET, PUT, DELETE, and POST.|
| Path	| The path to the resource that we're working with.|
| Headers	| A collection of colon-separated key-value pairs that can be used to provide additional context about the request, e.g. Content-Type: application/json (which indicates that the content of the body will be in JSON format.)|
| Body	| A payload that can be sent with the request.|

A **response** message/object has these parts:

| Part	| Explanation|
| --- | --- |
| Status Code / Message	| A numeric code and short message that indicate whether the request was successful.|
| Headers	| A collection of colon-separated key-value pairs that can be used to provide additional context about the response, e.g., Content-Type: application/json indicates that the content of the body is in JSON format.|
| Body	| A payload that can be sent with the response.|

You can find more detailed [information about HTTP here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview#Requests).

#### Interacting with a REST API

Up to this point, we've interacted with the Star Wars API by using a browser. This is convenient but limiting. The browser's address bar and links can only make one type of request, known as a **GET** request, which is used (unsurprisingly) to get a resource. But what if we want to create, update, or delete a resource? We either have to write code or use another tool. Fortunately, there is a powerful and free tool called [Postman](https://www.postman.com/) that we can use to more fully interact with REST APIs.

#### Beyond GET: HTTP Verbs

The Star Wars API was a useful starting place, but it only allows us to retrieve information. In the following video, we'll look [at another API](https://reqres.in/), provided by Ben Howdle, and dig in to the full range of request types and how they're used in REST APIs. First we'll explore the API using the interface provided by the website and then we'll use Postman to interact with the API.

<!-- !Video Content: 321: Using Postman -->
<iframe src="https://player.vimeo.com/video/344941801?byline=0&portrait=0" width="655" height="368" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

### Learning Curl!

We've learned the basics of what an API is today and touched on how to make a call but another way to make an API request is using something called `curl`. `curl` is a way to make calls using your terminal and getting information back sometimes faster and more efficiently. Its good to understand alternative ways to make requests and `curl` can be another strong choice to make requests. Simply follow these steps and you can practice using `curl`. To install `curl` you can follow instructions on their website, I included a link to the website in the additional resources section. 

- [ ] Check to see if `curl` is already installed `curl --version`
  > NOTE: curl is default command most computers already have installed. 
- [ ] If `curl` is not already installed [download `curl`](https://curl.se/docs/install.html) 
  > NOTE: If you have Homebrew installed you can also run the command `brew install curl`. 
- [ ] Check Version using command `curl --version`
- [ ] Now run command `curl https://jsonplaceholder.typicode.com/posts`

This URL is a dummy website to make practice API calls with. If you paste the URL in the browser you can see the data written in JSON. Once you run this command in the terminal you have successfully created an API request using `curl`. Feel free to visit this website and run a few more tests trying a different routes or a different type of request. We can also test this type of call by running our API route with some dummy data we can input in our files. Happy coding! 

## Additional Resources

- [ ] [Article, RestfulAPI - What is REST?](https://restfulapi.net/)
- [ ] [Article, Daniel Miessler - What’s the Difference Between a URI and a URL?](https://danielmiessler.com/study/url-uri/)
- [ ] [Req/Res API](https://reqres.in/)

## Know Your Docs

- [ ] [MDN Docs - HTTP(S) Request Object](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview#Requests)