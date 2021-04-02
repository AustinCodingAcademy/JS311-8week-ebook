# Node Recap

*He who moves not forward goes backward. —Johann Wolfgang von Goethe*

## Overview

In this class we are going to be focused on creating and deploying APIs with Node.js and Express. Hopefully we are starting to feel quite comfortable using Node but we will spend the first class recapping/summarizing our knowledge of Node and NPM so that we can really hit the ground running in the coming weeks.

## JavaScript, why?

JavaScript was originally designed to work on the web and so it only ran in browsers (Chrome/Safari/IE). Its purpose was to add functionality to websites to make them interactive and it has been very successful in this regard. Eventually, experts in the language decided they wanted to take the benefits of JavaScript and use them OUTSIDE of a web browser, for example on a server, and thus Node.js was born. Node.js is an open-source environment that executes JavaScript outside of a web browser.

Why? While there are many benefits of using JavaScript, we'll focus on the big one for you as the developer. You may have heard the term fullstack used in the software industry to reference a person who works on both the frontend and the backend. The frontend almost always includes JavaScript while the backend could be any assortment of server-side languages such as Java, C# or Python. Because of this, many traditional full-stack developers were proficient in at least two languages. Adding Node.js into that mix allows the developer to focus on only one, JavaScript. With Node.js, we can run JavaScript on both the client side and the server.

### See It - What is Node.js

<!-- ! Video Conent: Programming with Mosh - What is Node.js -->
<iframe width="655" height="368" src="https://www.youtube.com/embed/uVwtVBpw7RQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Practice It

- [ ] Open the Repl.it below.
- [ ] Alter the function to include functionality for an international phone number. Ex. (+1).
- [ ] Add one number to the beginning of the array to support this.
- [ ] Additionally, remove all formatting (besides the +) from the phone number such that the result is returned as `+19775631212`. This should make the logic of the function very simple.

Without the advent of Node.js, we wouldn't be able to use JavaScript as a scripting language in the terminal as we can here in this Repl.it example or in our own terminal on our personal machine.

<iframe height="600px" width="100%" src="https://repl.it/@MattViteri/TenderHorizontalUnits?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

#### Try It on Your Personal Machine

- [ ] By the time you come to this course you should have installed Node.js and be able to type into your terminal/bash `node -v` to get the current version of Node.js you have installed and running.
- [ ] On your desktop, create a file called: `myTestFile.js` and open it with your text editor, VS Code or your preference.
- [ ] Copy/paste the code from the Repl.it into that file, save, and return to your terminal/bash.
- [ ] `cd desktop` to change into your Desktop directory.
- [ ] Run the command `node myTestFile.js` + ++enter++
- [ ] You should see the same results you saw in the Repl.it online terminal.
- [ ] Now delete the file `myTestFile.js` to keep your desktop clean and organized.

This is the power of Node.js. Without it, JavaScript couldn't be run outside of your browser.

#### Try it in the Browser

- [ ] Now go back to Chrome and type ++cmd+option+i++ or ++ctrl+shift+i+ to open your dev tools tray.
- [ ] Navigate to the console.
- [ ] Copy/paste the `formatPhone` function into the console  and hit ++enter++.
- [ ] Copy/paste the invocation of the function `formatPhone([9, 7, 7, 5, 6, 3, 1, 2, 1, 2])` and hit ++enter++.
- [ ] You should get the exact same return value.

It's important to note the difference in the environment. If you built a web page like you did in 101 and added functionality to it with JavaScript, the code was running in the browser. But if you were running unit tests on your terminal apps like you did in JS211, your JavaScript code was running in the Node environment. Without having to switch between a front-end scripting language and a back-end programming language we can focus all of our attention on one language, JavaScript. So let's get really good with JavaScript in this course!!

## NPM

NPM stands for *Node Package Manager*. It also stands for *Not Pancake Mix* or any other assortment of clever acronyms developers can think of, and it's become something of a running joke on their website. The purpose of this tool is to allow you to integrate third-party code into your application. Third-party code means code another developer has written and published to NPM. Many developers in the open-source community work on projects that will benefit the masses and these projects can be downloaded via NPM and used in your project. A *package.json* file keeps track of all the packages you are currently using in your current project.

  > If you were building with Python and `pip`(the Python equivalent of `npm`) you would see all of your code packages in a `requirements.txt` file.

### See It - NPM

<!-- ! Video Content: Viktor Dozal - What is npm? -->
<iframe width="655" height="368" src="https://www.youtube.com/embed/ZNbFagCBlwo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Practice It: NPM

We are going to practice creating a new project with NPM. When complete, we will have a new folder with a `package.json` file inside and we will have included an external package in our project to tinker with.

- [ ] Navigate to your desktop: `cd desktop` + ++enter++.
- [ ] Create a new folder called `"sampleProject"`: `mkdir sampleProject` on your desktop.
- [ ] Navigate to it `cd sampleProject` + ++enter++.
- [ ] Run the command `npm init` to initialize your project. READ THE WORDS PRINTED ON YOUR SCREEN!!
- [ ] Accept all the default options by typing ++enter++ over and over all the way through the last step: "Is this OK? (yes)".  -> ++y+enter++
- [ ] `ls` on Mac or `dir` on Windows and you will see `package.json`, right?
- [ ] Let's install [moment](https://www.npmjs.com/package/moment), a date/time package by typing `npm i moment`.
- [ ] Now open the `sampleProject` folder in your text editor. Do you see moment listed in your `package.json` file?
- [ ] Do you see a new folder called "`node_modules/`"? This folder keeps up with all of our third-party code packages.
- [ ] Now, create a file called `index.js` in your project folder.
- [ ] Import moment into the file by copy/pasting: `const moment = require('moment')` on the first line.
- [ ] On the third line create a variable for the current day: `const day = moment().format('dddd')`.
- [ ] On the fifth line log a message for the user that tells them what day it is: `console.log('Today is', day)`.
- [ ] Use our Node environment to run the code: `node index.js`.

## Know Your Docs

- [ ] [Node Docs - Nodejs.org](https://nodejs.org/en/docs/)
- [ ] [NPM Docs - Moment.js](https://www.npmjs.com/package/moment)