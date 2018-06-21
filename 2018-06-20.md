# 搭建React项目  
package.json 文件
```
npm init
```
#### Eslint
初始化，按照问题选择即可，一般选择 Airbnb 规范，相应的编辑器上安装 eslint 插件.  
package script: `eslint --ext js --ext jsx .`  
相关文件 ： `.eslintrc.yml`,`eslintignore`
```
eslint --init
? How would you like to configure ESLint? Use a popular style guide
? Which style guide do you want to follow? Airbnb
? Do you use React? Yes
? What format do you want your config file to be in? YAML

// .eslintrc.yml
extends: airbnb
env:
  browser: true
  node: true
rules:
  import/no-extraneous-dependencies: off
  semi:
    - error
    - never
  react/prop-types: off
  comma-dangle: off
  react/jsx-filename-extension: off

```  
#### Babel  
ES6/7规范中新特性的加入（比如箭头函数、async/await等），可以让开发者书写更优雅、简洁的代码。但是由于各大浏览器并未全面实现最新的ECMAScript规范。为了更好的兼容性，想要使用这些新特性就必须将ES6/7代码`转换为ES5代码`供浏览器运行。  

Babel的配置文件是.babelrc，存放在项目的根目录下。  
该文件用来设置转码规则和插件，基本格式如下。
```
{
  "presets": [],
  "plugins": []
}
```
**presets 规则集：**  不想自己单独配置各个plugins时，或没有特殊plugin需求，可直接使用预设规则集）。presets 分为官方维护的规则集和npm社区维护的规则集。
> [参考](https://zhuanlan.zhihu.com/p/35888257)

官方规则集如下：
```
# env转码规则
$ npm install --save-dev babel-preset-env

# ES每年规范的转码规则
$ npm install --save-dev babel-preset-es2015
$ npm install --save-dev babel-preset-es2016
$ npm install --save-dev babel-preset-es2017

# react转码规则
$ npm install --save-dev babel-preset-react

# flow静态类型检查转码规则
$ npm install --save-dev babel-preset-flow

# ES7不同阶段*语法提案*的转码规则
$ npm install --save-dev babel-preset-stage-0
$ npm install --save-dev babel-preset-stage-1
$ npm install --save-dev babel-preset-stage-2
$ npm install --save-dev babel-preset-stage-3

# stage-4 完成: 将被添加到下一个年度版本
$ npm install --save-dev babel-preset-stage-4
```
**plugins 为插件集：** presets 其实是一堆plugins的预设，起到方便的作用。如果你不采用presets，完全可以单独引入某个功能，比如以下的设置就会引入编译箭头函数的功能。
> [各种插件](https://babeljs.io/docs/en/plugins/#transform-plugins)
```json
{
  "plugins": ["transform-es2015-arrow-functions"]
}
```

将安装好的规则加入到 .babelrc 文件中  
```json
{
    "presets": ["es2017", "react"],
    "plugins": []
}
```
**其中 babel-preset-env 规则可以根据配置的目标运行环境（environment）自动启用需要的 babel 插件。（可以避免 环境（浏览器、node...）已经原生实现规范，Babel却还将代码转换为繁琐的ES5代码）** 

> 官网：Each yearly preset only compiles what was ratified in that year. babel-preset-env replaces es2015, es2016, es2017 and latest
每年预设仅编译当年批准的内容。 babel-preset-env取代了es2015，es2016，es2017和最新版本。

所以配置.babelrc更加简单。
> [参考](http://2ality.com/2017/02/babel-preset-env.html)
```json
npm install babel-preset-env --save-dev

/* 
* 配置
* 参考：https://www.babeljs.cn/docs/plugins/preset-env/
*／

{
  "presets": ["env"],
  "plugins": []
}
```
 使用：babel-loader, babel-core
 
 **Babel是如何读懂JS代码的**  
 > https://zhuanlan.zhihu.com/p/27289600  
 https://zhuanlan.zhihu.com/p/27305941  
 
 #### webpack  
 webpack-dev-server  
 > [参考](https://segmentfault.com/a/1190000006670084)
 
 webpack-dev-server主要是启动了一个使用express的Http服务器。它的作用主要是用来伺服资源文件。此外这个Http服务器和client使用了websocket通讯协议，原始文件作出改动后，webpack-dev-server会实时的编译，但是最后的编译的文件并没有输出到目标文件夹，即上面配置。  
webpack-dev-server 支持自动刷新和模块热替换机制
> [webpack-flow](http://taobaofed.org/blog/2016/09/09/webpack-flow/)




 
