# Reverse Engineering Code - Tutorial

## config
### middleware >>> isAuthenticated.js
```
Custom middleware for checking if a user is logged in and redirecting them to the login page if they are not. 
```

### config.json
```
Stores credentials dialect information for connecting to the database depending on the environment.
```

### passport.js
```
Dependencies: passport, passport-local, models

Authentication middleware that is checking if the username and password combination entered exists in the User database. The serialize and deserialize methods allow the user to stay signed in even as the app re-routes to different HTML pages.
```

## models
### index.js
```
Dependencies: fs, path, sequelize, config.json

Imports all files in the models folder and "sequelizes" them. Developers can then import the entire models folder in another file and have access to all models and sequelize functions in those models.
```

### user.js
```
Dependencies: bcryptjs

Creates a model for the User table with proper validation. bcryptjs is used to hash passwords so that they can be safely stored and read in the database.
```

## public
### js >>> login.js
```
Dependencies: login form, email input, password input

Javascript for the login page that handles user submission of email and password. On submission the code checks that an email and password have been entered, sends a post request to the api validate user info, clears the form and either throws an error or redirects to the members page.
```

### js >>> members.js
```
Javascript for the members page that sends a get request to the api returning the users email.
```

### js >>> signup.js
```
Dependencies: signup form, email input, password input

Almost identical to login.js, this file contains Javascript for the signup page that handles user submission of email and password. On submission the code checks that an email and password have been entered, sends a post request to the api to create a new user, clears the form and either throws an error or redirects to the members page.
```

### stylesheets >>> style.css
```
Sets a 50px top margin for the signup and login forms
```

### login.html
```
Dependencies: style.css, login.js

HTML for the login page with a form that contains inputs for email and password, a login button and a link to the signup page.
```

### members.html
```
Dependencies: style.css, members.js

HTML for the members page with a button to logout and a dynamic welcome banner displaying the members's name or email.
```

### signup.html
```
Dependencies: style.css, signup.js

HTML for the signup page with a form that contains inputs for email and password, a signup button and a link to the login page.
```

## routes
### api-routes.js
```
Dependencies: models, passport

Creates routing for querying the database. Queries include: login post requests that check entered info (authenticated with passport) against the database, signup post requests that create a new user on the database, get request for logging users out and redirecting them and get request for getting user data to be displayed client side.
```

### html-routes.js
```
Dependencies: path, isAuthenticated.js

Creates routing for navigating the HTML pages. Page routes include: get requests for redirecting users to the members page after signup or login and a get request for all redirections to the members page that uses the custom isAuthenticated.js middleware to check if the user is logged in before allowing redirection to the members page.
```

### package.json
```
Contains overview information about our node project including the name, version, description, author and license. It also includes a list of all project dependencies that will be load on "npm install"
```

### server.js
```
Dependencies: express, express-session, passport, models, routes

Initializes the entire app. First loads dependencies then sets up a port and requires all models. Next sets up express app and configures middleware, including express session which allows the use of sessions to track user info (login status) across multiple HTTP requests and re-routing. Finally, loads api and html routes and then syncs models to the database and begins listening at the appropriate port, at this point the app is now running. 
```