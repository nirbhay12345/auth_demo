# auth_demo

A simple barebone demo for implementing Authentication in NodeJS using ExpressJS. Make sure you have nodejs and mongodb configured locally

## Modules used

This project here uses:

1. `express` for creating the backend for the app
1. `mongoose` ro interact with MongoDB database
1. `bcrypt` hashing passwords
1. `express-session` for creating the seesion middleware with unique sessionID

## Mongoose setup

In the project the mongoose is setup locally as `mongodb://localhost:27017/loginDemo` is the local URL.

```js
mongoose.connect('mongodb://localhost:27017/loginDemo', { 
        useNewUrlParser: true, 
        useUnifiedTopology: true 
    })
    .then(() => {
        console.log("Database Connected!")
    })
    .catch(err => {
        console.log("Connection Error!")
        console.log(err)
    })
```
You can change the url as per your requirement and then run the app according to the setup instructions.

## App setup

`app.set('view engine', 'ejs');` - sets the view engine to ejs, so that the server can serve EJS files as default.

`app.set('views', 'views');` - it sets the views directory to be available as default.

`express.urlencoded` - It parses incoming requests with urlencoded payloads and is based on body-parse.

## User Model

A schema is described inside the `./models/user.js` file.

```js
username: {
    type: String,
    required: [true, 'Username cannot be blank']
},
password: {
    type: String,
    required: [true, 'Password cannot be blank']
}
```

The description include the type of variable.

This description also includes the errors that needs to be thrown when the required variables are not provided.


## API endpoints

| Route | description | body | sessionID |
|:---:|:---:|:---:|:---:|
|/register|new users can register into the app|username, password| new sessionID created|
|/login|already existing user can login to their account|username, password|new sessionID created|
|/secret|"sessionID" is checked so only visible to loggedin users|None|None|
|/logout|users can logout of the app|None|sessionID destroyed|

## Setup Instructions
  
1. Clone the repo
  
1. Go to the directory where the repo is downloaded and run `npm install` to install dependencies.
  
1. Replace your Mongo url in place of `mongodb://localhost:27017/loginDemo` and alter the `mongoose.connect('YOUR MONGOURI/loginDemo` in the app.js file 
  
1. Run npm install nodemon in the terminal this will help re-run the app when ever you try to change something in app.js
1. Go to the directory same as app.js and enter in the command `nodemon`
  
If you have followed through then the application should be up and running at 'localhost:3000'
