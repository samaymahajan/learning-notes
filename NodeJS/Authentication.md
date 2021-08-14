### Passport + Express + NodeJs

#### Prerequisties
* NodeJS
* Express JS and How middleware works
* MongoDB
* Javascript and Async Programming


### Options for User Authentication Implementation
* Session
* JWT (JSON Web Tokens)
* OAuth
* Ad-Hoc Implementation

#### Packages Required
* Express
* mongoose
* dotenv
* express-session
* connect-mongo (MongoDB based session store)v
* memorystore (In Memory Session storage)
* morgan
* cors
* crypto
* passport
* passport-local
* passport-activedirectory

### Express Session

* Session store is required to store session data on a storage (File, Memory, DB)
* express-session use [session store packages](https://www.npmjs.com/package/express-session#compatible-session-stores)

```js
const session = require('express-session');
const MongoStore = require('connect-mongo')(session);

/*** -------------- SESSION SETUP ----------------*/
const sessionStore = MongoStore.create(
                              { 
                                    mongoUrl: process.env.MONGO_URL, 
                                    collection: 'sessions',
                                    autoRemove: true,
                                    ttl: 2 * 24 * 60 * 60

                              });
app.use(session({
                  secret: process.env.SECRET,
                  resave: false,
                  saveUninitialized: true,
                  store: sessionStore,
                  cookie: {
                        maxAge: 1000 * 60 * 60 * 24 // Equals 1 day (1 day * 24 hr/1 day * 60 min/1 hr * 60 sec/1 min * 1000 ms / 1 sec)
                  }
      }));

```
### Passport Configuration & Setup

#### Methods Used
* passport.authenticate('<strategy>');


```js
//app.js
require('./config/passport');
app.use(passport.initialize());
app.use(passport.session());


// config/passport.js
// get passport, localstrategy, db connection, userSchema

const customFields = { 
      usernameField = 'uname',
      passwordField = 'pw'
}

const verifyCallback = (username,passowrd,doneCB) => {
      User.findOne({username:username})
                  .then((user) => {
                        if(!user) {
                              return doneCB(null,false) 
                        }
                        const isValid = validPassword(password,user.hash,user.salt);

                        if(isValid) {
                              return doneCB(null,user);
                        }else{
                              return doneCB(null,false);
                        }
                  }).catch(err => doneCB(err;)54
}
const strategy = new LocalStrategy(customFields,verifyCallsback);
passport.use(strategy())
}))


```

## References
* User Authentication in Web Apps (Passport.js, Node, Express) - https://www.youtube.com/watch?v=F-sFp_AvHc8
