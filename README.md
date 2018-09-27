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

## ?.语法
```jvascript
const obj = {
  foo: {
    bar: {
      baz() {
        return 42;
      },
    },
  },
};

const baz = obj?.foo?.bar?.baz(); // 42

const safe = obj?.qux?.baz(); // undefined
const safe2 = obj?.foo.bar.qux?.(); // undefined

const willThrow = obj?.foo.bar.qux(); // Error: not a function

// Top function can be called directly, too.
function test() {
  return 42;
}
test?.(); // 42

exists?.(); // undefined
//从代码中猜测是用于判断对象是否存在,如果存在则继续执行,如果不存在则返回undefind

//如果是原生代码将多很多判断的代码
if(obj&&obj.foo&&obj.foo.bar&&obj.foo.bar.baz){
    obj.foo.bar.baz()
}
```
> 对应的babel
https://babeljs.io/docs/en/babel-plugin-proposal-optional-chaining

## |> 语法,管道操作
```javascript
const double = (n) => n * 2;
const increment = (n) => n + 1;

// without pipeline operator
double(increment(double(double(5)))); // 42

// with pipeline operator
5 |> double |> double |> increment |> double; // 42

//为了解决嵌套调用的语法糖
```
> 对应的bable
> https://babeljs.io/docs/en/next/babel-plugin-proposal-export-default-from.html#example
> 说明文档Pipeline operator
> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Pipeline_operator

## do表达式
```javascript
let a = do {
  if(x > 10) {
    'big';
  } else {
    'small';
  }
};
// is equivalent to:
let a = x > 10 ? 'big' : 'small';

//对a的赋值是一个运算

```
> 对应的bable
> https://babeljs.io/docs/en/babel-plugin-proposal-do-expressions


## React 高阶组件

日期 2018年9月4日

深入理解 React 高阶组件 https://www.jianshu.com/p/0aae7d4d9bc1

> 看文这篇文章我对高阶组件的理解:

高阶组件的概念更像是 设计模式中的"装饰模式",将组件颗粒化,基础的组件通过高阶组件的包装达到功能的真强,同时高级组件之间也是独立的,不同的功能可以通过不同的高阶组件(或是通过多个)高阶组件来包装


> 用高阶组件能干什么?

* 代码复用，逻辑抽象，抽离底层准备（bootstrap）代码
* 渲染劫持
* State 抽象和更改
* Props 更改
  
> 最基本的使用方法
```jvascript

//包装
export defaunt function ppHOC(WrappedComponent) {
  return class PP extends React.Component {
    render() {
      return (<div><WrappedComponent {...this.props}/></div>)
    }
  }
}

export defaunt class Example extends React.Component {
  render() {
    return <input name="name"/>
  }
}

const HOC = PComponent(Example);

```

> 添加新的props或修改props
``` javascript
function ppHOC(WrappedComponent) {
  return class PP extends React.Component {
    render() {
      const newProps = {
        user: currentLoggedInUser
      }
      return <WrappedComponent {...this.props} {...newProps}/>
    }
  }
}

```

> 反向继承
```javascript
function iiHOC(WrappedComponent) {
  return class Enhancer extends WrappedComponent {
    render() {
      return super.render()
    }
  }
}
```

## 在windows上调试ioswebView的设置方法:
https://cloud.tencent.com/developer/ask/81532/answers/created

https://github.com/mrdulin/blog/issues/50

https://github.com/RemoteDebug/remotedebug-ios-webkit-adapter#getting-started
