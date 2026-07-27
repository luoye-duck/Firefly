---
title: 小白教程！0成本免费申请域名！可托管CF！
published: 2026-07-27
pinned: false
description: 0成本白嫖永久免费域名，支持托管到Cloudflare，小白也能轻松搞定！
tags: [域名, Cloudflare, 免费域名, 建站]
category: 建站干货
draft: false
---

想搭建自己的网站但不想花钱买域名？本教程手把手教你 **0 成本白嫖免费域名！可续期**，可托管 CF 享受免费 CDN 加速！

> 无论你是建站新手还是薅羊毛老手，跟着步骤走，几分钟就能拥有自己的专属域名！

---

## 📋 免费域名平台一览

目前主流的免费域名平台对比如下：

| 平台 | 域名后缀 | 审核方式 | 费用 | Cloudflare托管 | 推荐指数 |
|------|----------|----------|------|----------------|----------|
| **DNSHE** | `.cc.cd` / `.bot.cd` 等等| 免审核，支持自定DNS（要先到官方的Github仓库点Star和绑定TOTP） | 完全免费 | ✅ 小型个人网站首选 | ⭐⭐⭐⭐⭐ |
| **GNAME** | `.eu.cc` | 免审核，支持自定DNS（要先进行手机号和邮箱验证）| ✅ 支持自定义NS | ⭐⭐⭐⭐ |
> 💡 **推荐首选 DNSHE**：多种后缀可选，可做任务领注册额度！

---

## 方案一：DNSHE


> ⚠️ 选择 `.cc.cd` 后缀注册托管CF成功率更高！

### 第一步：注册账号并做任务申请域名

1. 访问 DNSHE 官网：🔗 [DNSHE直达](https://dnshe.com)
2. 点击 **Sign UP** 注册新账号
3. 完成任务免费注册域名：前往**免费域名**>**奖励中心**
   - 根据提示前往他们的Github仓库为他们点上Star，在此之前你需要注册一个Github账号🔗 [Github直达](https://github.com)
   - 完成之后继续根据提示去绑定并启用 TOTP 安全登录后就可以注册免费的域名了！


### 第二步：托管到 Cloudflare

将域名的 DNS 管理权交给 Cloudflare，享受免费的 CDN 加速和 DNS 解析服务。

1. **在 Cloudflare 添加域名**
   - 登录或注册 Cloudflare账号：🔗 [CF直达](https://dash.cloudflare.com/)
   - 点击 **网域**>**添加网域**
   - 输入你刚申请的域名（如 `yijiansanlian.cc.cd`）
   - 选择 **Free** 免费套餐

2. **获取 Cloudflare 的 NS 地址**
   - Cloudflare 会分配两个 NS 服务器地址，类似：
     ```
     xxx.xx.cloudflare.com
     xxxx.xxx.cloudflare.com
     ```

3. **把DNSHE的DNS替换为CF的DNS**
   - 来到 DNSHE 域名的管理页，选择**DNS服务器**>**修改DNS服务器**然后把里面的两个DNS服务器替换为CF的DNS服务器即可

4. **等待生效**
   - 完成后稍等片刻，Cloudflare 会发送邮件通知域名已成功接入
   - 之后就可以在 Cloudflare 中运用此域名了！

---

## 方案二：GNAME 免费域名


### 第一步：注册账号

1. 访问 GNAME 官网：🔗 [GNAME直达](https://gname.com)
2. 填写 **邮箱** 和 **密码**
3. 把发送到邮箱的验证码复制到刚刚的注册页面（点击邮箱中GNAME的邮件复制）

### 第二步：搜索并注册域名

1. 来到**域名注册**>**免费注册**
2. 搜索想要的域名格式：例如`xxxx.eu.cc`（一定要选择后缀为“.eu.cc”的免费注册）
3. 点击 **立即注册** 到达结算页面
4. 系统会自动填充赠送的3张eu.cc免费注册卡
5. 添加手机号验证账号：（这样才能改DNS）
   - **手机号码**：必须真实可用（平台要发送验证码）
   - **邮箱**：注册时已验证，所以不需要二次验证

### 第三步：托管到 Cloudflare

1. 来到后台，点击左侧 **我的域名**
2. 点击**管理**>**域名DNS**修改DNS（DNS按上文所说获取）
3. 等待生效后即可在 Cloudflare 中管理 DNS


> 🎉 有了免费域名 + Cloudflare 托管，再配合免费部署平台（如 Cloudflare Pages、GitHub Pages），你就可以 **0 成本** 搭建一个完整的个人网站了！

**相关教程推荐：**
- [使用 Cloudflare 免费部署网站，小白也能轻松建站](/posts/cloudflare-deploy/)
- [一键解决 Cloudflare Pages 文件过大无法上传的问题](/posts/cloudflare-pages-github-upload/)
