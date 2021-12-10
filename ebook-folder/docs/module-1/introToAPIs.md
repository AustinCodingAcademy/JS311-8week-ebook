# Intro to RESTful APIs

*Take calculated risks. That is quite different from being rash. —George S. Patton*

## Overview

In this course, we're going to learn how to build an **API** using **Node.js** and **Express**. If you don't know exactly what an "API" is, why you'd want to build one, or how **Express** fits in, don't worry! That's why we're here.

## What's an API?

A traditional software application has a User Interface(**UI**): a mechanism that allows a person to interact(interface) with a computer; these include: Graphical User Interfaces (GUIs), a Web-Based User Interfaces, a Text-Based User Interfaces like a command line, or a Voice Interface like Siri. Whatever form it takes, the UI is a way for a human person to tell the computer what they want it to do. But what if we want the computer to interact with other computers? A user interface built for human interaction isn't well-suited for programmatic interaction because it takes keystrokes and mouse clicks... that's where APIs come in.

**API** is an acronym that stands for **A**pplication **P**rogramming **I**nterface. In its most general sense, an API is a well-defined way for one computer program to interact with another program. More technically, an API is a set of functions and data structures that allow other application developers to leverage the functionality and/or data of other software within their own software applications.

There are many different ways to implement an API, so the term can be somewhat ambiguous. There are high-level APIs and low-level APIs, internal APIs and public APIs, and so on, but in all cases they help different programs interact. Let's look at two examples.

### Example One of an API - Native APIs

If you are building a desktop application that runs on macOS or Windows, you will likely want your app to have menus, buttons, windows and other familiar user interface elements. You could build these things from scratch, drawing each pixel and handling every keystroke and mouse click in your code in order to make it look and act like other software, but that's a *LOT of work*!

Fortunately, the creators of macOS and Windows provided APIs that make your life as an application developer much easier. These APIs provide many functions (methods) that can help you create menus and buttons, respond to mouse clicks, etc. Other functions might help you interact with the file system or determine who is currently logged in. These APIs are building blocks that make it easier for application developers to create new software by giving your application well-defined ways to interact with the features of the operating system.

### Example Two of an API - Web API

The HTML APIs you learned in Web 101 like **Canvas**, **Geolocation**, **Drag and Drop**, etc. These are also APIs because they provide the web developer(you) with functionality that can be accessed through property names like `.getContext()` or `isdraggable=`. These are built into the HTML language but not implicitly used or required, yet are available by simply knowing their property names. Pretty cool, right?

### Example Three of an API - REST API

Let's say you're building a tourism mobile app with detailed information about the historical sites in your city. You'd also like to provide the traveler with a list of highly-rated restaurants that are near each site. You could gather this information yourself and include it in your app, but restaurants come and go, ratings change, and it's somewhat outside of the main scope of your app. Besides, other apps like Yelp already have this pretty well covered. Fortunately, Yelp provides an API that you can use to leverage their business data and ratings. Using their API, your app can search for nearby restaurants that are rated 4 stars or higher and conveniently display them alongside the site the traveler is currently viewing.

### Which Are We Building?

There's a subtle difference between the examples we just covered. In the first, your desktop app is running on a computer right alongside the operating system. Your app and the operating system can interact directly. In the second, you are accessing objects built-into the language itself. In the third example, your app is running on a smart phone. Does the person using your app need to have the Yelp app installed? Is your tourism app talking directly to the Yelp mobile app? No, it's not. Your app is using a **remote API**. It communicates with a remote server located somewhere in "The Cloud". More precisely, your app communicates over the internet with server software made by Yelp, which is running on a computer in some data center("The Cloud"), and that software was specifically designed to allow other programs, like yours, to interact with it in a well-defined way.

Each of these examples can be termed APIs, but it is APIs in the third example, a remote **RESTful APIs**, that we will be building in this course, using a specific architectural style known as REST, **Representational State Transfer**. We'll get into the details of **REST** APIs later. For now, just be aware that when many people say "API" they often mean this specific kind of remote API known as a **RESTful API**. But APIs come in many forms and you'll undoubtedly become familiar with many different types in your career.

Below is a short video that explains the concept of APIs and how they enable the connectivity that we have become accustomed to in modern applications.

## See It - What's An API?

<!-- !Video Content: MuleSoft Videos - What is an API? -->
<iframe width="655" height="368" src="https://www.youtube.com/embed/s7wmiS2mSXY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Practice - Explore the Star Wars API

Go to the [Star Wars API](https://swapi.dev/) site and experiment with it. The site gives you a simple UI and hints so you can try different API requests. Be sure to use the hints and see what the return values are. Visit the documentation page for a full explanation of what it offers and will allow you to do.

Here are a few things to try:

- [ ] Try retrieving a few different people by changing the id value.
- [ ] What happens if you put in an invalid id value, such as 9999?
- [ ] Can you retrieve a list of all people?
- [ ] Discover other types of information you can access, besides people.
- [ ] Do you notice any common pattern for how you use the API?

*You can [fork this CodePen](https://codepen.io/austincoding/pen/RzNaOw) or create your own repo to play with.*

## Additional Resources

- [ ] [Req/Res API](https://reqres.in/)
- [ ] [YT, Programming With Mosh - What is a REST API](https://www.youtube.com/watch?v=SLwpqD8n3d0)
- [ ] [Tutorial - Guiding Principles of REST](https://restfulapi.net/)

## Know Your Docs

- [ ] [MDN Docs - Intro to Web APIs](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Introduction)
- [ ] [MDN Docs - Third-Party APIs](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Third_party_APIs)
- [ ] [MDN Docs - REST](https://developer.mozilla.org/en-US/docs/Glossary/REST)