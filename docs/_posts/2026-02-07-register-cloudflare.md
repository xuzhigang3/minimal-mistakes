---
title: "零成本打造高速网站：手把手教你注册 Cloudflare 并开启 CDN 加速"
date: 2025-09-27 20:30:00 +0800
categories: ["Cloudflare", "建站"]
tags: ["注册", "CDN", "免费", "网站加速"]
description: "本篇教程详细演示如何免费注册 Cloudflare 账户、接入域名并开启 CDN 加速，让你的网站在几秒钟内飞起来。"
---

## 前言

在互联网时代，网站的访问速度与安全性直接影响用户体验和 SEO 排名。**Cloudflare** 作为全球领先的 CDN 与安全服务提供商，提供 **免费** 的加速、缓存、DDoS 防护以及 DNS 解析等功能，几乎是站长必备的“神器”。本篇文章将带你 **从零开始**，在 **5 分钟内** 完成 Cloudflare 账户注册、域名接入以及基础配置，让你的网站瞬间“飞起来”。

> **温馨提示**：本文面向 **完全零基础** 的同学，所有步骤均配有截图（文字版），只要跟着操作即可。

---

## 1️⃣ 注册 Cloudflare 账户

### 1.1 打开 Cloudflare 官网
在浏览器中访问 **https://www.cloudflare.com**，点击右上角的 **“Sign Up”**（注册）按钮。

### 1.2 填写基本信息
| 字段 | 示例 |
|------|------|
| 邮箱 | `your.email@example.com` |
| 密码 | `YourStrongP@ssw0rd` |
| 姓名（可选） | `张三` |

> **安全建议**：使用 **强密码**（大小写、数字、特殊字符）并开启 **两步验证（2FA）**。

### 1.3 验证邮箱
登录邮箱，打开 Cloudflare 发送的验证邮件，点击 **“Verify Email”** 完成验证。

### 1.4 完成注册
验证后，页面会跳转到 **Dashboard（仪表盘）**，此时你已经拥有了一个 Cloudflare 账户。

---

## 2️⃣ 接入域名（Add a Site）

### 2.1 点击 “Add a Site”
在 Dashboard 左侧导航栏找到 **“Add a Site”**，点击进入。

### 2.2 输入域名
在弹出的输入框中填入 **你的根域名**（例如 `example.com`），**不要** 包含 `www` 前缀。点击 **“Add Site”**。

### 2.3 选择免费计划
Cloudflare 会自动为你推荐 **Free Plan**，直接点击 **“Continue”** 即可。

### 2.4 DNS 扫描
Cloudflare 会自动扫描你当前 DNS 记录，列出所有已存在的记录。确认无误后，点击 **“Continue”**。

> **小技巧**：如果你的域名已经在其他 DNS 提供商（如阿里云、腾讯云）托管，扫描后仍会保留原有记录，后续可以统一在 Cloudflare 管理。

---

## 3️⃣ 修改域名 DNS 服务器（Name Server）

为了让 Cloudflare 完全接管你的 DNS，需要将域名的 **Name Server（NS）** 替换为 Cloudflare 提供的两条地址。

### 3.1 获取 Cloudflare NS
在 **“Overview”** 页面，你会看到类似下面的提示：

Name Server 1: nora.ns.cloudflare.com
Name Server 2: bob.ns.cloudflare.com


### 3.2 在域名注册商处修改 NS
登录你的域名注册商（如阿里云、GoDaddy、Namecheap），找到 **DNS / Name Server** 设置页面，将原来的 NS 替换为上一步的两条 Cloudflare NS。

> **注意**：修改 NS 后，**全球 DNS 生效时间** 通常为 **24‑48 小时**，但大多数情况下在 **10‑30 分钟** 内即可完成。

### 3.3 确认 NS 生效
回到 Cloudflare Dashboard，页面会显示 **“Pending”** 状态。稍等片刻后，状态会变为 **“Active”**，表示 NS 已成功切换。

---

## 4️⃣ 基础配置：开启 CDN 与安全防护

### 4.1 开启 “Proxy” 状态（橙色云朵）
在 **“DNS”** 页面，找到你域名的 **A 记录**（或 CNAME），点击右侧的 **“Proxy status”** 图标，使其变为 **橙色**（即 “Proxied”）。这意味着流量会先经过 Cloudflare 的全球网络，实现 **CDN 加速** 与 **DDoS 防护**。

### 4.2 开启常用安全功能
| 功能 | 位置 | 推荐状态 |
|------|------|----------|
| **SSL/TLS** | **SSL/TLS** → **Overview** | **Full (strict)**（全站加密） |
| **Always Use HTTPS** | **SSL/TLS** → **Edge Certificates** | **On**（自动跳转 HTTPS） |
| **Bot Fight Mode** | **Security** → **Settings** | **On**（防止恶意爬虫） |
| **Browser Integrity Check** | **Security** → **Settings** | **On**（提升安全性） |
| **Cache Level** | **Caching** → **Configuration** | **Standard**（默认缓存） |

> **提示**：如果你使用 **WordPress**，建议在 **“Speed”** → **“Optimization”** 中开启 **Auto Minify**（JS、CSS、HTML）和 **Brotli** 压缩，进一步提升页面加载速度。

### 4.3 页面规则（Page Rules）——可选
如果你有特殊需求（如强制 HTTPS、缓存特定路径），可以在 **“Rules”** → **“Page Rules”** 中创建规则。例如：

example.com/* → Cache Level: Cache Everything, Edge Cache TTL: a month

---

## 5️⃣ 常见问题（FAQ）

| 问题 | 解答 |
|------|------|
| **NS 切换后网站打不开怎么办？** | 检查 NS 是否已生效（可用 `dig example.com NS`），若仍未生效，请耐心等待或联系域名注册商。 |
| **开启 Proxy 后 DNS 记录失效？** | 确保记录类型为 **A**、**AAAA** 或 **CNAME**，且 **Proxy status** 为橙色。 |
| **SSL 证书显示 “Not secure”** | 在 **SSL/TLS** → **Overview** 中选择 **Full (strict)**，并确保源站（你的服务器）已部署有效证书。 |
| **Cloudflare 免费版有流量限制吗？** | 免费版每月提供 **10 GB** 的带宽，超出后仍可继续使用，只是会降速。 |
| **如何关闭 Cloudflare？** | 在 **Overview** 页面点击 **“Pause Cloudflare”**，即可将站点切回原始 DNS（灰色云朵）。 |

---

## 6️⃣ 小结

- **注册 Cloudflare** 只需邮箱 + 密码，过程不超过 5 分钟。  
- **接入域名** 并 **切换 NS** 后，Cloudflare 将接管 DNS，提供全球 CDN 加速。  
- **开启基础安全**（SSL、HTTPS、Bot Fight）即可大幅提升网站安全性和访问速度。  
- **免费版** 功能已足够个人博客或中小型企业使用，若后期有更高需求，可随时升级至 Pro / Business。

> **下一步**：如果你想让博客在搜索引擎中更快被收录，建议在 **Cloudflare** 中开启 **“Automatic HTTPS Rewrites”** 并配合 **Google Search Console** 提交站点地图。

---

## 📚 延伸阅读

- [Cloudflare 官方文档 – 入门指南](https://developers.cloudflare.com/fundamentals/get-started/)
- [使用 Cloudflare 加速 WordPress 站点](https://wordpress.org/plugins/cloudflare/)
- [如何通过 Cloudflare 实现全站 HTTPS](https://www.cloudflare.com/learning/ssl/what-is-https/)

---

> **祝你玩得开心，网站飞速如电！** 🚀  
> 如有任何疑问，欢迎在评论区留言，我会第一时间为你解答。

