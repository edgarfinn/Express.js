# [Express.js](http://expressjs.com/)
A quick guide to using [express.js](http://expressjs.com/)

# What
[Express](http://expressjs.com/) is a flexible and relatively easy-to-use Node.js framework for building web and mobile applications.


Basic Setup
---

**Command line:**

```bash
npm init
npm i express [--save]
touch app.js
```

**app.js :**

```js
const express = require('express');
const app = express();
const port = process.env.PORT || 3000;

// route handler function
app.get('/', function(req,res){
  res.send('Welcome to my app');
})

// start server
// and listen for connections on specified port
app.listen(3000, function() {
  console.log('App listening on port: ', port);
})

```

Serving Static Files (such as HTML, CSS and client-side javascript)
---

#### Can be done using either:

##### The __```express.static```__ middleware function

#### OR

##### The __```res.sendFile()```__ method

```express.static```

```res.sendFile()```


Resources
---
- [Express Documentation](http://expressjs.com/)
- [Full Stack Training: How to serve static files with express](http://www.fullstacktraining.com/articles/how-to-serve-static-files-with-express)
