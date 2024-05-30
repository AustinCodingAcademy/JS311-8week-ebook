# MySQL Workbench Setup

## Overview

We've just learned to use that tool called Postman. What that tool allows us to do is quickly test our server app without having to build a front-end app or use the `curl` command in our terminals. This is really handy because you can just focus on your server app, prove that routes work the way they're expected to and then build your front-end app using those same requests you prepare in Postman.

In the same way, when we're building a database we don't want to worry about our server app code being buggy when we're proving that our database is setup and accepted requests as expected; we just want to prove the database is working then we can connect our server to it.

The Database equivalent of Postman is [MySQL Workbench](https://www.mysql.com/products/workbench/){:target="_blank"}. It's a stand-alone tool that allows us to setup, connect, query and manage a MySQL database with a graphical user interface (GUI). We are going to download this tool and connect to your database in GCP (Google Cloud Platform) now.

## Practice It

### Download MySQL Workbench

- [ ] Navigate to [MySQL Workbench download](https://www.mysql.com/products/workbench/){:target="_blank"}
- [ ] Click "Download Now"
- [ ] At the bottom of the page select your system specs (Mac, Windows)
- [ ] Click the "download" button again and then click "No thanks, just start my download" on the next page
- [ ] When the download completes, install MySQL Workbench
- [ ] Start MySQL Workbench.

=== "For Windows Users"

    <iframe width="560" height="315" src="https://www.youtube.com/embed/12j-tiRpXX4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

=== "For Older Mac Users"

    * download an early version of the workbench: 
        - [https://downloads.mysql.com/archives/workbench/](https://downloads.mysql.com/archives/workbench/)
    * and/or use this guide: 
        - [https://www.macminivault.com/install-mysql-on-macos-high-sierra/](https://www.macminivault.com/install-mysql-on-macos-high-sierra/)

### Connect MySQL Workbench

Watch the video below on connecting and using the MySQL Workbench. The instructor is using Windows but it works the same for Macs.

Your goal is to be able to connect to this pre-existing database:

```console
  Host: den1.mysql1.gear.host
  User: aca311week3day1
  Password: Wq87E!7mUF~7
```

<!-- ! Video Content: YT, Woo@ACA - Connect and Use MySQL Workbench -->
<iframe width="655" height="368" src="https://www.youtube.com/embed/8lMCudSTnOU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Know Your Docs

- [ ] [MySQL Docs - Home Page](https://dev.mysql.com/doc/){:target="_blank"}
