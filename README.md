**INFO**: Cloned from [Passport-pinterest](https://travis-ci.org/analog-nico/passport-pinterest) and upgraded the apis to pinterest v5.

# Passport-Pinterest-v5

[Passport](https://github.com/jaredhanson/passport) strategy for authenticating with [Pinterest](https://www.pinterest.com) using the OAuth 2.0 API.

This module lets you authenticate using Pinterest in your Node.js applications. By plugging into Passport, Pinterest authentication can be easily and unobtrusively integrated into any application or framework that supports [Connect](http://www.senchalabs.org/connect/)-style middleware, including [Express](http://expressjs.com/).

## Installation

[![NPM Stats](https://nodei.co/npm/passport-pinterest-v5.png?downloads=true)](https://npmjs.org/package/passport-pinterest-v5)

This is a module for node.js and is installed via npm:

``` bash
npm install passport-pinterest-v5
yarn add passport-pinterest-v5
```

## Usage

### Configure Strategy

The Pinterest authentication strategy authenticates users using a Pinterest account and OAuth 2.0 tokens. The strategy requires a `verify` callback, which accepts these credentials and calls `done` providing a user, as well as `options` specifying a client ID, client secret, scope, and callback URL.

``` js
passport.use(new PinterestStrategy({
        clientID: PINTEREST_APP_ID,
        clientSecret: PINTEREST_APP_SECRET,
        callbackURL: "https://localhost:3000/auth/pinterest/callback",
        state: true
    },
    function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ pinterestId: profile.id }, function (err, user) {
            return done(err, user);
        });
    }
));
```

**Pinterest only allows https callback urls.** [This blog article](http://blog.mgechev.com/2014/02/19/create-https-tls-ssl-application-with-express-nodejs/) explains the quickest way to enable https for your Express server.

### Authenticate Requests

Use `passport.authenticate()`, specifying the `'pinterest'` strategy, to authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/) application:

``` js
app.get('/auth/pinterest',
    passport.authenticate('pinterestV5')
);

app.get('/auth/pinterest/callback', 
    passport.authenticate('pinterestV5', { failureRedirect: '/login' }),
    function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
    }
);
```

## Contributing

To set up your development environment for Passport-Pinterest:

1. Clone this repo to your desktop,
2. in the shell `cd` to the main folder,
3. hit `npm install`,
4. hit `npm install gulp -g` if you haven't installed gulp globally yet, and
5. run `gulp dev`. (Or run `node ./node_modules/.bin/gulp dev` if you don't want to install gulp globally.)

`gulp dev` watches all source files and if you save some changes it will lint the code and execute all tests. The test coverage report can be viewed from `./coverage/lcov-report/index.html`.

If you want to debug a test you should use `gulp test-without-coverage` to run all tests without obscuring the code by the test coverage instrumentation.

## License (ISC)

In case you never heard about the [ISC license](http://en.wikipedia.org/wiki/ISC_license) it is functionally equivalent to the MIT license.

See the [LICENSE file](LICENSE) for details.