# particle-firebase-ui

### Introduction

A [Bootstrap](http://getboostrap.com) framework for building a [Particle.io](http://particle.io) IoT cloud connected web app, with persistent storage and management of access tokens using [Firebase](http://firebase.google.com).

### Requirements

- A [Firebase](http://firebase.google.com) project
- [`firebase-tools`](https://firebase.google.com/docs/cli/) npm package for testing and deploying the project
- A [Particle.io](http://particle.io) device and account for testing

### Setup

- In the [`./public/index.html`](./public/index.html) file, change the Firebase script tag to use your API keys and settings, from the _Add Firebase to your web app_ window in your Firebase console
- Configure your Firebase app for Google OAuth authentication. Go to the app's Firebase console, and then enable the `Google` sign-in method in the `Auth` section
- From the root of this repository, run the `firebase init` npm command to tie your copy of the repo to your Firebase project
- Test your app by running the `firebase serve` npm command from the root of this repository
- Deploy your app to Firebase hosting with `firebase deploy`. Don't forget to also deploy the database rules, or your users' access tokens will be publicly accessible!

### How It Works

When a user logs in to this app's main page, they are asked to log in to their Particle.io account. This will create a non-expiring access token for that Particle.io account and save it to your Firebase. (It's secure, if you use the provided `database.rules.json` Firebase security rules.) The user can then add individual devices tied to that account to your Firebase, so that you can track them by device ID, and retrieve other device information. Device information is updated in your Firebase every time the user logs in.

All data is stored in the `ParticleBase/users` tree in your Firebase.

When the user selects a device, the `deviceSelectCallback` function in (`./public/js/app.js`)[./public/js/app.js] is fired, with a device object as the parameter. At any point, you may access the user's Firebase authenticated user information, a device list and the access token in the `ui.profile` object. The token will be needed to call any cloud functions from the [Particle.io Javascript Library](https://docs.particle.io/reference/javascript), included in this project.