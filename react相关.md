#  
[React性能优化总结 ](https://github.com/Pines-Cheng/blog/issues/3)  
[Immutable 详解及 React 中实践](https://github.com/camsong/blog)


https://juejin.im/post/5abf4a09f265da237719899d

#### 生命周期

> [React 源码剖析系列 － 生命周期的管理艺术](https://zhuanlan.zhihu.com/p/20312691)
![](/images/1531798876dr.png)  

#### SSR
> [Vue SSR 指南](https://ssr.vuejs.org/zh/#%E4%BB%80%E4%B9%88%E6%98%AF%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E6%B8%B2%E6%9F%93-ssr-%EF%BC%9F)

概念
  - 客户端渲染：页面在 JavaScript，CSS 等资源文件加载完毕后开始渲染，路由为客户端路由，也就是我们经常谈到的 SPA（Single Page Application）。
  - 服务端渲染：页面由服务端直接返回给浏览器，路由为服务端路由，URL 的变更会刷新页面，原理与 ASP，PHP 等传统后端框架类似。
  - 同构：英文表述为 Isomorphic 或 Universal，即编写的 JavaScript 代码可同时运行在浏览器及 Node.js 两套环境中，用服务端渲染来提升首屏的加载速度，首屏之后的路由由客户端控制，即在用户到达首屏后，整个应用仍是一个 SPA。

优缺点  

- 客户端渲染：构建方便，部署简单（可以部署在任何静态文件服务器上）
- 服务端渲染：SEO，首屏加载速度

服务端 SSR 需要注意的点 
- 开发条件所限。  
浏览器特定的代码，只能在某些生命周期钩子函数(lifecycle hook)中使用；一些外部扩展库(external library)可能需要特殊处理，才能在服务器渲染应用程序中运行。  
比如，一些第三方库只能在 react 生命周期 ComponentDidMount 中运行。
- 涉及构建设置和部署的更多要求。  
与可以部署在任何静态文件服务器上的完全静态单页面应用程序(SPA)不同，服务器渲染应用程序，需要处于 Node.js server 运行环境。
- 更多的服务器端负载。  
在 Node.js 中渲染完整的应用程序，显然会比仅仅提供静态文件的 server 更加大量占用 CPU 资源(CPU-intensive - CPU 密集)，因此如果你预料在高流量环境(high traffic)下使用，请准备相应的服务器负载，并明智地采用缓存策略。

方法  
- `react-dom/server` 中 `renderToString` 和 `renderToStaticMarkup` 方法

其他

> [React16中的服务端渲染（译）](http://imweb.io/topic/59dc46db856028aa249e2a57)  - React 16 支持 Streaming

##### 总结参考 
> [React 16 加载性能优化指南](https://zhuanlan.zhihu.com/p/37148975)  

这篇文章里，我们一共提到了下面这些优化加载的点：  
- 在 HTML 内实现 Loading 态或者骨架屏；  
- 去掉外联 css；  
- 缓存基础框架；  
- 使用动态 polyfill；  
- 使用 SplitChunksPlugin 拆分公共代码；  
- 正确地使用 Webpack 4.0 的 Tree Shaking；  
- 使用动态 import，切分页面代码，减小首屏 JS 体积；  
- 编译到 ES2015+，提高代码运行效率，减小体积；  
- 使用 lazyload 和 placeholder 提升加载体验。  
  
> [React v16.3 版本新生命周期函数浅析及升级方案](https://zhuanlan.zhihu.com/p/36062486)  

##### noflux  
> [noflux 中文](https://noflux.js.org/zh/migration/)  

- Noflux 所暴露的接口非常少，准确讲只有 state 与connect。  
(1) state 维护着全局唯一的状态，并提供如 get、set 之类的接口供数据操作。
与 Redux 类似，Noflux 使用 单一数据源 ，**且 state 是不可变的（immutable）**——虽然它的操作方法看起来不像。  
(2) @connect 修饰符将跟踪 state 的变化并智能的重新渲染组件。   
如果一个组件通过 state.get 获取的值被修改了，那么这个组件将通过 forceUpdate 被重新渲染，这意味着它的 render 方法将会被调用。





























