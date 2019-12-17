# How to Make Secure HTTP Requests with Vue and Express

This is an example of how you can make secure API calls to an Express API from a Vue client. It uses Auth0 to secure the Express API and also to allow users to register and login to the Vue application.

You can clone this project and follow the directions below or [check out the tutorial](https://auth0.com/blog/how-to-make-secure-http-requests-with-vue-and-express/) where I cover everything step by step!

![Vue events app](https://cdn.auth0.com/blog/vue-meetup/vue-event-app-home.png)

## Project setup

First, clone this repo:

```bash
git clone https://github.com/hollylawly/vue-express-auth.git
```

Now you need to install the dependencies for the client and server code and get everything running. It won't run properly until you fill in the Auth0 values, but you can still start everything up now.

### Set up the Express server

```bash
cd server
npm install
npm start
```

Server is running at [http://localhost:8000](http://localhost:8000).

### Set up the Vue client

In a new terminal tab:

```bash
cd ../client
npm install
npm run serve
```

View it in the browser at [http://localhost:8080](http://localhost:8080).

## Configuring Auth0

We're going to use Auth0 to add authentication to the app.

First, [sign up for a free Auth0 account](https://auth0.com/signup). Once you're registered, you'll be taken to the [Auth0 management dashboard](https://manage.auth0.com/dashboard/).

### Create the Auth0 application

Click on the big red button that says "Create Application". 

Name it "Vue Events" (or anything you'd like), click on "Single Page Web Applications" for "application type", and press "Create".

![Auth0 Dashboard](https://cdn.auth0.com/blog/vue-meetup/auth0-create-app.png)

Now click into "Settings" and fill in some information that Auth0 needs to configure authentication:

**Allowed Callback URLs** &mdash; `http://localhost:8080`

**Allowed Logout URLs** &mdash; `http://localhost:8080`

**Allowed Web Origins** &mdash; `http://localhost:8080`

### Create the Auth0 API

Next, click on "APIs" on the left menu. Click "Create API" and call it "Vue Express API" (or anything you'd like). For "Identifier", we recommend a URL such as `https://vue-express-api.com`. It doesn't have to be a publicly available URL and we'll never call it, it's just for naming purposes. You can leave "Signing algorithm" as is and then press "Create".

That's all we need from the dashboard for now, but don't click out yet. We'll need to pull some of these values from the dashboard into our application soon.

Create a file (and add to `.gitignore`) for the config values:

```bash
touch auth_config.json
```

Now open up `auth_config.json` and paste in:

```js
{
  "domain": "your-domain.auth0.com",
  "clientId": "your-client-id",
  "audience": "https://your-identifier.com"
}
```

**Finding your `auth_config` values:**

* Head to the [Auth0 dashboard](https://manage.auth0.com/dashboard)
* Click on "APIs" and select your API
* Copy the value for "Identifier" and past it into `audience` in `auth_config.json`
* Click on "Applications" and select your application
* Click on "Settings"
* Copy the value for "Domain" and paste it into `domain` in `auth_config.json`
* Copy the value for "Client ID" and paste it into `clientId` in `auth_config.json`

Now you should be able to sign in to the application, but you still won't be able to access single event details because you need to add this information to the server side where the API access token is validated.

Open up `server/server.js` and find:

```js
const authConfig = {
    domain: "YOUR-DOMAIN",
    audience: "YOUR-IDENTIFIER"
};
```

Replace the `domain` and `audience` placeholders with the values listed above.

Now you can sign in, receive an API access token, and view an event's details page at [http://localhost:8080/event/1](http://localhost:8080/event/1).

Be sure to [check out the full tutorial]() to see how this process works.
