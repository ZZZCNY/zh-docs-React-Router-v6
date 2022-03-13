# React Router V6 来了

React Router v6 在客户端路由方面已经走过了十年，它从以前的版本和它的姐妹项目 Reach Router 中获得了最好的功能，是我们目前最小和最强大的软件包。

[开始教程](https://github.com/ZZZCNY/zh-docs-React-Router-v6/blob/823c2b0ea3dafbe687f8bef2c1c65e587ce03938/%E5%85%A5%E9%97%A8/%E6%95%99%E7%A8%8B.md)

---

## 嵌套式路由

大多数应用程序都有一系列围绕页面主要部分的嵌套式布局。这些布局几乎总是与 URL 段相联系。

每个应用程序都有一些始终在渲染的根布局，无论你使用什么路由器，这部分都很容易。

但是随着 URL 段的增加，新的布局也被添加到用户界面中。

有时它变得很深，你必须在应用程序的所有路由中重复这些布局层次。

有四个层次的布局是很常见的!

有了 React Router，这些都是内置的。嵌套路由将段添加到 URL 中，并将布局添加到 UI 层次结构中。随着 URL 的变化，你的布局也会自动改变。

```js
<Route path='/' element={<App />}>
  <Route path='sales' element={<Sales />}>
    <Route path='invoices' element={<Invoices />}>
      <Route path=':invoice' element={<Invoice />} />
    </Route>
  </Route>
</Route>
```

---

## 路由排名

有时一个类似的 URL 可以匹配一个以上的路由模式。React Router 对你的路由进行排名，并挑选出最好的一个。

如果你访问 `https://myapp.com/teams/new`，React Router 将呈现 `<NewTeam />`，因为它比 `:teamId` 参数更具体。不用再为精确的 props 或需要注意（但很容易出错）的路由排序而烦恼了!

```js
<Routes>
  <Route path='teams/:teamId' element={<Team />} />
  <Route path='teams/new' element={<NewTeam />} />
</Routes>
```

---

| GITHUB 用户 | 贡献者 | NPM 下载量 | 在 REACT 应用中 |
| ----------- | ------ | ---------- | --------------- |
| 2.4M        | 600+   | 3.6M       | 70%             |

---

## 保持联系

React Router 是由 [Remix](https://remix.run/) 团队开发的。要获得 React Router（以及我们的其他项目）的更新和特别内容，请订阅 Remix 通讯或[在 Discord 上加入对话](https://discord.gg/VBePs6d)。

![](https://reactrouter.com/discord.png)
