# How to Make Secure HTTP Requests with Vue and Express

This is an example of how you can make secure API calls to an Express API from a Vue client. It uses Auth0 to secure the Express API and also to allow users to register and login to the Vue application.

You can clone this project and follow the directions below or [check out the tutorial](https://auth0.com/blog/how-to-make-secure-http-requests-with-vue-and-express/) where I cover everything step by step!

![Vue events app](https://cdn.auth0.com/blog/vue-meetup/vue-event-app-home.png)

## Project setup

First, clone this repo and switch into the repo folder:

```bash
git clone git@github.com:auth0-blog/vue-express-auth.git
cd vue-express-auth
```

Now you need to install the dependencies for the client and server code.

### Set up the Express server

```bash
cd server
npm install
```

### Set up the Vue client

In a new terminal tab:

```bash
cd ../client
npm install
```

## Configuring Auth0

You're going to use Auth0 to add authentication to the app.

First, [sign up for a free Auth0 account](https://auth0.com/signup). Once you're registered, you'll be taken to the [Auth0 management dashboard](https://manage.auth0.com/dashboard/).

### Create the Auth0 application

Click on the big red button that says "Create Application". 

Name it "Vue Events" (or anything you'd like), click on "Single Page Web Applications" for "application type", and press "Create".

![Auth0 Dashboard](https://cdn.auth0.com/blog/vue-meetup/auth0-create-app.png)

Now click into "Settings" and fill in some information that Auth0 needs to configure authentication:

**Allowed Callback URLs** &mdash; `http://localhost:8080`

**Allowed Logout URLs** &mdash; `http://localhost:8080`

**Allowed Web Origins** &mdash; `http://localhost:8080`

Scroll down and click "Save Changes".

### Create the Auth0 API

Next, click on "APIs" on the left menu. Click "Create API" and call it "Vue Express API" (or anything you'd like). For "Identifier", we recommend a URL such as `https://vue-express-api.com`. It doesn't have to be a publicly available URL and we'll never call it, it's just for naming purposes. You can leave "Signing algorithm" as is and then press "Create".

That's all you need from the dashboard for now, but don't click out yet. You'll need to pull some of these values from the dashboard into your application soon.

In the `client` directory, create a file for the config values:

```bash
touch auth_config.json
```

> **Important:** Make sure you add `auth_config.json` to your `.gitignore` file!

### Connecting with Auth0

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
* Copy the value for "Identifier" and paste it into `audience` in `auth_config.json`
* Click on "Applications" and select your application (Vue Events)
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

### Testing the app

Now that everything is set up, you can test the app.

**Run the server**

Make sure you're in the `server` directory in your terminal and start the server with:

```bash
npm start
```

Server is running at [http://localhost:8000](http://localhost:8000).

**Run the client**

In your other tab, make sure you're in `client` and run:

```bash
npm run serve
```

You can view the Vue app in the browser at [http://localhost:8080](http://localhost:8080).
 
You can now also sign in, receive an API access token, and view an event's details page at [http://localhost:8080/event/1](http://localhost:8080/event/1).

Be sure to [check out the full tutorial](https://auth0.com/blog/how-to-make-secure-http-requests-with-vue-and-express/) to see how this process works.
