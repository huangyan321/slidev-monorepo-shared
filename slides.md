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
  <div text-sm opacity-50>2022/12/10</div>
  <div text-sm opacity-50>Author: 王伟平</div>
</div>

---

# 思考：现有仓库管理方式遇到了什么问题？

<v-clicks>

可以先贴一张gif，然后演示目前打包等等的不足之处

</v-clicks>
---

如今大部分的前端应用会采用Multi repo，即每个独立的项目都会有相对应的repo，对于维护自己的项目分清责任也很容易。
（这里插入公司的各个项目）

```
Design-systems Repository
design-systems
  ├ node_modules
  ├ e2e
  ├ xxxx
Admin Repository
admin
  | ├ node_modules
  | ├ e2e
  | ├ xx...
```

<br>
<br>
<v-clicks>

这种方式看似不错，但也会带来一些问题

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

对于我们团队的前端项目，目前选定的技术栈已经正在向 jquery -> vue2.6 -> vue2.7 -> vue3.x 的方向演进，总体技术生态已经基本固定。这时候大部分项目所安装的依赖库都有重复
<v-clicks>

// 贴上相关package

</v-clicks>
---

## 工程配置重复

<div mt-4/>

<v-clicks>

贴上具体案例

</v-clicks>
<v-clicks>

- webpack、vite配置管理，兼容性问题

- 开发环境

- 多仓库手动部署

</v-clicks>

---

## 跨项目代码难共享

<v-clicks>

贴例子

</v-clicks>

---
layout: center
---

# Monorepo

---

## 什么是Monorepo

Monorepo 是一种项目代码管理方式，指单个仓库中管理多个项目。并不是一种工具，它只是对于项目的一种管理手段，一种思维方式。

<v-clicks>

- 统一管理 configs and tests。只有一个 repo 所以不需要再重复配置环境，包括 CI/CD、unit、e2e、webpack 都只需要维护一份就好。

- 统一管理 依赖。

- 复用模块代码以及share code

- 简化组织

- 减少重复依赖项

- 跨项目代码共享

</v-clicks>

---

# 经典开源案例

<v-clicks>

贴几个开源案例

</v-clicks>

---

# pnpm： Workspace

贴上具体的案例
---

# 简易实现 Monorepo

---

# 项目实践

---

# TurboRepo

---

# Monorepo的缺点

monorepo也有一些不足的地方

<v-clicks>

- 无法管理某个、某些项目对于指定人员的权限

- 不同分支下的版本控制会显得较为混乱（medical-device bedside-terminal）

- 发布构建的难度较大

- 不适用于业务相对零散、项目之间关系不大的场景
</v-clicks>

---
layout: center
---
## 无论是对于代码层面的设计，亦或是仓库管理层面的设计思想，都像踩跷跷板一样，没有最好，只有最适合
---

## 查阅以下链接了解更多

[Turbo: what-is-a-monorepo](https://turbo.build/repo/docs/handbook/what-is-a-monorepo)  
[项目级 monorepo 策略最佳实践](https://zhuanlan.zhihu.com/p/348898271)  

---

# Thank You
