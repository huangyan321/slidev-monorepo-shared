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
优化代码管理，提供更好的可重用性和协作性
</p>

<div abs-bl mx-14 my-12 flex flex-col>
  <div text-sm opacity-50>2023/06/02</div>
  <div text-sm opacity-50>Author: huangyan321</div>
</div>

---
layout: two-cols
---

# 现有仓库管理方式
<v-click>

我们大部分前端应用都采用`Multi repo`的方式来管理，即每个独立的项目都有相对应的`repo`，很容易维护自己的项目、并且分清责任。
</v-click>
::right::
<v-click>

```
queue-admin
  ├ node_modules
  ├ src
  ├ xxxx
hos-admin
  ├ node_modules
  ├ src
  ├ xx...
medical-device
  ├ node_modules
  ├ src
  ├ xx...
bedside-terminal
  ├ node_modules
  ├ src
  ├ xx...
device
  ├ html
  ├ css
  ├ js
  ├ xx...
chart
```

<br>
<br>
</v-click>
---

# 遇到什么问题？



<v-clicks>

- 跨服务和项目使用的公共依赖和库必须定期同步以获得最新版本。（列举一下element-plus遇到的bug）
- 如使用同一技术栈的项目：data-admin device-admin，如果在开发中遇到了某些依赖库的bug，需要在多个仓库中同时更新。
- 每个仓库都遵循不同的一组最佳实践来编写代码，从而导致难以遵循通用的最佳实践。
- node-modules 重复空间占用巨大。

</v-clicks>
---


<v-clicks>

所以这种仓库管理模式看似不错，但也会带来一些问题。

</v-clicks>

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

对于团队而言，目前选定的技术栈已经从 jquery 、 vue2.6 向 vue2.7 、 vue3.x 的方向演进，总体技术生态稳定。此时大部分新项目所安装的依赖库都有重复

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

## 跨项目代码难共享


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

- 统一管理 configs and tests。只有一个 repo 所以不需要再重复配置环境，包括 CI/CD、unit、e2e、webpack 都只需要维护一份就好。

- 统一管理 依赖，减少重复依赖项。

- 复用模块代码

- 简化组织

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

# pnpm 工作空间功能

Workspace 协议 (workspace:): 当使用此协议时，pnpm 将拒绝解析除本地 workspace 包含的 package 之外的任何内容。 因此，如果您设置为 "foo": "workspace:2.0.0" 时，安装将会失败，因为 "foo@2.0.0" 不存在于此 workspace 中
---

# 实现简易的 Monorepo
熟悉构建流程
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
