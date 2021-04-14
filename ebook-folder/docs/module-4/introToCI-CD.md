# Intro to CI/CD

*Amazing how we can light tomorrow with today. —Elizabeth Barrett Browning*

We've learned so much in this course! From servers and RESTful APIs to Relational Databases and ER Diagrams to Authentication, Hashing, Tokens and Cookies...you should be *filled* with pride for your accomplishments!

Now that you have a general understanding of how to setup and host a database, a server, and even a front-end client (the Creact-React-App) you're going to need a way to continually add functionality to it and serve it to the world without it breaking every time you merge new features in.

In this lesson we are going to learn **Continuous Integration** & **Continuous Development** or **CI/CD**, what that entails and how to implement a low-cost technique of it using:

* GitHub as a code base repository
* GCP App Engine as our hosting solution
* and [CodeShip](https://codeship.com/) as our *code migrator* to move our app's code from the repo to the host

## Overview

**CI/CD** stands for **Continuous Integration** & **Continuous Development**. It's the process by which we automate our deployments so that we can deploy quickly and easily each time we merge new code to our `main` branch. This isn't something we build ourselves. . . instead there are tools for us to configure that help us move our code from it's repository out to the production environment of our choice(App Engine).

When talking about CI/CD you often hear the word **pipeline**. That's because the "pipeline" refers to all the possible things we can do through the CI/CD process. These things often include installing dependencies, building our production build, running a suite tests, etc. Our **pipeline** is going to be rather simple, each time a merge happens to the `main` branch, trigger an automatic migration to App Engine, re-build, and re-deploy. That's it.

The common CI/CD tools in the industry include:

* [CircleCI](https://circleci.com/)
* [Travis](https://travis-ci.org/)
* [Jenkins](https://jenkins.io/)
* [CloudBees CodeShip](https://codeship.com/)

Many of these tools offer free startup trials. We'll utilize CloudBees CodeShip's free low-tier membership.

The point of this setup is that we can commit our code to GitHub and the CI/CD integration will realize we've made a change and take the appropriate action to deploy that change. Once it's set up, life becomes very easy for us!

### See It - CloudBees CodeShip

<!-- ! Video Contents: YT, CodeShip - Intro to Codeship Basic-->
<iframe width="655" height="368" src="https://www.youtube.com/embed/yv-Jx79MQsQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Practice It

Through this course you've learned how to model data, create an ER diagram to represent your data's model and its relationships, build a SQL database, build an Express server, and add a layer of authentication to it. This is no small feat. In the coming days you will be building the foundation of your graduation app's back end. Today's homework is to:

- [ ] Draw out your dataset requirements.
- [ ] Plan and build the basis of your SQL database.
- [ ] Build the folder structure of your Express server.
- [ ] After you finish this have a glass of wine or cola or other... and know you have a great start to building the app of your dreams. We'll bring this into class and continue working on it with the help of your instructor.

<!-- ## Additional Resources

- [ ] [YT, tuber - title]() -->

## Know Your Docs

*Be sure to read over these before class.*

- [ ] [CloudBees CodeShip Docs - Home Page](https://codeship.com/)

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