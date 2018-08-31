# web_learn_article_record
web端技术文章收藏和学习 (对web端的查漏补缺,持续更新)

## ES6的双冒号

> ES7-函数的扩展-双冒号运算符
https://blog.csdn.net/ww430430/article/details/78492439
是 bind call apply的语法糖

```javascript
//无参数绑定对象
// 双冒号左边是一个对象，右边是一个函数。改运算符会自动将左边的对象，作为上下文环境（即 this 对象），绑定到右边的函数上面
foo::bar
bar.bind(foo)


//有参数时
foo::bar(...arguments);
bar.apply(foo, arguments);

// 如果双冒号左边为空，右边是一个对象的方法，则等于将该方法绑定在该对象上面。

let log = ::console.log;
var log = console.log.bind(console);

var method = ::obj.foo;
var method = obj::obj.foo;
var method = obj.foo.bind(obj)


```
>对应的babel
https://babeljs.io/docs/en/babel-plugin-proposal-function-bind