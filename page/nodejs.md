* Node.js 就是运行在服务端的 JavaScript
* console.log("Hello World");  node helloworld.js
* 1. 高并发  2. 适合I/O密集型应用
* Nnigx反向代理，负载均衡，开多个进程，绑定多个端口
* 开多个进程监听同一个端口，使用cluster模块
* Web开发有两个UI层，一个是在浏览器里面我们最终看到的，另一个在server端，负责生成和拼接页面
* 但是有另外一种实践，面向服务的架构，更好的做前后端的依赖分离。如果所有的关键业务逻辑都封装成REST调用，就意味着在上层 只需要考虑如何用这些REST接口构建具体的应用。那些后端程序员们根本不操心具体数据是如何从一个页面传递到另一个页面的，他们也不用管用户数据更新是 通过Ajax异步获取的还是通过刷新页面
* NodeJS适合运用在高并发、I/O密集、少量业务逻辑的场景
* npm init  npm install --save express  
body-parser
cookies
markdown
mongoose
swig
* db/model/public/routers/schemas/views/app.js
* 模块化开发：SeaJS基于CMD的模块化开发解决方案
* node是门技术不是语言   Node 是一个可以解析和执行 JavaScript 代码的 运行时环境
* V8 JavaScript 解析执行引擎 ECMAScript->中间层 （提供了文件操作、网络操作登陆接口）更加接近操作系统的接口供开发人员使用->硬件层
* 可以使用 require 指令来载入 Node.js 模块
* NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题:
  允许用户从NPM服务器下载别人编写的第三方包到本地使用
  允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用
  允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用
* npm uninstall express npm ls  npm update express npm search express npm init npm adduser npm publish
  npm install -g cnpm --registry=https://registry.npm.taobao.org cnpm install [name]
* fs.readFile('input.txt', function (err, data) {
    if (err) return console.error(err);
    console.log(data.toString());
});
* var data = fs.readFileSync('input.txt');
