# Hosting a Database on Google Cloud Platform

## Overview

While we could run a database on our local computer the same way we've been running our server app on our computer this isn't a good idea simple because we'll soon be running a front-end app on our computer while developing. THAT WOULD BE 3 APPS running on our computer while we're still coding....not a good idea.

In addition, we want our data to persist on a computer that's available globally, literally globally to all those with an internet connection. To do this we need to put our data in a database that is hosted on a service like Azure, AWS, or Google Cloud (GCP). The video below shows you how to sign-up and use GCP to host a MySQL database but before you jump into that let's first get a big picture of what we're doing.

## The Big Picture

We're learning how to build servers using Express.js. These servers will serve data to our front-end app we build in 411, thus a full-stack application. But we need to have a database to keep up with our data. Today you're going to sign-up for a GCP account and get free credit to run what's called a **virtual machine**(VM). This is going to be called an **instance** in the video below.

The instance will work just like your personal computer. It will be a computer running on a very large computer somewhere in the world. This credit will go toward paying for that computer to run and accept requests.

Once your server is build you'll host it on GCP, AWS, Heroku, or where ever. This too will be on a computer/virtual machine that is running and accepting requests and sending requests to your database.

Then you'll build your front-end app using React. This will also be its own app and will need to run on a virtual machine somewhere like AWS, Azure, etc.

All of this costs money! Hosting apps and websites is not free. It costs money. We introduce you to GCP because it's an industry standard like Azure and AWS. As you move through this program you will likely run our of credit. Don't agree to pay for more and you **won't** be charged more!

However, as you approach graduation you might need to move your DB, Server App, and Front-end(Client) app from GCP to Heroku or AWS to save money. This is totally fine and we have instructions for both. Please talk to your instructors and mentors to make sure you're not paying too much money.

## Sign-up and Setup a Database on GCP

<!-- ! Video Contents:  YT, Jon@ACA - Sign-up and Setup GCP -->
<iframe width="655" height="368" src="https://www.youtube.com/embed/ypQaSyICc3A" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
