# Auth0 React Sample with Random Dog

## Project setup

Use `npm` to install the project dependencies:

```bash
npm install
```

## Configuration

### Create an SPA on the Auth0 Dashboard

1. Access the Auth0 Dashboard by logging into your account, if you don't have one, [you can sign up for free by clicking here](https://a0.to/jtemporal-signup-for-auth0);
1. Go into the _Applications_ on the left-hand side menu, then select _Applications_;
1. Click _+ Create Application_ button;
1. Give your application a name (I picked "dogfy" for the name of my app) then select _Single Page Application_, then click create, this will take you to the application details page;
1. Move to the _Settings_ tab and set your _callback urls_ and your allowed _logout urls_ to `https://localhost:3000`;

Now you've configured everything you needed on the Auth0 Dashboard to get your app up and running.

### Configure credentials

The project needs your Auth0 domain and client ID in order for the authentication flow to work.

To do this, first copy `src/auth_config.json.example` into a new file in the same folder called `auth_config.json`, and replace the values with your own Auth0 application credentials:

```json
{
  "domain": "YOUR_AUTH0_DOMAIN",
  "clientId": "YOUR_AUTH0_CLIENT_ID"
}
```

## Run the sample

### Compile and hot-reload for development

This compiles and serves the React app and starts the backend API server on port 3000.

```bash
npm start
```

## Action Code

Add the `axios` module in the _Modules_ tab on the Action editor. Then update the action code itself to contain the following code.

```javascript
exports.onExecutePostLogin = async (event, api) => {
  const axios = require("axios");

  const randomDog = await axios.get("https://dog.ceo/api/breeds/image/random");

  if (event.authorization) {
    api.idToken.setCustomClaim("https://dogfy.com/random_dog", randomDog.data.message);
  }
};
```

Then _Deploy_ the action and drag it into the flow.
