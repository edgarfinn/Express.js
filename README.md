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

**Serving Static Files**
---

``` express.static ``` is a built-in middleware function in express based on the ``` serve-static ``` node module, used for serving static files (such as HTML, CSS and client-side javascript)

** Basic setup: **

If your files are structured into separate folders (such as below), its best to expose the ``` path ``` node module, and use the ``` path.join() ``` method for binding filepaths.

** Your app file structure: **

public/

  - index.html
  - styles/
    - index.css


src/

  - app.js


**app.js:**
```js

const path = require('path');

// basic setup for express.static:
app.use(express.static(path.join(__dirname, '../public')));

```

Once set-up, assuming your index.html file links to the css file, when serving up the index.html file, express will also know to use the css file, and any other **linked** static files (including images and javascript) within the public folder

You can also tell express to serve up different html files within the public folder using express's ```res.sendFile()``` method like so:

```js
app.use('/',express.static(path.join(__dirname, '../public')));

app.get('/about', function(req,res){
  res.sendFile(path.join(__dirname, '../public/about.html'))
})
```

In the above example, any stylesheets within the public folder will still be read also, so long as they are called / linked in the ```about.html``` file. **HOWEVER**, this means that about/index.html and home/index.html both need to share the SAME supporting files (ie index.css and any supporting JS files). In many cases it is better to separate out different endpoint requests within multiple incidences of ```express.static```, and create a separate directory for all supporting files like so:

** Your app file structure: **

public/

  /about/

  - index.html
  - styles/
    - index.css


  /home/

  - index.html
  - styles/
    - index.css

src/

  - app.js

```js
app.use('/', express.static(path.join(__dirname, '../public/home')));
app.use('/about', express.static(path.join(__dirname, '../public/about')));
```

You can then set up separate directories for the 'about' page html, css and javascript under the 'public/about' directory (eg 'public/about/styles/about.css')

This is generally preferable over using the res.sendFile() method because ```express.static``` sets the [ETag](https://en.wikipedia.org/wiki/HTTP_ETag) for you, and allows you to set file extension fallbacks (eg ['html', 'htm'])

To link a particular path prefix (such as 'localhost:3000/**about**'), you can specify a given path (ie 'about') to a particular file directory like so:

```js

 app.use('/about', express.static(path.join(__dirname,'../about')))
 ```


Resources
---
- [Express Documentation](http://expressjs.com/)
- [Full Stack Training: How to serve static files with express](http://www.fullstacktraining.com/articles/how-to-serve-static-files-with-express)
