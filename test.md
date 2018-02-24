# 测试

> 此篇规范说明针对 `alibaba/macaca` 编写  
> `macaca` 是基于 `mocha` 的多端测试工具，断言库选择 `chai.expect`


### 1 mocha相关

**1.1 测试脚本的写法**  

通常，测试脚本与所要测试的源码脚本同名，但是后缀名为 `.test.js` （表示测试）或者 `.spec.js` （表示规格）。比如， `demo.js` 的测试脚本名字就是 `demo.test.js`。

测试脚本里面应该包括一个或多个 `describe` 块，每个 `describe` 块应该包括一个或多个 `it` 块。

`describe` 块称为"测试套件"（test suite），表示一组相关的测试。它是一个函数，第一个参数是测试套件的名称（"加法函数的测试"），第二个参数是一个实际执行的函数。  

`it` 块称为"测试用例"（test case），表示一个单独的测试，是测试的最小单位。它也是一个函数，第一个参数是测试用例的名称（"#1 should ..."），第二个参数是一个实际执行的函数。

**1.2 断言库的用法**  

所谓 `断言` ，就是判断源码的实际执行结果与预期结果是否一致，如果不一致就抛出一个错误。  

断言库有很多种，Mocha并不限制使用哪一种。上面代码引入的断言库是 `chai` ，并且指定使用它的 `expect` 断言风格。
expect断言的优点是很接近自然语言，下面是一些例子：  

```javascript
// 相等或不相等
expect(4 + 5).to.be.equal(9);
expect(4 + 5).to.be.not.equal(10);
expect(foo).to.be.deep.equal({ bar: 'baz' });

// 布尔值为true
expect('everthing').to.be.ok;
expect(false).to.not.be.ok;

// typeof
expect('test').to.be.a('string');
expect({ foo: 'bar' }).to.be.an('object');
expect(foo).to.be.an.instanceof(Foo);

// include
expect([1,2,3]).to.include(2);
expect('foobar').to.contain('foo');
expect({ foo: 'bar', hello: 'universe' }).to.include.keys('foo');

// empty
expect([]).to.be.empty;
expect('').to.be.empty;
expect({}).to.be.empty;

// match
expect('foobar').to.match(/^foo/);
```

基本上， `expect` 断言的写法都是一样的。头部是 `expect` 方法，尾部是断言方法，比如 `equal`、`a`/`an`、`ok`、`match` 等。两者之间使用 `to` 或 `to.be` 连接。  

如果 `expect` 断言不成立，就会抛出一个错误。**事实上，只要不抛出错误，测试用例就算通过。**

**1.3 测试用例钩子**

```javascript
describe('hooks', function() {

  before(function() {
    // 在本区块的所有测试用例之前执行
  });

  after(function() {
    // 在本区块的所有测试用例之后执行
  });

  beforeEach(function() {
    // 在本区块的每个测试用例之前执行
  });

  afterEach(function() {
    // 在本区块的每个测试用例之后执行
  });

  // test cases
});
```

**1.4 测试用例选择执行**

```javascript
it.only('#1(0) should ...', function() {
  // 此时只有带only的测试用例才会执行
});

it('#1(1) should ...', function() {
  // 此方法不会执行
});

it.skip('#1(2) should ...', function() {
  // 此方法指定被跳过，不会执行
});
```

### 2 macaca测试脚本模板

```javascript
// 引入官方 webdriver client 包
var wd = require('macaca-wd');

// 引入断言库
var expect = require('chai').expect;

// 引入 macaca API 扩展
require('./wd-extend')(wd, false);

// 定义 webdriver client 要链接的服务端 host 和 port
var remoteConfig = {
  host: 'localhost',
  port: 3456 // Macaca server 默认使用 3456 端口
};

// 后面 driver 直接使用链式调用即可
var driver = wd.promiseChainRemote(remoteConfig);

// 桌面端配置
const pcOpts = {
  platformName: 'desktop', // iOS, Android, Desktop
  browserName: 'chrome'    // Chrome, Electron
};

// 移动端配置
const iOSSafariOpts = {
    deviceName: 'iPhone 6',
    platformName: 'iOS',
    browserName: 'Safari'
};

const AndroidChromeOpts = {
    platformName: 'Android',
    browserName: 'Chrome'
    // app: 'path/to/app'
};

describe('demo.test.js', function(){
  // 测试前的初始化操作
  before(function() {
    return driver.init(pcOpts);
  });
  
  // 每项测试结束后的操作
  afterEach(function() {
    return driver
      .customSaveScreenshot(this)
      .sleep(1000)
  });
  
  // 所有测试结束后的操作
  after(function() {
    opn(path.join(__dirname, '..', 'reports', 'index.html'));
    return driver
      .sleep(1000)
      .quit();
  });
  
  describe('test demo name', function() {
    // 测试套件内容
    it('#1 should ...'/* 测试用例名称 */, function() {
      // 测试用例内容
      const initialURL = 'http://localhost:9000';
      return driver
        .get(initialURL)
        .sleep(3000);
    });
    
    it('#2 should ...'/* 测试用例名称 */, function() {
          // 测试用例内容
          const initialURL = 'http://localhost:9001';
          return driver
            .get(initialURL)
            .sleep(3000);
        });
  });
});
```

```javascript
// macaca API 扩展 wd-extend.js
module.exports = (wd, isIOS) => {
  // 例如以下几个方法
  wd.addPromiseChainMethod('customback', function() {
    if (isIOS) {
      return this
        .waitForElementByName('list')
        .click()
        .sleep(1000);
    }

    return this
      .back()
      .sleep(3000);
  });

  wd.addPromiseChainMethod('changeToNativeContext', function() {
    return this
      .contexts()
      .then(arr => {
        return this
          .context(arr[0]);
      });
  });

  wd.addPromiseChainMethod('customSaveScreenshot', function(context) {
    const filepath = path.join(__dirname, '..', 'screenshots', `${_.uuid()}.png`);
    const reportspath = path.join(__dirname, '..', 'reports');
    _.mkdir(path.dirname(filepath));

    return this
      .saveScreenshot(filepath)
      .then(() => {
        appendToContext(context, `${path.relative(reportspath, filepath)}`);
      });
  });
}
```

### 3 macaca 测试用例常用API

|序号|名称|描述|
|---|---|---|
|1|`get(url) → { Promise.<string> }`|导航到一个新的网址|
|2|`elementById(value) → { Promise.<Element> }`|从根结点搜索获取id为指定值的元素|
|3|`sleep(ms) → { Promise }`|阻塞（等待）指定毫秒数|
|4|`click() → { Promise }`|点击一个元素|
|5|`close() → { Promise.<string> }`|关闭窗口|
|6|`context(contextRef) → { Promise }`|上下文|
|7|`allCookies() → { Promise.<string> }`|获取所有cookies内容|
|8|`back() → { Promise.<string> }`|导航到上一页|
|9|`clear() → { Promise.<string> }`|清空input或textarea元素的内容|
|10|`getComputedCss(propertyName) → { Promise.<string> }`|获取计算后的css|
|11|`getProperty(name) → { Promise.<string> }`|获取一个元素的参数|
|12|`execute(code[, args]) → { Promise.<string> }`|插入JS片段以执行|
|13|`frame(frameRef) → { Promise.<string> }`|变换焦点 frameRef为目标元素的id或name|
|14|`hasElementById(value) → { Promise.<boolean> }`|是否存在名为id的元素|
|15|`keys(keys) → { Promise }`|向页面发送键盘按键|

参考资料：https://macacajs.github.io/macaca-wd/

### 4 macaca 测试环境配置完整过程

#### 4.1 安装依赖环境并检查

```bash
npm i macaca-cli -g
```
参考链接：https://macacajs.github.io/zh/environment-setup

* **注意：**  
1. 全局安装不要用sudo命令，推荐使用nvm安装node，可将node和npm安装到用户目录下（若安装在系统目录下，会导致测试脚本运行失败！）
2. Java环境只支持Java 1.8，不支持Java 9
3. 不同移动平台测试需要安装对应驱动：

|平台|驱动名称|
|---|---|
|iOS|`macaca-ios`|
|Android|`macaca-android`|

* **配置环境样例：**

```json
// package.json
"devDependencies": {
    "blink-diff": "^1.0.13",
    "detect-port": "^1.1.4",
    "macaca-cli": "^2.0.13",
    "macaca-reporter": "^1.0.10",
    "macaca-simple-reportor": "^1.0.0",
    "macaca-utils": "*",
    "macaca-wd": "^1.0.17",
    "mocha": "^4.1.0",
    "opn": "^5.1.0",
    "should": "^13.1.3",
    "webdriver-keycode": "^1.0.2",
    "macaca-chrome": "^1.0.7",
    "macaca-ios": "^2.0.30"
  }
```

#### 4.2

#### 4.3

#### 4.4

#### 4.5



