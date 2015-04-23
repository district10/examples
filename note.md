# Some Notes


### 404

```js
// --404
app.use(function *pageNotFound(next){
  yield next;

  if (404 != this.status) return;

  // we need to explicitly set 404 here
  // so that koa doesn't assign 200 on body=
  this.status = 404;

  switch (this.accepts('html', 'json')) {
    case 'html':
      this.type = 'html';
      this.body = '<p>Page Not Found</p>';
      break;
    case 'json':
      this.body = {
        message: 'Page Not Found'
      };
      break
    default:
      this.type = 'text';
      this.body = 'Page Not Found';
  }
})
```


### Basic Auth

```js
// custom 401 handling

app.use(function* (next){
  try {
    yield* next;
  } catch (err) {
    if (401 == err.status) {
      this.status = 401;
      this.body = 'cant haz that';
    } else {
      throw err;
    }
  }
});

// require auth

app.use(auth({ name: 'tj', pass: 'tobi' }));

// secret response

app.use(function* (){
  this.body = 'secret';
});
```

### Body Parse

```js
// --body parse
app.use(function *(next){
  if ('POST' != this.method) return yield next;
  var body = yield parse(this, { limit: '1kb' });
  if (!body.name) this.throw(400, '.name required');
  this.body = { name: body.name.toUpperCase() };
});
```


### Route

```js
// --route
app.use(route.get('/', list));               // -X GET
app.use(route.get('/post/new', add));        // -X GET
app.use(route.get('/post/:id', show));       // -X GET
app.use(route.post('/post', create));        // -X POST

// route definitions

/**
 * Post listing.
 */

function *list() {
  this.body = yield render('list', { posts: posts });
}
// --render
// render.js
var views = require('co-views');

module.exports = views(__dirname + '/../views', {               /* export a function */
  map: { html: 'swig' }
});
// app.js
var render = require('./lib/render');                           /* get the function */
render('list', { posts: posts })                                /* use this function */    
```



