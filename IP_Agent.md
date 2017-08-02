# IP Agent
 - 安装中间件superagent
 ```javascript
    npm install superagent-proxy
    npm install superagent
```
###Example
- proxy is ip agent address
```javascript
var request = require('superagent');

// extend with Request#proxy()
require('superagent-proxy')(request);

// HTTP, HTTPS, or SOCKS proxy to use
var proxy = process.env.http_proxy || 'http://168.63.43.102:3128';

request
  .get(process.argv[2] || 'https://encrypted.google.com/')
  .proxy(proxy)
  .end(onresponse);

function onresponse (err, res) {
  if (err) {
    console.log(err);
  } else {
    console.log(res.status, res.headers);
    console.log(res.body);
  }
}
```
 refer to :https://github.com/alsotang/node-lessons/blob/master/lesson3/app.js