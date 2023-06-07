---
theme: Seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: true
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
title: Welcome to Slidev
colorSchema: light
---

# 前端工程化-Monorepo

<p text-xl>
优化代码管理以增强其可重复使用性和协同工作效率。
</p>

<div abs-bl mx-14 my-12 flex flex-col>
  <div text-sm opacity-50>2023/06/02</div>
  <div text-sm opacity-50>Author: huangyan321</div>
</div>

---
layout: two-cols
---

要认识monorepo，首先要知道这个东西到底解决了什么问题，他为什么会出现，所以我们要清楚，没有monorepo的时候，出现了哪些问题

# 团队实行的仓库管理方式

<v-click  at="1">

#### 我们团队前端应用基本都采用 `Multi repo` 的策略来管理，即每个独立的项目都有相对应的 `repo` ，很容易维护自己的项目、并且分清责任。

</v-click>

::right::
<v-click at="0">

```
hos-admin
  |-- node_modules
  |-- src
  |-- xx...
medical-device
  |-- node_modules
  |-- src
  |-- xx...
bedside-terminal
  |-- node_modules
  |-- src
  |-- xx...
queue-admin-2.0
  |-- node_modules
  |-- src
  |-- xxxx
device-admin
  |-- node_modules
  |-- src
  |-- tsconfig.json
  |-- xxx
data-admin
  |-- node_modules
  |-- src
  |-- tsconfig.json
  |-- xxx
```
</v-click>
---

# 遇到什么问题？



<v-clicks>

- 使用同一技术栈的项目：`data-admin` `device-admin`，如在开发中遇到了某些依赖库的bug，需要在多个仓库中同时更新。
- 每个仓库都遵循不同的一组最佳实践来编写代码，从而导致难以遵循通用的最佳实践。
- node_modules 重复空间占用巨大。
- 跨服务和项目使用的公共依赖和库必须定期同步以获得最新版本。
  - 使用相同技术栈的项目：data-admin device-admin，在开发过程中遇到了某些依赖库的bug，我们需要在多个仓库中同时进行更新。
- 每个仓库都按照各自不同的最佳实践编写代码，这可能导致难以统一遵循通用的最佳实践
- node-modules 的重复依赖会占用大量的存储空间。
</v-clicks>


---


虽然这种仓库管理模式看起来很好，但它也可能会带来一些问题。


<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>


---

## 依赖项重复

对于我们的团队来说，目前选定的技术栈已经从 jQuery 和 Vue 2.6 向 Vue 2.7 和 Vue 3.x 进行了演进，整体技术生态稳定。然而，在这个过程中，我们发现大部分新项目所安装的依赖库都存在重复。

<div style="display: flex; justify-content: space-between;">
  <img src="path/to/image1.jpg" style="width: 30%;" alt="alt text" v-click />
  <img src="path/to/image2.jpg" style="width: 30%;" alt="alt text" v-click />
  <img src="path/to/image3.jpg" style="width: 30%;" alt="alt text" v-click />
</div>

---

## 工程配置重复

<div mt-4/>


<div style="display: flex; justify-content: space-between; text-align: center;">
  <div v-click>
    <img src="path/to/image1.jpg" style="width: 30%;" alt="alt text" />
    <p> 打包配置 </p>
  </div>
  <div v-click>
    <img src="path/to/image2.jpg" style="width: 30%;" alt="alt text" />
    <p> 开发环境配置 </p>
  </div>
  <div v-click>
    <img src="path/to/image3.jpg" style="width: 30%;" alt="alt text" />
    <p> 多仓库手动部署 </p>
  </div>
</div>

---

## 跨项目间的代码共享存在一定的困难


<div style="display: flex; justify-content: space-between;">
  <img src="path/to/image1.jpg" style="width: 30%;" alt="alt text" v-click />
  <img src="path/to/image2.jpg" style="width: 30%;" alt="alt text" v-click />
  <img src="path/to/image3.jpg" style="width: 30%;" alt="alt text" v-click />
</div>


---
layout: center
---

# Monorepo

---

## Monorepo 简介

monorepo 是一种将**多个项目代码**存储在**一个仓库**里的软件开发**策略**（"mono" 来源于希腊语 μόνος 意味单个的，而 "repo"，显而易见地，是 repository 的缩写）。

<v-clicks>

通过 monorepo 策略组织代码，我们的代码仓库的目录结构看起来会是这样：
```
.
├── pnpm-lock.yaml
├── pnpm-workspace.yaml
├── package.json
└── packages/ # 这里将存放所有子 repo 目录
    ├── project_1/
    │   ├── index.js
    │   ├── node_modules/
    │   └── package.json
    ├── project_2/
    │   ├── index.js
    │   ├── node_module/
    │   └── package.json
    ...
```

</v-clicks>

---

# 优点
<v-clicks>

- 统一管理 configs and tests。只有一个 repo 所以不需要再重复配置环境，包括 CI/CD、unit、e2e、webpack 都只需要维护一份就好。

- 统一管理 依赖，减少重复依赖项。

- 复用模块代码

- 简化组织，更易浏览项目

- 跨项目代码共享

</v-clicks>

---

# 经典开源案例

<div style="display: flex; justify-content: space-between; align-items: center; flex-flow: nowrap row; text-align: center;">
  <div class="w-80% m-2" v-click>
    <img src="/vue3.png" alt="alt text" />
    <p> vue3 </p>
  </div>
  <div class="w-50% m-2" v-click>
    <img src="/element-plus.png" alt="alt text" />
    <p> element-plus </p>
  </div>
  <div  class="w-50% m-2" v-click>
    <img src="/vben.png" alt="alt text" />
    <p> vben-admin </p>
  </div>
</div>

---

# Pnpm 
pnpm 是新一代 Node 包管理器，它由 npm/yarn 衍生而来，解决了 npm/yarn 内部潜在的风险，并且极大提升依赖安装速度。

<v-click>
Workspace 协议 (workspace:): 执行`pnpm install`时，默认情况下，如果可用的 `packages` 与已声明的可用范围相匹配，pnpm 将从工作区链接这些 `packages`。
</v-click>

<v-click  at="1">

<p style="width: 40%;float:right">Tip: 子包内的任何改动将被同步更改至该包所安装工作区的node_modules中，所以不用担心代码不同步的问题。</p>

</v-click>

<v-click at="0">
  <div style="display:flex;justify-content:flex-end">
  <img src="/pnpminstall.png" style="height: 40vh;" alt="alt text" /></div>
</v-click>


---

# 实现轻量化 Monorepo 方案
接触实现流程


---

# 项目实践

---

# TurboRepo

---

# Monorepo的缺点

软件开发领域从来没有「银弹」。monorepo 策略也并不完美。

<v-clicks>

- 无法管理某个、某些项目对于指定人员的权限

- 不同分支下的版本控制会显得较为混乱（medical-device bedside-terminal）

- 发布构建的难度较大

- 不适用于业务相对零散、项目之间关系不大的场景
</v-clicks>

---
layout: center
---
##  无论是对于代码层面的设计，亦或是仓库管理层面的设计思想，都像踩跷跷板一样，没有最好，只有最适合
---

## 查阅以下链接了解更多

[Turbo: what-is-a-monorepo](https://turbo.build/repo/docs/handbook/what-is-a-monorepo)  
[项目级 monorepo 策略最佳实践](https://zhuanlan.zhihu.com/p/348898271)  

---

# Thank You
