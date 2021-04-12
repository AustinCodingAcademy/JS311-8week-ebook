# Authentication with Auth0

As you've seen in the code snippets, there are third-party systems that most (small/medium size) businesses use to secure their Node.js applications without writing all of that logic themselves. It's important to know the concepts though and that's why it was introduced. With that being said, it's time to introduce [Auth0](https://auth0.com/)!

We're going to do this section tutorial-style since it's the easiest way to follow along. To start . . . the first thing we need to do is create an Auth0 account. Since Auth0 is a third-party application, they require registration and you can do that here: [https://auth0.com/signup](https://auth0.com/signup).

- [ ] All you need is an email and password and you can get a free account to work with.

- [ ] While you're signing up, leave all default options until you get to the "account type" section and then choose "personal". If prompted, select any "role" and "challenge" you want and click "Create Account".

- [ ] After your account is created you need to go to the "APIs" section and create an API associated with your specific project. So navigate to your dashboard: [https://manage.auth0.com/dashboard/us/](https://manage.auth0.com/dashboard/us/dev-t4vriwms/apis), select "APIs" from the left menu, and click "CREATE API". The system will ask you for three things: `Name`, `Identifier`, and `Signing Algorithm`. Leave the signing algorithm alone use the following:

```console
  Name: My Express App

  Identifier: my-express-app
```

- [ ] Click "CREATE".

- [ ] Finally, in the upper right-hand corner where your avatar is . . . click the icon and then click settings. On the main page (under the "General" tab) scroll down until you see "API Authorization Settings". Set the default directory to "Username-Password-Authentication" and save your changes. This will help us avoid authentication problems later.

- [ ] Now that we have our Auth0 account set up we are going to leave the integration with our Node.js app for class work time. If you want to get ahead and really understand what's going on here we would recommend the following Auth0 tutorial:

- [ ] [Tutorial, Auth0 - Secure Express Server](https://auth0.com/blog/node-js-and-express-tutorial-building-and-securing-restful-apis/)

  > Authentication with Auth0 is a way to safely handle authentication. With tools like becrypt or argon2 we can store hashes and use Auth0 to save our usernames and passwords securely and safely.
  
## Additional Resources

- [ ] [YT, Traversy Media - Node.js API Authentication with JWT](https://youtu.be/7nafaH9SddU)

## Know Your Docs

- [ ] [JWT Docs - Home Page](https://jwt.io/)
- [ ] [Tutorial, Auth0 - Node, Express, Authentication](https://auth0.com/blog/create-a-simple-and-secure-node-express-app/)