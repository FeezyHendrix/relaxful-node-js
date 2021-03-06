# Relaxful Node-js

A REST API client.  Currently no file upload support.

## Use

Note the path to the APIHelper.js module, if not installed through npm or a package manager use the absolute path the the file.

Non npm ```require('./relaxful.js');```

### Simple Request

Access string result using 'result.text' property of the result object if request is successfule

Also supports https  

```js
var helper = require('relaxful');

helper.request('get', 'http://someurl/some/path').promise.then(result => {
  console.log(result.text);
}).catch(error => {
  // todo handle error
});
```

### Request Headers

```js
var helper = require('relaxful');

var reqHeaders = { 'api-key': 'some-api-key' };

helper.request('get', 'http://someurl/some/path',{ headers: reqHeaders }).promise.then(result => {
  console.log(result.text);
}).catch(error => {
  // todo handle error
});
```

### Request Body

```js

var helper = require('relaxful');

var body = { 'name': 'John Smith' };

helper.request('get', 'http://someurl/some/path', { body: body }).promise.then(result => {
  console.log(result.text);
}).catch(error => {
  // todo handle error
});
```

### JSON

Use the 'json()' method of a result to parse JSON data from the reqponse.

```js
var helper = require('relaxful');

helper.request('get', 'http://someurl/some/path').promise.then(result => {
  return result.json();
}).then(json => {
  // todo handle json object  
}).catch(error => {
  // todo handle error
});
```

### Validation

Use the 'validate()' method of a result to validate its' status code.

```js
var helper = require('./relaxful');

helper.request('get', 'http://someurl/some/path').promise.then(result => {
  return result.validate();
}).then(result => {
  console.log(result.text); 
}).catch(error => {
  // todo handle error
});
```

### Response

When a response fails validation or you need to check the HTTP Status code, you can access the ```status``` property of the response.  To get the HTTP Status message, access it through the ```message``` property.  

```js
var helper = require('./relaxful');

helper.request('get', 'http://someurl/some/path').promise.then(result => {
  return result.validate();
}).then(result => {
  console.log(result.status); 
  console.log(result.message);
}).catch(error => {
  // todo handle error
});     
```

To access a plain text response of the response body, use the ```text``` property.

```js
var helper = require('./relaxful');

helper.request('get', 'http://someurl/some/path').promise.then(result => {
  return result.text;
}).catch(error => {
  // todo handle error
});
```

Response headers are passed back in the ```headers``` property of the response.  

```js
var helper = require('./relaxful');

helper.request('get', 'http://someurl/some/path').promise.then(result => {
  return result.headers;
}).catch(error => {
  // todo handle error
});
```

### Cancel a Request

The current request is stored in the 'req' property of the helper object.  
Get the current helper object and access the request property and abort.

```js
helper.req.abort();
```
