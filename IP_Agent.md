### 代理服务器的原理
<p>代理服务器的工作机制很象我们生活中常常提及的代理商，假设你的机器为A机，你想获得的数据由B机提供，代理服务器为C机，那么具体的连接过程是这样的。 
首先，A机需要B机的数据，它与C机建立连接，C机接收到A机的数据请求后，与B机建立连接，下载A机所请求的B机上的数据到本地，再将此数据发送至A机，完成代理任务。</p>

### 谁提供免费的代理服务器
* 善良的服务器的系统管理员或能取得服务器管理权的人设置的。（简单的说通常就是用肉鸡 做的） 
* 真正好心的人，在自己的服务器设置代理，造福大众。 
* 一些ISP商为了提高影响，在一段时间内开放的免费代理。通常时间很短。
 
<strong>
在您的流量中注入广告，或通过向广告客户销售数据来实现此目的。
</strong>

#### IP代理的商业价值
1. 1 网络兼职。
- 如游戏试玩、电商优化、邮件群发以及打码投票。
2. 2 网络推广
- 使用代理IP的话就能够轻松的在同一个网站上以及不同的网站上注册多个账号,发表许多推广帖子。
3. 3 销量补量
- 通过换IP的技术来进行投票点赞、提高软件下载量、宝贝收藏等销售量。
4. 4 爬虫的采集
5. 5 通过代理服务器访问一些不能直接访问的网站
6. 6 安全性得到提高 (别人得不到你的真正的IP)

#### 代理分类
- 匿名代理 代理不改变客户机的请求，这样在服务器看来就像有个真正的客户浏览器在访问它，这时客户的真实IP是隐藏的,服务器端不会认为我们使用了代理

- 普通匿名代理: 代理能隐藏客户机的真实IP，但会改编我们的请求信息，服务器端有可能会认为我们使用了代理，但其实这种代理的安全性可能比全匿名代理更高，有的代理甚至会剥离客户机发送信息中 的一部分，这样服务器端就根本探测不到我们所用的操作系统版本和浏览器版本；

- 透明代理: 它不但改编我们的请求信息，还会传送真实的IP地址。

###免费代理采集

1. [快代理](http://www.kuaidaili.com/)
2. [代理66](http://www.66ip.cn/)
3. [全网代理](http://www.goubanjia.com/free/gngn/index.shtml)

###如何保证代理质量
1. 进行ping
2. 代理

#### 需要用到的技术
1. superagent
2. superagent-proxy

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
 
 ### 防止IP被封
 - 每次请求动态修改了useragent和x-forward-for 