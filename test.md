# 测试


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
