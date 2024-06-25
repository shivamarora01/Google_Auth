# Google_Auth


#Steps for Client ID & Client Secret 

**Step 1:** open <https://console.developers.google.com/>  and you will be directed to this page![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.001.png)









**Step 2:** Click on the **dropdown of Projects**

![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.002.png)


**Step 3:** Tap on **New Project** as shown below…

![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.003.png)




**Step 4:** Create a **New Project** by adding a Project name 

![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.004.png)





















**Step 5:** You will be directed to the dashboard , then go to the projects dropdown and select your project 

![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.005.png)

**Step 6:** Click on the **Credentials** options and then go to the **create credentials** button in the credentials page

![ref1]

**Step 7:** Click on the **OAuth Client ID** and then click on the **create credentials button** in the credentials page

![ref2]


**Step 8:** Click on the **Consent screen button**

![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.008.png)










**Step 9:** Select the User Type External and create the app registration

![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.009.png)


**Step 10:** Add the **App information name** & **user mail**

![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.010.png)

**Step 11:** Click **SAVE AND CONTINUE** for next scope and test users

![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.011.png)![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.012.png)








**Step 12:** Click on the **Credentials** options and then open on the **create credentials** button in the credentials page

![ref3]






**Step 13:** Click on the **OAuth Client ID** and then tap on the create credentials button in the credentials page

![ref4]





**Step 14:** Then choose the application type as Web application and add this url <http://localhost:3000/auth/google/callback> into **Authorized redirect URIs**  as we will use it into project for requesting and tap on the create button.

<http://localhost:3000/auth/google/callback> => this port number should be given same as the server will run on port
![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.015.png)![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.016.png)

**Step 16:** Then the keys can be copy & paste in the project where needed
![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.017.png)




















**Step 2 : Open the VSCode and do the Nodejs Setup**

**For reference of files :** 

[**Google Login Link**](https://drive.google.com/file/d/1Hpt-hGoZZmgte9-V541v9_1blj-qC92l/view?usp=sharing)

**Directory Structure :** 

![](Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.018.png)

**1. Install Required Packages :** 

Install the packages in your terminal  

**npm i express dotenv ejs express-session passport passport-google-oauth2**

**Passport is a popular middleware for Node.js that provides a simple and flexible way to handle authentication in web applications. It supports various authentication strategies, allowing you to authenticate users using different methods, such as username and password, social login (like Google, Facebook, Twitter), OAuth, JWT (JSON Web Tokens), and more.**

**Passport-google-oauth2 is a strategy for Passport.js to authenticate users using their Google accounts through OAuth 2.0.** 


**2. Environment Variables:** 

**Create a .env file** in root and **Setup the .env file** by adding **CLIENT\_ID & CLIENT\_SECRET** as  generated in the step 1.10 as shown above

**.env file**

SESSION\_SECRET="SECRET\_HERE"

CLIENT\_ID=""

CLIENT\_SECRET=""



**3. Passport Configuration :** Create **passport.js file** in your main root folder to configure Passport with the Google strategy:

const passport = require('passport');

const GoogleStrategy = require('passport-google-oauth2').Strategy;

//serializeUser defines how user information is stored in the session

passport.serializeUser((user , done) => {

`    `done(null , user);

})

//deserializeUser defines how user information is retrieved from the //session

passport.deserializeUser(function(user, done) {

`    `done(null, user);

});

//Google Strategy Configuration

passport.use(new GoogleStrategy({

`    `clientID:process.env.CLIENT\_ID, // Your Credentials here.

`    `clientSecret:process.env.CLIENT\_SECRET, // Your Credentials here.

`    `callbackURL:"http://localhost:3000/auth/google/callback",

`    `passReqToCallback:true

},

// callback function that is called after Google has authenticated the user.

function(request, accessToken, refreshToken, profile, done) {

`    `return done(null, profile);

}

));


**4. User Controller:**

Create a **userController.js** file in the **controllers** directory to handle the responses for the authentication routes.

**userController.js file**

**// server/controllers/userController.js**

//Renders the authentication page.

const loadAuth = (req, res) => {

`    `res.render('auth');

}

//Handles the response after a successful Google login.

const successGoogleLogin = (req , res) => {

`    `if(!req.user)

`        `res.redirect('/failure');

`    `console.log(req.user);

`    `res.send("Welcome " + req.user.email);

}

//Handles the response after a failed Google login

const failureGoogleLogin = (req , res) => {

`    `res.send("Error");

}

module.exports = {

`    `loadAuth,

`    `successGoogleLogin,

`    `failureGoogleLogin

}

**5. Routes :** Create a **userRouter.js** in your **routes** directory to define the routes for authentication:

**userRoute.js file**

**// server/routes/userRoute.js**

const express = require('express');

const router = express();

const passport = require('passport');

require('../passport');


//Initializing Passport Middleware

router.use(passport.initialize());

router.use(passport.session());

const userController = require('../controllers/userController');

router.get('/', userController.loadAuth);

// Auth

//initiates authentication with Google, requesting access to the //user's email and profile information.

router.get('/auth/google' , passport.authenticate('google', { scope:

`    `[ 'email', 'profile' ]

}));

// Auth Callback

router.get( '/auth/google/callback',

`    `passport.authenticate( 'google', {

`        `successRedirect: '/success',

`        `failureRedirect: '/failure'

}));

// Success

router.get('/success' , userController.successGoogleLogin);

// failure

router.get('/failure' , userController.failureGoogleLogin);

module.exports = router;




**6. Main Application File:** Create a **index.js file** in your main directory to set up the Express application and use the routes:

**// server/app.js**

require('dotenv').config();

const express = require('express');

const app = express();

const session = require('express-session');

//Setting Up Session Management

app.use(session({

`    `resave: false,

`    `saveUninitialized: true,

`    `secret: process.env.SESSION\_SECRET

}));

app.set('view engine', 'ejs');

const userRoutes = require('./routes/userRoute');

app.use('/',userRoutes);

app.listen(3000 , () => {

`    `console.log("Server Running on port 3000");

});


**7. EJS Views:** Create a **auth.ejs** file in **views** directory under the **server** directory to render the authentication page: 

**Auth.ejs file** 

**<!-- server/views/auth.ejs -->**

<button><a href='/auth/google'>Login With Google</a></button>

[ref1]: Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.006.png
[ref2]: Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.007.png
[ref3]: Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.013.png
[ref4]: Aspose.Words.c4f8087a-1578-4c87-94a2-2f68d1367562.014.png
