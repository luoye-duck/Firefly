---
title: 一键解决Cloudflare Pages文件过大无法上传的问题，直接上传Github小白教程！超详细！
published: 2026-07-05
pinned: false
description: Cloudflare文件过大？试试上传Github连接到Cloudflare Worker!
tags: [Cloudflare, GitHub, 建站]
category: 建站干货
draft: false
---

Cloudflare文件过大？试试上传Github连接到Cloudflare Worker!

> 本教程将手把手教你解决 Cloudflare Pages 直接上传文件时遇到的文件过大问题，通过 GitHub 仓库中转，轻松搞定部署！

## 问题背景

很多小白在使用 Cloudflare Pages 部署网站时，可能会遇到这样的报错：

> **Error: File size exceeds the limit**（文件大小超出限制）

Cloudflare Pages 直接上传方式对单文件大小和总项目体积都有限制。当你的网站包含很多文件，就很容易触发这个限制。

**解决方案：** 把文件先上传到 GitHub 仓库，然后让 Cloudflare 连接你的 GitHub 仓库进行自动构建部署，就能完美绕过文件大小限制！

---

## 第一步：注册一个 GitHub 账号

如果你还没有 GitHub 账号，先去注册一个。

🔗 链接直达：[ GitHub 官网直达](https://github.com/signup)

1. 打开 GitHub 官网，点击 **Sign up**
2. 输入你的邮箱、设置密码和用户名
3. 完成邮箱验证（去邮箱点确认链接）
4. 选择免费计划（Free）即可

---

## 第二步：创建 GitHub 仓库

注册好账号后，我们要创建一个仓库来放文件。

1. 登录 GitHub，点击右上角 **+** 号，选择 **New repository**

2. 填写仓库信息：
   - **Repository name**（仓库名称）：输入一个你喜欢的名字，比如 `my-website`
   - **Description**（描述）：可选，简单写一下说明
   - **Public / Private**：选择 **Public**（公开），这样 Cloudflare 才能访问
   - **Add a README file**：建议勾选

3. 点击 **Create repository** 创建完成

---

## 第三步：上传网站文件到 GitHub

把你的网站所有文件都上传到仓库里（有手就会）

### 方式一：网页直接上传（推荐小白用）

1. 进入你刚创建的仓库页面
2. 点击 **Add file** → **Upload files**
3. 将你网站的所有文件**拖拽**到上传区域
   - ⚠️ **注意：** 如果网站主页面是 HTML 文件，请提前命名为 `index.html`
   - 建议先在本地把文件整理好，确保能正确运行！
4. 在下方填写提交信息（Commit changes），随便写个说明，比如 "网站文件"
5. 点击 **Commit changes** 提交

### 方式二：使用 Git 命令行上传（大佬可用）

首先到Git官网下载软件🔗 链接直达：[Git软件官网直达](https://git-scm.cn/install/windows)

然后使用依以下命令

```bash
# 克隆仓库到本地
git clone https://github.com/你的用户名/my-website.git

# 进入仓库目录
cd my-website

# 把你的网站文件复制到这个目录

# 添加所有文件
git add .

# 提交
git commit -m "上传网站文件"

# 推送到 GitHub
git push origin main
```

> 💡 **小提示：** 如果是第一次使用 Git，需要先配置用户名和邮箱：
> ```bash
> git config --global user.name "你的名字"
> git config --global user.email "你的邮箱"
> ```

---

## 第四步：在 Cloudflare 创建项目并连接 GitHub

文件上传到 GitHub 后，接下来让 Cloudflare 连接你的仓库。

1. 登录 Cloudflare Dashboard
   🔗 链接直达：[前往 Cloudflare Dashboard](https://dash.cloudflare.com/)

2. 左侧菜单找到 **Workers & Pages**，点击 **Create**（创建）

3. 选择 **Pages** 标签页，然后点击 **Connect to Git**（连接 Git）

4. 首次使用会弹出授权页面，点击 **Connect GitHub**，授权 Cloudflare 访问你的 GitHub 仓库
   - 可以选择授权所有仓库，或只授权特定仓库

5. 授权完成后，选择你刚创建的仓库 `my-website`

---

## 第五步：配置构建设置

连接仓库后，需要配置一些构建参数。

| 配置项 | 填写内容 |
|---|---|
| **Project name** | 随意，比如 `my-website` |
| **Production branch** | `main`（或你的默认分支名） |
| **Framework preset** | 如果是纯静态网站选 `None`；如果用了框架（如 Astro、Hugo 等）选择对应框架 |
| **Build command** | 纯静态网站留空；用了框架则填构建命令（如 `npm run build`） |
| **Build output directory** | 纯静态网站填 `.`（当前目录）；框架则填输出目录（如 `dist`、`public` 等） |

> ⚠️ **重点提醒：**
> - 如果你的网站是**纯 HTML/CSS/JS** 文件，**Build command 留空**，**Build output directory 填 `.`**
> - 如果用了 **Astro** 框架，Build command 填 `npm run build`，输出目录填 `dist`
> - 如果用了 **Hugo**，Build command 填 `hugo`，输出目录填 `public`

点击 **Save and Deploy**（保存并部署）！

---

## 第六步：等待部署完成

点击部署后，Cloudflare 会自动从你的 GitHub 仓库拉取文件并进行构建。

1. 你会看到部署进度页面，通常 **1-5 分钟** 就能完成
2. 状态显示 **Success**（成功）就大功告成了！
3. Cloudflare 会给你分配一个 `xxx.pages.dev` 的域名，点击即可访问你的网站

> 🎉 恭喜！你的网站已经成功部署了！

---

## 进阶：绑定自定义域名

如果你有自己的域名，可以绑定到 Cloudflare Pages：

1. 进入项目页面，点击 **Custom domains** 标签
2. 点击 **Set up a custom domain**
3. 输入你的域名，按照提示完成 DNS 配置
4. 等待 DNS 生效（通常几分钟到几小时），即可通过自定义域名访问

---

## 自动更新：以后改了文件怎么办？

这是连接 GitHub 的最大好处 —— **自动部署**！

以后你只需要：
1. 修改 GitHub 仓库里的文件（可以网页直接编辑，也可以本地上传）
2. 每次提交（Commit）后，Cloudflare 会**自动检测到更新**
3. 自动重新构建部署，无需手动操作

> 💡 **简单说：改了 GitHub 仓库 → Cloudflare 自动更新网站，全程自动化！**

---

## 常见问题排查

### Q1：部署失败怎么办？

检查以下几点：
- Build command 和 output directory 是否填写正确
- 查看 Cloudflare 的构建日志（Build logs），找到报错信息
- 确保仓库里的文件结构正确，`index.html` 在正确的目录下

### Q2：网站打开是空白页？

- 检查 `index.html` 是否在构建输出目录的根目录
- 检查 HTML 中的文件路径是否正确（相对路径 vs 绝对路径）
- 打开浏览器开发者工具（F12），查看 Console 是否有报错

### Q3：GitHub 单文件大小也有限制吗？

GitHub 免费版单个文件限制 **100MB**，仓库总大小建议不超过 **1GB**。如果你的文件（如视频）超过 100MB，建议：
- 使用 Git LFS（Large File Storage）
- 或者把大文件放到其他存储服务（如 Cloudflare R2、对象存储），在网站中通过链接引用

### Q4：仓库设为 Private 可以吗？

可以，但 Cloudflare 连接 Private 仓库需要你的 GitHub 账号有相应的权限授权。免费版 Cloudflare Pages 支持连接 Private 仓库。

---
