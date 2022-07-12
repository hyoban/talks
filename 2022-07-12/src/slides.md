---
highlighter: shiki
fonts:
  mono: Input Mono
info: |
  实验室内分享
---

# Git 和 GitHub

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
---

# 前置准备

<v-clicks>

1. 设置用户名 `git config [--global] user.name "<name>"`
2. 设置邮件 `git config [--global] user.email "<email address>"`
3. （可选）设置默认分支名 `git config --global init.defaultBranch <branchName>`
4. 查看设置情况 `git config --list`
5. （可选）[设置 ssh](https://docs.github.com/cn/authentication/connecting-to-github-with-ssh) `ssh-keygen -t ed25519 -C "your_email@example.com"`

</v-clicks>

<div class="h-10"></div>

<div v-click>

> 你也可以通过 [GitHub Desktop](https://desktop.github.com/) 来进行设置

</div>

---
layout: center
class: text-center
---

# Git 基础

init, add, commit, clone, push, pull

---
clicks: 3
---

# 初始化仓库

<div class="grid grid-cols-2 gap-x-4 gap-y-4">

###### 执行的操作

###### 对应的命令

<v-clicks at="1">

- 在当前文件夹下初始化 Git
- 创建文件夹并初始化 Git
- 从远端拉取仓库

</v-clicks>

<v-clicks at="1">

- `git init`
- `git init <project-name>`
- `git clone username@host:/path/to/repository`

</v-clicks>

</div>

---
clicks: 8
---

# 记录提交

<img v-motion-slide-visible-left v-click-hide class="h-48 rounded" src="https://rogerdudler.github.io/git-guide/img/trees.png">

<div class="grid grid-cols-2 gap-x-4 gap-y-4" v-click-hide>

<v-after>

###### 执行的操作

###### 对应的命令

</v-after>

<v-clicks at="2">

- 将改动记录到暂存区
- 提交记录到仓库
- 不记录部分指定文件
- 添加远端仓库
- 推送提交记录到远端
- 同步远端最新的提交

</v-clicks>

<v-clicks at="2">

- `git add <filename>` `git add *`
- `git commit -m "Commit message"`
- .gitignore
- `git remote add origin <server>`
- `git push origin main`
- `git pull`

</v-clicks>

</div>

<div class="h-10">
</div>

<v-clicks at="8">

> 提交信息的编写应当遵循 [Conventional Commits](https://www.conventionalcommits.org/) 和 [Angular Commit Message Guidelines](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)

</v-clicks>

---
---

# .gitignore 编辑技巧

<v-clicks at="1">

1. 支持 [glob](https://en.wikipedia.org/wiki/Glob_(programming))
    * `src/**/*.js` `src/*.??` `file-[01].js`
    * `src/**/*.{css,scss}` `file-{1..3}.js` `file-(1|2)`

</v-clicks>
<v-clicks at="2">

2. [A collection of .gitignore templates](https://github.com/github/gitignore)

</v-clicks>
<v-clicks at="3">

3. 忽略一个文件夹中的大部分内容，但是需要保留追踪其中的一些文件

```
.idea/*
!/.idea/codeStyles
```

</v-clicks>

---
layout: center
class: text-center
---

# 多分支操作

新建，切换，合并

---
clicks: 6
---

# 创建切换分支

<img
  v-click-hide
  v-motion-slide-visible-top
  class="py-4 w-3/5" 
  src="https://rogerdudler.github.io/git-guide/img/branches.png">

<div class="grid grid-cols-2 gap-x-4 gap-y-4" v-click-hide>

<v-after>

###### 执行的操作

###### 对应的命令

</v-after>

<v-clicks at="2">

- 创建一个分支并切换过去
- 切换回主干分支
- 删除指定分支
- 将分支推送到远端
- 列出所有分支

</v-clicks>

<v-clicks at="2">

- `git checkout -b <branch>`
- `git checkout main`
- `git branch -d <branch>`
- `git push origin <branch>`
- `git branch -a`

</v-clicks>

</div>

---
---

# Fast-forward 和 No-fast-foward（合并分支）

```
git merge <branch>
git merge –no-ff <branch>
```

如果合并的分支上有当前分支的全部 commit，则可以快速向前合并。

如果并非是快速向前，则会创建一个指向当前和合并分支的 commit。

<img v-motion-slide-visible-left v-click-hide class="h-56 mt-5 rounded" src="https://res.cloudinary.com/practicaldev/image/fetch/s--cT4TSe48--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/894znjv4oo9agqiz4dql.gif">

<img v-motion-slide-visible-left v-after class="h-56 mt-5 rounded" src="https://res.cloudinary.com/practicaldev/image/fetch/s--zRZ0x2Vc--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/rf1o2b6eduboqwkigg3w.gif">

---
---

# 处理冲突

```
git merge <branch>
vim <file>
git add <file>
git commit -a "<message>"
```

<img v-motion-slide-visible-left class="h-56 mt-5 rounded" src="https://res.cloudinary.com/practicaldev/image/fetch/s--7lBksXwA--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/bcd5ajtoc0g5dxzmpfbq.gif">

---
---

# Squash 和 Rebase（合并分支）

```
git merge –squash <branch>
git rebase <branch>
```

squash 和此前合并方式的不同之处在于，新的 commit 不会指向原分支。

rebase 会将待合并分支上的 commit 全部提交过来，如果存在冲突则以其为准，我们无需手动修改。
我们**不会经常使用 rebase**，它会修改项目的历史，因为被复制过来的 commit 有着新的 hash 值。

<img v-motion-slide-visible-left v-click-hide class="h-56 mt-5 rounded" src="https://yanhaijing.com/blog/500.gif">

<img v-motion-slide-visible-left v-after class="h-56 mt-5 rounded" src="https://res.cloudinary.com/practicaldev/image/fetch/s--EIY4OOcE--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/dwyukhq8yj2xliq4i50e.gif">

---
---

# Cherry-picking

```
git cherry-pick <commit-id>
```

<img v-motion-slide-visible-left class="h-56 mt-5 rounded" src="https://res.cloudinary.com/practicaldev/image/fetch/s--9vWP_K4S--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/2dkjx4yeaal10xyvj29v.gif">

---
layout: center
class: text-center
---

# Rebase and Reset

糟糕，我要修改此前的一些东西

---
---

# Rebase

在 rebase 分支之前，我们可以交互式的修改一些 commit。比如：

- reword: 修改 commit 信息
- squash: 融合该 commit 到此前的 commit
- drop: 移除该 commit

<img v-motion-slide-visible-left v-click class="h-56 mt-5 rounded" src="https://res.cloudinary.com/practicaldev/image/fetch/s--P6jr7igd--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/msofpv7k6rcmpaaefscm.gif">

---
---

# Reset

reset 会清空当前暂存区中的文件

```
git reset --soft HEAD~2
git reset --hard HEAD~2
```

Soft reset 只是移动头部指针到此前的 commit，而不会清除之后 commit 的内容。

Hard reset 会直接清空对应的 commit，好像它们从未出现过。

<img v-motion-slide-visible-left v-click-hide class="h-56 mt-5 rounded" src="https://res.cloudinary.com/practicaldev/image/fetch/s---GveiZe---/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/je5240aqa5uw9d8j3ibb.gif">

<img v-motion-slide-visible-left v-after class="h-56 mt-5 rounded" src="https://res.cloudinary.com/practicaldev/image/fetch/s--GqjwnYkF--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/hlh0kowt3hov1xhcku38.gif">

---
---

# Reverting

revert 会创建一个能够恢复此前 commit 内容的新 commit

```
git revert <commit-id>
```

<img v-motion-slide-visible-left class="h-56 mt-5 rounded" src="https://res.cloudinary.com/practicaldev/image/fetch/s--eckmvr2M--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/3kkd2ahn41zixs12xgpf.gif">

---
layout: center
class: text-center
---

# Git hooks

实现在 git push 时自动构建

---
---

# 设置 ssh key

把本机的 ssh 公钥拷贝到服务器中，实现免密登录

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@ip
```

---
---

# 初始化 bare 仓库（服务端）

bare 仓库就是没有实际内容的仓库，可以作为远端仓库来执行 push 操作

```bash
git init xxx.git --bare
```

创建一个 `post-receive` 文件，在我们 push 代码时即可自动执行该脚本。

```bash
cd xxx.git/hooks && vim post-receive
```

在脚本中，通过 `--git-dir` 和 `--work-tree` 参数可以拿到 push 来的最新代码。

---
---

# post-receive 脚本内容

```bash
#!/bin/bash
echo 'server: received code push...'
cd /opt/healthapp/watch-chart
echo 'server: checkout latest code from git ...'
git --git-dir=/opt/healthapp/watch-chart.git --work-tree=/opt/healthapp/watch-chart checkout main -f
echo 'server: remove previous container and image'
docker stop watch-chart && docker rm watch-chart
docker rmi vitesse:latest
echo 'server: running docker build'
docker buildx build . -t vitesse:latest
echo 'server: running vitesse'
docker run -d -p 8085:80 --name watch-chart vitesse:latest
echo 'server: done'
```

使脚本可以执行

```bash
chmod +x post-receive
```

---
---

# 添加设置好的远端仓库

```bash
git remote add prod ssh://user@ip/path-to-bare/xxx.git
```

推送代码，此时可以在终端看到服务端打印的日志。

```bash
git push prod main
```

---
---

# 其他 CI/CD 工具

- [Vercel](https://vercel.com/)
- [netlify](https://www.netlify.com/)
- [GitHub Actions](https://github.com/features/actions) ([一个🌰](https://github.com/hyoban/data-playback-compose/blob/master/.github/workflows/gradle.yml))
- [Jenkins](https://www.jenkins.io/)

---
---

# 参考和阅读更多

- [git - the simple guide](https://rogerdudler.github.io/git-guide/index.html)
- [CS Visualized: Useful Git Commands](https://dev.to/lydiahallie/cs-visualized-useful-git-commands-37p1)
- [Anthony's zshrc](https://github.com/antfu/dotfiles/blob/main/.zshrc)
- [常用 Git 命令清单](https://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)
- [Commit message 和 Change log 编写指南](https://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)
- [图解 4 种 git 合并分支方法](https://yanhaijing.com/git/2017/07/14/four-method-for-git-merge/)
- [Oh Shit, Git!?!](https://ohshitgit.com/)
- [【Git】部署流程｜持续部署到私有服务器](https://www.bilibili.com/video/BV1ck4y1B7Pw)

---
layout: center
class: 'text-center pb-5 :'
---

# 谢谢！

幻灯片可以在我的网站 [hyoban.cc](https://hyoban.cc) 上下载
