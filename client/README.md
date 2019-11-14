# Vue Events App w/ Authentication

This is a simple Vue website that demonstrates how to get started with Vue.js, add authentication, and restrict certain pages from users who aren't logged in. You can clone this project and follow the directions below or [check out the tutorial](https://auth0.com/blog/beginner-vuejs-tutorial-with-user-login/) where I cover all the deets step by step!

![Vue events app](https://cdn.auth0.com/blog/vue-meetup/vue-event-app-home.png)

## Project setup

```bash
git clone https://github.com/hollylawly/vue-events-auth.git
npm install
npm run serve
```

View it in the browser at [http://localhost:8080](http://localhost:8080).

## Adding Authentication to our Vue App

We're going to use Auth0 to add authentication to the app.

First, [sign up for a free Auth0 account](https://auth0.com/signup). Once you're registered, you'll be taken to the [Auth0 management dashboard](https://manage.auth0.com/dashboard/).

Click on the big red button that says "Create Application". 

Name it "Vue Events" (or anything you'd like), click on "Single Page Web Applications" for "application type", and press "Create".

![Auth0 Dashboard](https://cdn.auth0.com/blog/vue-meetup/auth0-create-app.png)

Now click into "Settings" and fill in some information that Auth0 needs to configure authentication:

**Allowed Callback URLs** &mdash; `http://localhost:8080`
**Allowed Logout URLs** &mdash; `http://localhost:8080`
**Allowed Web Origins** &mdash; `http://localhost:8080`

That's all we need from the dashboard for now, but don't click out yet. We'll need to pull some of these values from the dashboard into our application soon.

Create a file (and add to `.gitignore`) for the config values:

```bash
touch auth_config.json
```

Now open up `auth_config.json` and paste in:

```js
{
  "domain": "your-domain.auth0.com",
  "clientId": "yourclientid"
}
```

**Finding your `auth_config` values:**

* Head to the [Auth0 dashboard](https://manage.auth0.com/dashboard)
* Click on "Applications" and select your application
* Click on "Settings"
* Copy the value for "Domain" and paste it into `domain` in `auth_config.json`
* Copy the value for "Client ID" and paste it into `clientId` in `auth_config.json`

Now you should be able to sign in to the application and access single event details.
