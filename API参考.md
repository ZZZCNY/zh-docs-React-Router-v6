# [API 参考](#api-参考)

React Router 是 [React 组件](https://zh-hans.reactjs.org/docs/components-and-props.html)、[hooks](https://zh-hans.reactjs.org/docs/hooks-intro.html) 和实用程序的集合，它使 [React](https://zh-hans.reactjs.org/) 构建多页面应用程序变得容易。本参考包含 React Router 中各种接口的函数签名和返回类型。

## [概述](#概述)

### [包](#包)

React Router 以三个不同的包发布到 npm。

- [`react-router`](https://npm.im/react-router) 包含了 React Router 的大部分核心功能，包括路由匹配算法和大部分的核心组件和 hooks。
- [`react-router-dom`](https://npm.im/react-router-dom) 包括 `react-router` 的所有内容，并增加了一些 DOM 特定的 API，包括 [`<BrowserRouter>`](https://reactrouter.com/docs/en/v6/api#browserrouter)、[`<HashRouter>`](https://reactrouter.com/docs/en/v6/api#hashrouter) 和 [`<Link>`](https://reactrouter.com/docs/en/v6/api#link)。
- [`react-router-native`](https://npm.im/react-router-native) 包括 `react-router` 的所有内容，并增加了一些特定于 React Native 的 API，包括 [`<NativeRouter>`](https://reactrouter.com/docs/en/v6/api#nativerouter) 和[一个本地版本的 `<Link>`](https://reactrouter.com/docs/en/v6/api#link-react-native)。

当你安装 `react-router-dom` 和 `react-router-native` 时，它们都会自动将 `react-router` 作为一个依赖项，并且这两个包都会从 `react-router` 重新导出所有东西。**当你 `import` 东西时，你应该总是从 `react-router-dom` 或 `react-router-native` 导入，而不是直接从 `react-router`。**否则，你可能会意外地在你的应用程序中导入不匹配的库的版本。

如果你把 React Router [安装](https://reactrouter.com/docs/en/v6/getting-started/installation)为全局（使用 `<script>` 标签），你可以在 `window.ReactRouterDOM` 对象上找到这个库。如果你从 npm 安装它，你可以 [`import`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/import) 你需要的部分。本参考文献中的例子都使用了 `import` 语法。

### [设置](#设置)

为了让 React Router 在你的应用程序中工作，你需要在你的元素树的根部或附近渲染一个路由器元素。我们提供了几种不同的路由器，这取决于你的应用程序的运行位置。

- [`<BrowserRouter>`](https://reactrouter.com/docs/en/v6/api#browserrouter) 或 [`<HashRouter>`](https://reactrouter.com/docs/en/v6/api#hashrouter) 应在网络浏览器中运行时使用（你选择哪一个取决于你喜欢或需要的 URL 的风格）。
- [`<StaticRouter>`](https://reactrouter.com/docs/en/v6/api#staticrouter) 应该在服务器渲染网站的时候使用。
- [`<NativeRouter>`](https://reactrouter.com/docs/en/v6/api#nativerouter) 应该在 [React Native](https://reactnative.dev/) 应用中使用。
- [`<MemoryRouter>`](https://reactrouter.com/docs/en/v6/api#memoryrouter) 在测试场景中很有用，可以作为其他路由器的参考实现。
- [`<unstable_HistoryRouter>`](https://reactrouter.com/docs/en/v6/api#unstable_historyrouter) 与你自己的 [`history`](https://github.com/remix-run/history) 实例一起使用。

这些路由器提供了 React Router 在特定环境中运行所需的环境。每一个都在内部渲染了[一个 `<Router>`](https://reactrouter.com/docs/en/v6/api#router)，如果你因为某些原因需要更精细的控制，你也可以这么做。但极有可能的是，内置路由器中的一个就是你所需要的。

### [路由](#路由)

路由是决定哪些 React 元素将在你的应用程序的特定页面上被渲染，以及它们将如何被嵌套的过程。React Router 提供了两个接口来声明你的路由。

- [`<Routes>` 和 `<Route>`](https://reactrouter.com/docs/en/v6/api#routes-and-route)，如果你使用 JSX 的话。
- 如果你喜欢基于 JavaScript 对象的配置，可以使用 [`useRoutes`](https://reactrouter.com/docs/en/v6/api#useroutes)。

我们内部使用的一些低层次的部分也以公共 API 的形式公开，以备你因某些原因需要建立自己的高层次接口。

- [`matchPath`](https://reactrouter.com/docs/en/v6/api#matchpath) - 与 URL 路径名匹配的路径模式。
- [`matchRoutes`](https://reactrouter.com/docs/en/v6/api#matchroutes) - 匹配一组路由与一个[地点](https://reactrouter.com/docs/en/v6/api#location)。
- [`createRoutesFromChildren`](https://reactrouter.com/docs/en/v6/api#createroutesfromchildren) - 从一组 React 元素（即 [`<Route>`](https://reactrouter.com/docs/en/v6/api#routes-and-route) 元素）创建一个路由配置。

### [导航](#导航)

React Router 的导航界面让你通过修改当前的[位置](https://reactrouter.com/docs/en/v6/api#location)来改变当前渲染的页面。有两个主要的界面用于在你的应用程序中的页面之间进行导航，这取决于你的需要。

- [`<Link>`](https://reactrouter.com/docs/en/v6/api#link) 和 [`<NavLink>`](https://reactrouter.com/docs/en/v6/api#navlink) 渲染一个可访问的 `<a>` 元素，或者是 React Native 上的 `TouchableHighlight`。这让用户可以通过点击或轻触页面上的某个元素来启动导航。
- [`useNavigate`](https://reactrouter.com/docs/en/v6/api#usenavigate) 和 [`<Navigate>`](https://reactrouter.com/docs/en/v6/api#navigate) 让你以编程方式进行导航，通常是在一个事件处理程序中或对状态的某些变化做出反应。

有一些我们内部使用的低级别的 API，在建立你自己的导航界面时也可能被证明是有用的。

- [`useResolvedPath`](https://reactrouter.com/docs/en/v6/api#useresolvedpath) - 根据当前[位置](https://reactrouter.com/docs/en/v6/api#location)解析一个相对路径。
- [`useHref`](https://reactrouter.com/docs/en/v6/api#usehref) - 解析一个适合用作 `<a href>` 的相对路径。
- [`useLocation`](https://reactrouter.com/docs/en/v6/api#uselocation) 和 [`useNavigationType`](https://reactrouter.com/docs/en/v6/api#usenavigationtype) - 这些描述了当前的[位置](https://reactrouter.com/docs/en/v6/api#location)和我们如何到达那里的。
- [`useLinkClickHandler`](https://reactrouter.com/docs/en/v6/api#uselinkclickhandler) - 在 `react-router-dom` 中建立一个自定义的 `<Link>` 时，返回一个事件处理程序，用于导航。
- [`useLinkPressHandler`](https://reactrouter.com/docs/en/v6/api#uselinkpresshandler) - 在 `react-router-native` 中构建自定义 `<Link>` 时，返回一个事件处理程序，用于导航。
- [`resolvePath`](https://reactrouter.com/docs/en/v6/api#resolvepath) - 根据给定的 URL 路径名解析一个相对路径。

### [搜索参数](#搜索参数)

对 URL [搜索参数](https://developer.mozilla.org/zh-CN/docs/Web/API/URL/searchParams)的访问是通过 [`useSearchParams` hook](https://reactrouter.com/docs/en/v6/api#usesearchparams) 提供的。

---

## [参考资料](https://reactrouter.com/docs/en/v6/api#reference)

> 待翻译
