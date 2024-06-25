# Google Authentication Setup

## Steps to Obtain Client ID & Client Secret

### Step 1: Open the Google Developer Console
Open [Google Developer Console](https://console.developers.google.com/) and you will be directed to this page:

![Step 1](https://drive.google.com/uc?export=view&id=1u71-OriOL1XNGPDlRBPLIUOJUzHDhHVv)

### Step 2: Access Projects Dropdown
Click on the **dropdown of Projects**:

![Step 2](https://drive.google.com/uc?export=view&id=1goWq-VO_jgRhYrMsk9aTZrimcSTNGfzx)

### Step 3: Create a New Project
Tap on **New Project** as shown below:

![Step 3](https://drive.google.com/uc?export=view&id=1Pic7uCu4uSVDX5ZlKA81L4ZP5BixtWIM)

### Step 4: Add Project Name
Create a **New Project** by adding a Project name:

![Step 4](https://drive.google.com/uc?export=view&id=1TnoHVS6waMv29dP9l78pNzWy-G6v18md)

### Step 5: Select Your Project
You will be directed to the dashboard. Go to the projects dropdown and select your project:

![Step 5](https://drive.google.com/uc?export=view&id=1c9hn4qLy9kEr2Hu9aqgVRz-RcA3vBM5e)

### Step 6: Navigate to Credentials
Click on the **Credentials** option and then click on the **create credentials** button in the credentials page:

![Step 6](https://drive.google.com/uc?export=view&id=1LQ5ZNAML6N2TWvOn0Yax0DCENc66DIt0)

### Step 7: Create OAuth Client ID
Click on **OAuth Client ID** and then click on the **create credentials** button in the credentials page:

![Step 7](https://drive.google.com/uc?export=view&id=1KNPBw_gk01oaL6113P_zet0otlC4LMRy)

### Step 8: Configure Consent Screen
Click on the **Consent screen** button:

![Step 8](https://drive.google.com/uc?export=view&id=1Ckfxc5N7LzKT5rywXMQ5_pAWmrH4HOLT)

### Step 9: Set User Type and Create App Registration
Select the User Type **External** and complete the app registration:

![Step 9](https://drive.google.com/uc?export=view&id=1aSDd_3Da7oCX-kZrCS_2phr4y4-uCqUR)

### Step 10: Add App Information
Add the **App information name** and **user mail**:

![Step 10](https://drive.google.com/uc?export=view&id=1K3GKLjgXdc4wLgNMTcwlvp6N6jTo9jZ7)

![Step 10](https://drive.google.com/uc?export=view&id=1XjTG7cxfuoE4-3-ZoIKQFcyqWXkUH5NW)

### Step 11: Save and Continue
Click **SAVE AND CONTINUE** for the next scope and test users:

![Step 11](https://drive.google.com/uc?export=view&id=1G7Yqy7X-7CJACX-BefciVC-zEtzxVF7t)

![Step 11](https://drive.google.com/uc?export=view&id=1obpi2DMigkPEjhSBs5Yg_CUKm9samFBF)

### Step 12: Create OAuth Client ID Again
Click on the **Credentials** option and then click on the **create credentials** button again in the credentials page:

![Step 12](https://drive.google.com/uc?export=view&id=1LQ5ZNAML6N2TWvOn0Yax0DCENc66DIt0)

### Step 13: Create OAuth Client ID Again
Click on **OAuth Client ID** and then tap on the **create credentials** button in the credentials page:

![Step 13](https://drive.google.com/uc?export=view&id=1KNPBw_gk01oaL6113P_zet0otlC4LMRy)

### Step 14: Configure Web Application
Choose the application type as **Web application** and add the redirect URI: `http://localhost:3000/auth/google/callback`. Adjust the port number according to your setup.

![Step 14](https://drive.google.com/uc?export=view&id=1sqAYCgxSqToRNYcrZUe9P3-q_OL-Rgpa)

![Step 14](https://drive.google.com/uc?export=view&id=1k_11fB0EPRonmz7cOZb4NJyVKsS8I0Uj)

### Step 15: Copy OAuth Keys
Copy and paste the keys into your project where needed:

![Step 15](https://drive.google.com/uc?export=view&id=1ppTtjqfYvtnUsJljaocHKVOuboctCPb9)


## Setting Up Node.js Application

### Step 1: Open VSCode and Setup Node.js
Set up Node.js environment in your preferred code editor.

### Directory Structure:
![Directory Structure](https://drive.google.com/uc?export=view&id=1gyt6mlpAXBaezdLegO_twtIzJDfD3Seo)

### Step 2: Install Required Packages
Install necessary packages in your terminal:

```bash
npm i express dotenv ejs express-session passport passport-google-oauth2
```

### Step 3: Environment Variables
Create a .env file in the root directory and set up environment variables:

```bash
SESSION_SECRET="YOUR_SESSION_SECRET_HERE" >
CLIENT_ID="YOUR_CLIENT_ID_HERE"
CLIENT_SECRET="YOUR_CLIENT_SECRET_HERE"
```

Replace YOUR_SESSION_SECRET_HERE, YOUR_CLIENT_ID_HERE, and YOUR_CLIENT_SECRET_HERE with your actual values.

### Step 4: Configure Passport
Create passport.js file in your main root folder to configure Passport with the Google strategy:

**Note:** Passport is a popular middleware for Node.js that provides a simple and flexible way to handle authentication in web applications. It supports various authentication strategies, allowing you to authenticate users using different methods, such as username and password, social login (like Google, Facebook, Twitter), OAuth, JWT (JSON Web Tokens), and more.

Passport-google-oauth2 is a strategy for Passport.js to authenticate users using their Google accounts through OAuth 2.0. 


#### Passport Initialization and Google Strategy Setup:
```bash
const passport = require('passport');
const GoogleStrategy = require('passport-google-oauth2').Strategy;
```
#### Serialize and Deserialize User:
##### passport.serializeUser: 
Defines how user information is serialized into the session. In this case, it simply passes the user object to done.
##### passport.deserializeUser: 
Defines how user information is deserialized from the session. It retrieves the user object from the session storage and passes it to done.
```bash
passport.serializeUser((user , done) => {
    done(null , user);
})

passport.deserializeUser(function(user, done) {
    done(null, user);
});

```
#### Google Strategy Configuration:
passport.use(new GoogleStrategy({...}, function(...){...}));: Configures the Google authentication strategy with Passport.

```bash
passport.use(new GoogleStrategy({
    clientID:process.env.CLIENT_ID, // Your Credentials here.
    clientSecret:process.env.CLIENT_SECRET, // Your Credentials here.
    callbackURL:"http://localhost:3000/auth/google/callback",
    passReqToCallback:true
},

```

#### Callback Function:
The callback function (request, accessToken, refreshToken, profile, done) is executed after Google has authenticated the user.
```bash
user.
function(request, accessToken, refreshToken, profile, done) {
    return done(null, profile);
}
));
```

### Step 5: Configure userController
Create a userController.js file in the controllers directory to handle the responses for the authentication routes.

#### loadAuth Function:
Renders the authentication page (auth) when a user navigates to the corresponding route.
```bash
const loadAuth = (req, res) => {
    res.render('auth');
}
```
#### successGoogleLogin Function:
Handles the response after a successful Google login.
```bash
const successGoogleLogin = (req, res) => {
    if (!req.user) {
        res.redirect('/failure');
    }
    console.log(req.user);
    res.send("Welcome " + req.user.email);
}

```
#### failureGoogleLogin Function::
Handles the response after a failed Google login

```bash
const failureGoogleLogin = (req, res) => {
    // Send a generic error message indicating login failure.
    res.send("Error");
}
```


### Step 6: Configure userRoute
Create a userRouter.js in your routes directory to define the routes for authentication

#### Passport Middleware Initialization::

##### router.use(passport.initialize());: 
Initializes Passport middleware to handle authentication.
##### router.use(passport.session());: 
Initializes Passport session support, which is typically needed when using persistent login sessions.

```bash
router.use(passport.initialize());
router.use(passport.session());
```
#### Route /auth/google/callback (GET):
Handles the callback from Google after authentication.
```bash
router.get('/auth/google/callback',
    passport.authenticate('google', {
        successRedirect: '/success', // Redirect to '/success' if authentication succeeds
        failureRedirect: '/failure' // Redirect to '/failure' if authentication fails
    })
);
```

#### Route /success (GET)::
Handles the response after a successful Google login.
```bash
router.get('/success', userController.successGoogleLogin);
```
#### Route /failure (GET)::
Handles the response after a failed Google login

```bash
router.get('/failure', userController.failureGoogleLogin);
```

### Step 6: Configure Main index.js
This file (server.js or similar) sets up a basic Node.js application using Express with session management and EJS as the view engine. Let's go through each part of the code to understand what it does:

##### Session Management Setup:
app.use(session({ ... })): Configures session management middleware:
resave: false: Prevents the session from being saved to the session store on every request unless the session data has been modified.
saveUninitialized: true: Forces a session that is "uninitialized" to be saved to the store. A session is uninitialized when it is new but not modified.
secret: process.env.SESSION_SECRET: Specifies the secret used to sign the session ID cookie. This secret is retrieved from the environment variable SESSION_SECRET set in the .env file.
```bash
const session = require('express-session');

app.use(session({
    resave: false,
    saveUninitialized: true,
    secret: process.env.SESSION_SECRET
}));

````
##### Routing Setup

```bash
const userRoutes = require('./routes/userRoute');
app.use('/', userRoutes);

```

##### Server Start

```bash
app.listen(3000, () => {
    console.log("Server Running on port 3000");
});

```

### STEP 7: EJS Views
Create a auth.ejs file in views directory under the server directory to render the authentication page:

```bash
<button><a href='/auth/google'>Login With Google</a></button>
```
