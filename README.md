# react 练习项目
使用 react 16.6.0（截止 2018-11-05 的最新版）。      
用 Create React App 初始化项目：  
```
npx create-react-app react-and-redux-demo
```
然后以《深入浅出React和Redux》这本书中的例子代码为基础，实际操作和演练。
《深入浅出React和Redux》，第三章，《从Flux 到Redux》，如果你不了解、也没有用过 Flux，建议跳过 3.1，直接看 3.2。

参考  
1. [《深入浅出React和Redux》代码](https://github.com/mocheng/react-and-redux)
1. [react 中文社区文档](https://react.docschina.org/docs/hello-world.html)
1. [Create React App official website,Getting Started](https://facebook.github.io/create-react-app/docs/getting-started)

# 欢迎提交 PR
本项目主要针对 react 全家桶技术栈，以学习、演示基础代码为目的，欢迎补充知识点与相关示例代码。
可通过 fork + pull request 的方式，参与到该项目。以下是两大平台的帮助文档。
* gitee.com  -> [Fork + Pull 模式 ](https://gitee.com/help/articles/4128)
* github.com -> [Creating a pull request from a fork](https://help.github.com/articles/creating-a-pull-request-from-a-fork/)

# 个人整理的相关知识点文档
1. [开发前的准备工作、相关知识储备](./doc/prepare.md)
1. [js 知识点、参考链接](./doc/js.md)
1. [redux 知识点、参考链接](./doc/redux.md)

# master 分支
为 Create React App 初始化项目，之后的练习代码都会体现到这个分支。  
针对《深入浅出React和Redux》一书中，某一个被挑选的例子，完成之后，会创建一个相应的分支。  

# 获取（切换至）某分支
以分支 branchName 为例，切换到该分支并拉取最新代码
```
git checkout branchName
git pull
```

# 例子代码
第一章代码位于 chapter-01，第二章的代码位于  chapter-02，依次类推。  
子目录名即为分支名，如第四章代码目录下的子目录：`todo_controlled_component`，会有一个对应分支也叫 `todo_controlled_component`。

# PropTypes 依赖变化
react 的类型检查 PropTypes 自 React v15.5 起已弃用，请使用 prop-types。
《深入浅出React和Redux》一书示例代码使用的 react 是 15.4.1 版本，需要调整 PropTypes 的引用：
```
// 书中的代码是
import { PropTypes } from 'react';
// 要改为：
import PropTypes from 'prop-types';
```

扩展阅读：[使用 PropTypes 进行类型检查](https://react.docschina.org/docs/typechecking-with-proptypes.html)

# 第二章
## 分支 controlpanel
[查看分支](https://gitee.com/elsafly/react-and-redux-demo/tree/controlpanel)

### 知识点
1. 组件。
1. 组件的 state、props。
1. 父组件通过 props 向子组件传递数据。

## 分支 controlpanel_with_summary
[查看分支](https://gitee.com/elsafly/react-and-redux-demo/tree/controlpanel_with_summary)

### 知识点
1. 组件的 props，父组件向子组件传递数据，包括传递函数。
1. 子组件通过调用父组件的函数，来达到向父组件传递数据的目的。

# 第三章
## 分支 react-redux
[查看分支](https://gitee.com/elsafly/react-and-redux-demo/tree/react-redux)

到项目根目录，添加 redux 和 react-redux 依赖。  
以下操作会添加最新版的 redux（截止 2018-11-06，版本为：4.0.1） 和 react-redux（截止 2018-11-06，版本为：5.1.0）
```
cnpm i redux --save
cnpm i react-redux --save
```
如果不事先添加 redux 依赖而直接添加 react-redux 依赖，会有警告：
```
peerDependencies WARNING react-redux@* requires a peer of redux@^2.0.0 || ^3.0.0 || ^4.0.0-0 but none was installed
```

### 知识点
1. UI 组件（presentational component）（傻瓜组件） 
1. 容器组件（container component）
1. 应用 redux 的三大原则
1. React-Redux 库
    * connect(mapStateToProps, mapDispatchToProps)
    * mapStateToProps
    * mapDispatchToProps

相关知识点，已经总结到文档：[redux 知识点、参考链接](./doc/redux.md)

# 第四章

### 知识点
#### 代码文件组织结构，以及确定模块的边界。
参考《深入浅出React和Redux》P75-81。
1. 推荐目录组织方式：按照功能组织。
1. 把一个目录看做一个模块，那么我们要做的是明确这个模块对外的接口，而这个接口应该实现把内部封装起来。
1. 目录下人 index.js 文件，就是我们的模块接口。
1. 各个模块之间只能假设其他模块包含 index.js 文件，要引用模块只能导入 index.js，不能够直接去导人其他文件。
1. 导人一个目录的时候，默认导人的就是这个目录下的 index.js 文件， index.js 文件中导出的内容，就是这个模块想要公开出来的接口。
1. 推荐使用 export（命名式）的方式导出模块，而不是用 export default（默认）的方式，因为 export default 在导入时，会增加代码量。

#### 状态树的设计
参考《深入浅出React和Redux》P81-83。
1. 一个模块控制一个状态节点。 
1. 避免冗余数据。
1. 树形结构扁平。
1. 只能通过 reducer 纯函数修改 state，不能直接修改 state。
    * 所以，push 和 unshift 会改变原来那个数组，是不能直接作用于 state 的。
    * 利用扩展操作符。
