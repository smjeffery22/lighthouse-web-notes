# Authentication

  - Process of verifying a user
    - Username
    - Password
    - Security questions
    - Facial recognition
    - Fingerprints

  - *Authorization* is verifying what the user has *access to*
    - Typically after being authenticated
      - Post, edit, delete, etc.
      - Include error handling code to prevent modifications through external applcations such as Postman

## Passwords

  - **Never** store passwords in *text*

### Hashing Functions

  - Run the password through a *hashing function*
    - Then store in the database
    - Maps the input data of some arbitrary size to *fixed-siz*e output values

  - Run the input through the same hashing function that created hashed value
    - To compare and see if they match

### Cryptographic Hash Functions

  - One-way function which is infeasible to invert
  
  - Small change in input yields large change in the output
    - Changing one character in input changes the output significantly
  
  - Deterministic => same input yields the same output

  - Highly unlikely to find 2 outputs with the same value

  - Password hash functions are deliberately slow
    - If fast, can allow to quickly try different passwords to get output values

### Salts

  - Adding random values prior to hashing password
    - `password` => `passwordSALT`
    - `hasedpassword` => `hasedpasswordwithsalt`

  - Need to save the salt value
    - To add it when user comes back and logs in
    - To compare the same input

## Bcrypt

  - Password hashing function

  - bcrypt vs. bcryptjs
    - bcrypt only runs on the server side
    - bcryptjs also runs on the client side

  - `genSalt()` to generate salted bcrypted password
  - `compare()` to compare password to hashed password

```js
// to hash password
const bcrypt = require('bcrypt');

const hashPassword = async (pw) => {
  const salt = await bcrypt.genSalt(saltRounds);  // saltRounds => number (typically 12)
  const hash = await bcrypt.hash(pw, salt);
  //OR
  const hasedPw = await bcrypt(pw, saltRounds);
}

hashPassword('bori');

// to check password
const login = async (pw, hashedPw) => {
  const result = bcrypt.compare(pw, hashedPw);

  if (result) {
    console.log('Successful login');
  } else {
    console.log('Login fail');
  }
};
```

## Passport.js

  - Authentication middleware for Node.js
  - Can be used in Express-based web application
  - Supports comprehensive set of strategies support authentication
    - Username/Password
    - Google
    - Facebook
    - Twitter

### Passport-Local & Passport-Local Mongoose

  - `passport-local` allows authentication using a username and password in Node.js applications
  - `passport-local-mongoose` a Mongoose plugin that simplifies building username and password login
    - Static methods such as `authenticate()`, `register()`, etc. available

```js
// in mongoose model
const mongoose = require('mongoose');
const Schema = mongoose.Schema;
const passportLocalMongoose = require('passport-local-mongoose');

const UserSchema = new Schema({
	email: {
		type: String,
		required: true,
	},
});

UserSchema.plugin(passportLocalMongoose)

// in express
const passport = require('passport');
const LocalStrategy = require('passport-local');

// middleware
app.use(passport.initialize()); // required to initialize passport
app.use(passport.session());    // persistent login session

// use LocalStrategy
// authenticate method located at User model
// all comes from passport-local-mongoose static method
passport.use(new LocalStrategy(User.authenticate()));
passport.serializeUser(User.serializeUser());
passport.deserializeUser(User.deserializeUser());
```

  - `passport.authenticate()` in post route to authenticate login
    - `req.user` property is set to the authenticated user
  - `isAuthenticated()` method to restrict access to certain pages
  - When redirected to login page due to have no authorization:
    - `req.path` gives the current url
    - `req.originalUrl` gives the url that the user was on before being redirected

```js
router.post('/login', passport.authenticate('local', { failureFlash: true, failureRedirect: '/login' }), (req, res) => {
  req.flash('success', 'Welcome back!');
  res.redirect('/campgrounds');
});

if (!req.isAuthenticated()) {
  req.flash('error', 'You must sign in first to create new campground.');
  res.redirect('/login');
}
```