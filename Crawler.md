###  Node Crawler
- Need  import superagent and cheerio.
```javascript
   var cheerio = require('cheerio');
   var superagent = require('superagent');
```
###Example Code

```javascript
    app.get('/', function (req, res, next) {
      superagent.get('https://cnodejs.org/')
        .end(function (err, sres) {
          if (err) {
            return next(err);
          }
          var $ = cheerio.load(sres.text);
          var items = [];
          $('#topic_list .topic_title').each(function (idx, element) {
            var $element = $(element);
            items.push({
              title: $element.attr('title'),
              href: $element.attr('href')
            });
          });
    
          res.send(items);
        });
    });
```