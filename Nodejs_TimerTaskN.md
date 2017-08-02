###Nodejs  定时任务
- 可是使用中间件node-schedule来实现定时任务
###  确定时间执行任务
```javascript
     var schedule = require("node-schedule");
    
        var date = new Date(2014,2,14,15,40,0);
    
        var j = schedule.scheduleJob(date, function(){
    
    　　　　console.log("执行任务");
    
    　 });
    
        取消任务
    
        j.cancel();
```
### 每小时的固定时间
* 例如：每小时的40分钟执行
```javascript
var rule = new schedule.RecurrenceRule();

　　rule.minute = 40;

　　var j = schedule.scheduleJob(rule, function(){

　　　　console.log("执行任务");

　　});
```
### 一个星期中的某些天的某个时刻执行
* 例如：周一到周日的20点执行
```javascript
var rule = new schedule.RecurrenceRule();

　　rule.dayOfWeek = [0, new schedule.Range(1, 6)];

　　rule.hour = 20;

　　rule.minute = 0;

　　var j = schedule.scheduleJob(rule, function(){

　　　　console.log("执行任务");

　　});
```
### 每秒都执行
```javascript
var rule = new schedule.RecurrenceRule();

　　var times = [];

　　for(var i=1; i<60; i++){

　　　　times.push(i);

　　}

　　rule.second = times;

　　var c=0;
　　var j = schedule.scheduleJob(rule, function(){
     　　 c++;
      　　console.log(c);
　　});
```