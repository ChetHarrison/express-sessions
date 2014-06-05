# express-sessions

ExpressJS/Mongoose Session Storage

## Installation

```
npm install express-sessions
```

## Usage

``` js
var mongoose = require('mongoose');

mongoose.connect();

app.use(express.session({
    secret: 'a4f8071f-c873-4447-8ee2',
    cookie: { maxAge: 2628000000 },
    store: new (require('express-sessions'))({
        storage: 'mongodb',
        instance: mongoose, // optional
        host: 'localhost', // optional
        port: 27017, // optional
        db: 'test', // optional
        collection: 'sessions', // optional
        expire: 86400 // optional
    })
}));
```
Or

``` js
var redis = require('redis');
var client = redis.createClient(6379, 'localhost');

app.use(express.session({
    secret: 'a4f8071f-c873-4447-8ee2',
    cookie: { maxAge: 2628000000 },
    store: new (require('express-sessions'))({
        storage: 'redis',
        instance: client, // optional
        host: 'localhost', // optional
        port: 6379, // optional
        collection: 'sessions', // optional
        expire: 86400 // optional
    })
}));
```
Or

``` js
var couchbase = require('couchbase');
var client = new couchbase.Connection({
    host: 'localhost:8091',  // You probably want to pull this from an evironment var.
	bucket: 'sessions',
	password: process.env.COUCHBASE_PASSWORD  // if you have a password 
});

app.use(express.session({
    secret: 'a4f8071f-c873-4447-8ee2',
    cookie: { maxAge: 2628000000 },
    store: new (require('express-sessions'))({
        storage: 'couchbase',
        instance: client, // optional
        host: 'localhost', // optional
        port: 8091, // optional
        bucket: 'sessions', // optional
        password: process.env.COUCHBASE_PASSWORD,  // optional, if you have a password 
        expire: 86400 // optional
    })
}));
```
That's it!
