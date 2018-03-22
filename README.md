# Express disk cache

Middleware for caching responses sent through [Express](http://expressjs.com/) to disk.

# Why is this useful?

Because servers are good at serving static files. It's also useful if you have NGINX sitting in front of your node.js webserver and want to take some of the load off it.

# How to use it

Install the module using your package manager of choice:

```
npm install express-disk-cache
```

Then include the middleware in your [Express](http://expressjs.com/) app:

```javascript
var cache = require('express-disk-cache');
var app = Express();

// This will cache every response to disk
// assuming it meets the conditions described below
app.use(cache({
  directory: __dirname + '/cache'
}));
```

# How it works

As I understand it, HTTP response in express and node is a writeable stream. It wraps the res.write and res.end functions so it will work no matter how you send the response, using res.send, res.render, res.sendStatus, res.sendFile etc...

# Conditions for caching

- The cache-control header is not set to no-cache
- There is no query string in the URL
- There is no session associated with the request

# To do

Check that the URL contains valid characters that we can use to create a file on the file system.
Re-implement the filter function used by compression.
