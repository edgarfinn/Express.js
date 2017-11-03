# Express.js
A quick guide to using express.js

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
