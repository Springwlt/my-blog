- 参考链接：https://cnodejs.org/topic/57c68052b4a3bca66bbddbdd
### Use ESLint check codeing quality.
<ins>
ESLint是一个插件化的javascript代码检测工具，它可以用于检查常见的JavaScript代码错误，也可以进行代码风格检查，这样我们就可以根据自己的喜好指定一套ESLint配置，然后应用到所编写的项目上，
从而实现辅助编码规范的执行，<strong>有效控制项目代码的质量</strog>.
</ins>

### Introduce Eslint
-  安装
 > npm install -g eslint

### 新建文件merge.js:
```javascript
function merge () {
  var ret = {};
  for (var i in arguments) {
    var m = arguments[i];
    for (var j in m) ret[j] = m[j];
  }
  return ret;
}

console.log(merge({a: 123}, {b: 456}));
```
执行eslint merge.js
<p> 没有任何执行结果，因为我们确实配置文件。

### 新建配置文件 .eslintrc.js：
```javascript
module.exports = {
  extends: 'eslint:recommended',
};
```
- 执行 eslint merge.js,结果如下
```javascript
  10:1  error  Unexpected console statement  no-console
  10:1  error  'console' is not defined      no-undef

✖ 2 problems (2 errors, 0 warnings)
```
- 信息说明：
* 1 Unexpected console statement no-console - 不能使用console
* 2 ‘console’ is not defined no-undef - console变量未定义，不能使用未定义的变量

### 禁用no-console,修改配置文件
```javascript
module.exports = {
  extends: 'eslint:recommended',
  rules: {
    'no-console': 'off',
  },
};
```
<strong>
说明：配置规则写在rules对象里面，key表示规则名称，value表示规则的配置，具体说明见下文。
</strong>
* 执行结果

```javascript
  10:1  error  'console' is not defined  no-undef
✖ 1 problem (1 error, 0 warnings)
```
<ins>
这是因为JavaScript有很多种运行环境，比如常见的有浏览器和Node.js，另外还有很多软件系统使用JavaScript作为其脚本引擎，
比如PostgreSQL就支持使用JavaScript来编写存储引擎，而这些运行环境可能并不存在console这个对象。
</ins>

### 指定程序的目标环境
```javascript
module.exports = {
  extends: 'eslint:recommended',
  env: {
    node: true,
  },
  rules: {
    'no-console': 'off',
  },
};
```
### 配置文件
```javascript
{
  "name": "my-package",
  "version": "0.0.1",
  "eslintConfig": {
    "extends": "eslint:recommended",
    "env": {
      "node": true
    },
    "rules": {
      "no-console": "off"
    }
  }
}
```
### 规则
<ins>
每条规则有3个等级：off、warn和error。off表示禁用这条规则，warn表示仅给出警告，
并不会导致检查不通过，而error则会导致检查不通过。
</ins>
<ins>
每条规则有3个等级：off、warn和error。off表示禁用这条规则，warn表示仅给出警告，
并不会导致检查不通过，而error则会导致检查不通过。
</ins>

[Rules-规则](http://eslint.cn/docs/rules/)

### 使用共享的配置文件
- 我们可以将定义好规则的.eslintrc.js文件存储到一个公共的位置，比如public-eslintrc.js
```javascript
module.exports = {
  extends: 'eslint:recommended',
  env: {
    node: true,
  },
  rules: {
    'no-console': 'off',
    'indent': [ 'error', 2 ],
    'quotes': [ 'error', 'single' ],
  },
};

```
- 然后将原来的.eslintrc.js文件改成这样

```javascript
module.exports = {
  extends: './public-eslintrc.js',
};
```
### 代码格式化

- 接着上文使用eslint-config-lei配置的检查，我们尝试在执行检查时添加--fix参数：
- 执行结果
```javascript
function merge() {
  const ret = {};
  for (const i in arguments) {
    const m = arguments[i];
    for (const j in m) ret[j] = m[j];
  }
  return ret;
}

console.log(merge({ a: 123 }, { b: 456 }));
```
### 发布自己的配置
- 新建文件eslint-config-my/index.js：
```javascript
module.exports = {
  extends: 'eslint:recommended',
  env: {
    node: true,
    es6: true,
  },
  rules: {
    'no-console': 'off',
    'indent': [ 'error', 2 ],
    'quotes': [ 'error', 'single' ],
  },
};

```
- 再新建文件eslint-config-my/package.json：
```javascript
{
  "name": "eslint-config-my",
  "version": "0.0.1",
  "main": "index.js"
}
```
- 为了能让eslint正确载入这个模块，我们需要执行npm link将这个模块链接到本地全局位置：
> $ npm link eslint-config-my

- 然后将文件.eslintrc.js改成这样：
```javascript
module.exports = {
  extends: 'my',
};

```
- 说明：在extends中，eslint-config-my可简写为my。



