# Intro to Hosting

*When the best things are not possible, the best may be made of those that are. —Richard Hooker*

We've spent a lot of time in this course learning how to build APIs and we've practiced interfacing with these mostly through Postman on LOCALHOST.

  > As a reminder, localhost is basically a local server that we run our code on for testing and development purposes.
  
But what about when we want to get into production, actually serving our data and API to the public? Other people will need to access our application from wherever they are in the world and for that we need to learn about hosting. Now that we understand authentication we can safely do this!

## Overview

Hosting is the process of making your application accessible to the internet. In the past, this involved buying a piece of hardware (a server), deploying your application to that server and creating your own firewall rules so that people could interface with your site or API. Nowadays there are numerous cloud services that do these types of things for us. One of those services is GCP, and since we have already used GCP to create our database, we will continue working with this technology.

As a recap, Google Cloud Platform (GCP) is a service that allows us access to the hundreds of thousands of servers that Google uses to run its business. Amazon Web Services (AWS) works in a very similar way. When these big companies have extra server space they rent out the resources to us so that we can make use of them for our projects. So when we say the servers are "in the cloud", we really just mean that the actual hardware lives somewhere else and is configurable over the internet. We are going to use some of these resources to "host" our API.

## App Engine

App Engine is one of the most popular tools that GCP(Google Cloud Platform) provides. All we need to do is deploy our code and App Engine takes care of the rest. If your website or API receives a sudden burst of traffic, App Engine will add more resources as necessary to handle it. We don't need to know everything about the internals of this tool, just that it makes a lot of sense for deploying an API. Other documentation will be provided so that you can do more research.

  > Think about how you would have to scale servers without using the cloud. Think how slow your local server can be just running singular requests. Now think about the multiple requests per second of say, Lyft, Walmart or Amazon.

### See It - App Engine

<!-- ! Video Contents: YT, Google Developers - What is App Engine? -->
<iframe width="655" height="368" src="https://www.youtube.com/embed/s1g4H4-MSJg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Practice It

  > IMPORTANT NOTE: The following tutorial, while a helpful introduction, is slightly outdated. Pay careful attention to all the steps below.

- [ ] Navigate to this [App Engine tutorial](https://medium.com/google-cloud/hosting-your-personal-website-on-google-cloud-platform-for-beginners-278543eaaa67)
- [ ] Follow the instructions for getting a sample app set up on App Engine using your Google Cloud account.
  *  [ ] Under **"Let's Get Started"**:
    *  [ ] Ignore the step that says to click the icon that looks like a pencil. Your terminal will already be open to where it needs to be.
  *  [ ] Under **"Time to write some code!"**
    *  [ ] Instead of `cd nodejs-docs-samples/appengine/hello-world`, type (or copy/paste) the following: `cd nodejs-docs-samples/appengine/hello-world/standard`
    *  [ ] Instead of `npm install && npm start`, type `npm install && node app.js`
- [ ] [How do you add `.env` variables](https://medium.com/@brian.young.pro/how-to-add-environmental-variables-to-google-app-engine-node-js-using-cloud-build-5ce31ee63d7?)

## Additional Resources

- [ ] [Article, Website.com - What is hosting?](https://www.website.com/beginnerguide/webhosting/6/1/what-is-web-hosting?.ws)

## Know Your Docs

- [ ] [GCP Docs - App Engine](https://cloud.google.com/appengine/)
- [ ] [Tutorial, Medium - Hosting on GCP](https://medium.com/google-cloud/hosting-your-personal-website-on-google-cloud-platform-for-beginners-278543eaaa67)

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