---
highlighter: shiki
fonts:
  mono: Input Mono
info: |
  操作系统课上的分享
---

# 包管理工具是如何处理 node_modules 的

Made with Slidev

<div class="abs-bl !mx-14 my-12 flex flex-col">
  <div class="mb-3 uppercase tracking-widest font-500">
  Hyoban
  </div>
  <div class="text-md opacity-50">Wuhu, China 2022</div>
</div>

<style>
p {
  @apply text-xl;
}
</style>

---
layout: center
class: text-center
---

# node_modules 安装方式

Nested installation 和 Flat installation

---
---

# Nested installation 嵌套安装

npm@3 之前

<img v-motion-slide-visible-left v-click-hide class="h-64" src="https://user-images.githubusercontent.com/38493346/168409843-67246227-2db6-4ff8-86cc-00377ba70fc1.png">

<div class="grid grid-cols-2 gap-x-4 gap-y-4">

<v-after>

###### 嵌套安装的优势

###### 嵌套安装存在的问题

</v-after>

<v-clicks>

- 干净，可预测
- 每个依赖项拥有自己的 node_modules

</v-clicks>

<v-clicks>

- 过深的依赖树，Windows上目录过长
- 磁盘空间浪费，相同的依赖存在多份文件

</v-clicks>

</div>

---
---

# Flat installation 扁平安装

npm@3+ 和 yarn中，随机提升多版本中的一个包

<img v-motion-slide-visible-left v-click-hide class="h-64 pb-10" src="https://user-images.githubusercontent.com/38493346/168409780-67eb383b-39bd-47e6-9d36-9c4c4d1f8503.png">

<div class="grid grid-cols-2 gap-x-4 gap-y-4">

<v-after>

###### 扁平安装的优势

###### 扁平安装存在的问题

</v-after>

<v-clicks>

- 改变了嵌套安装的情况
- 有限的节省了磁盘空间

</v-clicks>

<v-clicks>

- Phantom dependencies 幽灵依赖
- NPM doppelgangers NPM分身

</v-clicks>

</div>

---
layout: center
class: text-center
---

# pnpm 的做法

网状 + 平铺的node_modules结构

---
---

# 网状 + 平铺的 node_modules 结构

<img
  v-click-hide
  v-motion-slide-visible-top
  class="py-4 w-4/5" 
  src="https://pnpm.io/zh/assets/images/node-modules-structure-8ab301ddaed3b7530858b233f5b3be57.jpg">

<v-after>
<div class="mt-10"></div>
<p>总结</p>
<ul>
  <li>pnpm 拥有自己的 .pnpm 目录，它会以平铺的方式来存储所有的包。</li>
  <li>以依赖名加上版本号的方式命名，实现了版本的复用。</li>
  <li>它不是通过拷贝机器缓存中的依赖到项目目录下，而是通过硬链接的方式，这能减少空间占用。</li>
  <li>至于根目录下用于项目使用的依赖则是通过符号链接的方式，链接到它在 .pnpm 目录下的对应位置。</li>
</ul>
</v-after>

---
---

# 为什么不直接创建到全局存储的符号链接？

一台机器上一个包在可以有不同的依赖集。

在项目 A foo@1.0.0 可以具有一个依赖被解析为 bar@1.0.0，但在项目 B 中 foo 的依赖可能会被解析至 bar@1.1.0; 因此，pnpm 硬链接 foo@1.0.0 到每个使用它的项目，以便为其创建不同的依赖项集。

---
---

# shamefully-hoist

默认情况下，通过 pnpm 的 node_modules 你只能访问到在 package.json 文件中声明了的依赖

你可能需要在 .npmrc 中配置 node_modules 形式为和 npm 类似的平铺方式。

这是因为某些工具它只认根目录中的依赖。

不过事实上 pnpm 严格模式能够帮我们避免一些低级的错误，你可以阅读 [pnpm's strictness helps to avoid silly bugs](https://www.kochan.io/nodejs/pnpms-strictness-helps-to-avoid-silly-bugs.html)

---
---

# peer-dependencies

你需要手动安装 peer-dependencies，需要额外安装时会在命令行提示。

比如 vuepress 项目，如果使用 pnpm 的话，在你配置了 shamefully-hoist 的本地运行和构建都没问题，而在 vercel 的 node 14 版本上构建时会报错。
这是因为本地的依赖被提升，而 vercel 上面没有。

> Error: [vite]: Rollup failed to resolve import "@vuepress/client" from "docs/.vuepress/.temp/internal/pagesRoutes.js".

你需要手动安装 vue 和 @vuepress/client

关于是否应该自动安装 peerDependencies 的讨论，可以参考 [automatically install peerDependencies](https://github.com/pnpm/pnpm/discussions/3995)


---
layout: center
class: 'text-center pb-5 :'
---

# 谢谢！

幻灯片可以在我的网站 [hyoban.cc](https://hyoban.cc) 上下载
