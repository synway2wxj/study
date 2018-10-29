* https://react.docschina.org/tutorial/tutorial.html
* http://www.runoob.com/react/react-tutorial.html
* HTML 和 JavaScript 都比较熟悉了
* 在编码的时候已经开始使用 ES6 最新版本的 JavaScript, 在这篇教程里我们主要使用了 arrow functions, classes, let, and const 几个新的语法和关键字
* Node.js
* React 是一个采用声明式，高效而且灵活的用来构建用户界面的框架
* React 当中包含了一些不同的组件，我们从使用 React.Component
* class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}
* return React.createElement('div', {className: 'shopping-list'},
  React.createElement('h1', /* ... h1 children ... */),
  React.createElement('ul', /* ... ul children ... */)
);
* React主要用于构建UI，很多人认为 React 是 MVC 中的 V
* React 拥有较高的性能，代码逻辑非常简单
* React采用声明范式，可以轻松描述应用
* React通过对DOM的模拟，最大限度地减少与DOM的交互
* JSX 是 JavaScript 语法的扩展。React 开发不一定使用 JSX ，但我们建议使用它
* 通过 React 构建组件，使得代码更加容易得到复用，能够很好的应用在大项目的开发中
* React 实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更简单
* <div id="example"></div>
<script type="text/babel">
  ReactDOM.render(
    <h1>Hello, world!</h1>,
    document.getElementById('example')
  );
</script>
* <script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
<!-- 生产环境中不建议使用 -->
<script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>
* 在浏览器中使用 Babel 来编译 JSX 效率是非常低的
* react.min.js - React 的核心库
react-dom.min.js - 提供与 DOM 相关的功能
babel.min.js - Babel 可以将 ES6 代码转为 ES5 代码，这样我们就能在目前不支持 ES6 浏览器上执行 React 代码。Babel 内嵌了对 JSX 的支持。通过将 Babel 和 babel-sublime 包（package）一同使用可以让源码的语法渲染上升到一个全新的水平
* 如果我们需要使用 JSX，则 <script> 标签的 type 属性需要设置为 text/babel
* 建议在 React 中使用 CommonJS 模块系统，比如 browserify 或 webpack
* $ npm install -g cnpm --registry=https://registry.npm.taobao.org
* $ npm config set registry https://registry.npm.taobao.org
* $ cnpm install [name]
* create-react-app 自动创建的项目是基于 Webpack + ES6
* cnpm install -g create-react-app
* create-react-app my-app
* cd my-app/
* npm start
* npm config set registry https://registry.npm.taobao.org  npm config get registry
-- 或 npm info express
* 元素是构成 React 应用的最小单位，它用于描述屏幕上输出的内容：const element = <h1>Hello, world!</h1>;
* 与浏览器的 DOM 元素不同，React 当中的元素事实上是普通的对象，React DOM 可以确保 浏览器 DOM 的数据内容与 React 元素保持一致
* 用 React 开发应用时一般只会定义一个根节点
* 要将React元素渲染到根DOM节点中，我们通过把它们都传递给 ReactDOM.render() 的方法来将其渲染到页面上
* const element = <h1>Hello, world!</h1>;
ReactDOM.render(
    element,
    document.getElementById('example')
);
* function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>现在是 {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('example')
  );
}
 
setInterval(tick, 1000);
* function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>现在是 {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}
 
function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('example')
  );
}
 
setInterval(tick, 1000);
* class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>现在是 {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
 
function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('example')
  );
}
 
setInterval(tick, 1000);
* JSX 执行更快，因为它在编译为 JavaScript 代码后进行了优化
* 你的 React JSX 代码可以放在一个独立文件上：ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('example')
);
* 可以在 JSX 中使用 JavaScript 表达式。表达式写在花括号 {} 中；在 JSX 中不能使用 if else 语句，但可以使用 conditional (三元运算) 表达式来替
* React 推荐使用内联样式。我们可以使用 camelCase 语法来设置内联样式. React 会在指定元素数字后自动添加 px 。以下实例演示了为 h1 元素添加 myStyle 内联样式：
var myStyle = {
    fontSize: 100,
    color: '#FF0000'
};
ReactDOM.render(
    <h1 style = {myStyle}>菜鸟教程</h1>,
    document.getElementById('example')
);
* 注释需要写在花括号中，实例如下：ReactDOM.render(
    <div>
    <h1>菜鸟教程</h1>
    {/*注释...*/}
     </div>,
    document.getElementById('example')
);
* JSX 允许在模板中插入数组，数组会自动展开所有成员：
var arr = [
  <h1>菜鸟教程</h1>,
  <h2>学的不仅是技术，更是梦想！</h2>,
];
ReactDOM.render(
  <div>{arr}</div>,
  document.getElementById('example')
);
* function HelloMessage(props) {
    return <h1>Hello World!</h1>;
}
 
const element = <HelloMessage />;
 
ReactDOM.render(
    element,
    document.getElementById('example')
);
* 1、我们可以使用函数定义了一个组件 可以使用 ES6 class 来定义一个组件
* class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
 
  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
 
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
 
  tick() {
    this.setState({
      date: new Date()
    });
  }
 
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>现在是 {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
 
ReactDOM.render(
  <Clock />,
  document.getElementById('example')
);
