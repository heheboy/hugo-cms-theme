# Hugo CMS Theme

<p align="center">
  <img src="images/screenshot.png" alt="Hugo CMS Theme 预览" width="800">
</p>

<p align="center">
  <a href="https://github.com/heheboy/hugo-cms-theme/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/heheboy/hugo-cms-theme?style=flat-square" alt="License">
  </a>
  <a href="https://github.com/heheboy/hugo-cms-theme/stargazers">
    <img src="https://img.shields.io/github/stars/heheboy/hugo-cms-theme?style=flat-square" alt="Stars">
  </a>
  <a href="https://heheboy.github.io/">
    <img src="https://img.shields.io/badge/demo-online-blue?style=flat-square" alt="Demo">
  </a>
</p>

<p align="center">
  一个为 Hugo CMS 优化的、简洁优雅的个人博客主题。
</p>

<p align="center">
  <a href="https://heheboy.github.io/">🚀 在线演示</a> |
  <a href="#-快速开始">📦 快速开始</a> |
  <a href="#-配置指南">⚙️ 配置指南</a>
</p>

---

## ✨ 功能特性

- 📱 **响应式设计** - 完美适配桌面端、平板和移动设备
- 🌓 **暗黑/亮色模式** - 自动切换或手动选择，保护眼睛
- 🔍 **站内搜索** - 基于 Fuse.js 的快速全文搜索
- 📊 **侧边栏** - 个人简介、分类、标签等可配置小工具
- 🏷️ **分类 & 标签** - 完整支持，自动生成分类页面
- 📅 **归档页面** - 按年份展示所有文章
- 🔗 **RSS & 网站地图** - SEO 友好，便于搜索引擎收录
- 📝 **代码高亮** - Dracula 主题，支持多种语言
- 📐 **数学公式** - 集成 KaTeX，支持 LaTeX 数学公式
- 🎨 **SEO 优化** - 内置 Open Graph、Twitter Cards 支持

---

## 🚀 快速开始

### 1. 安装主题

**方式一：Git Submodule（推荐）**

```bash
cd your-hugo-site
git init
git submodule add https://github.com/heheboy/hugo-cms-theme.git themes/hugo-cms-theme
```

**方式二：直接下载**

下载主题压缩包，解压到 `themes/hugo-cms-theme` 目录。

### 2. 配置主题

在 `hugo.toml` 中添加：

```toml
theme = 'hugo-cms-theme'
```

### 3. 启动预览

```bash
hugo server -D
```

访问 http://localhost:1313 查看效果。

---

## ⚙️ 配置指南

### 基础配置

```toml
baseurl = 'https://yourdomain.com'
languageCode = 'zh-CN'
title = '我的博客'
theme = 'hugo-cms-theme'
hasCJKLanguage = true

[pagination]
  pagerSize = 10

[params]
  # 站点描述
  description = '分享技术与生活'

  # 首页标语（显示在首页大图上）
  slogan = '记录思考，分享成长'

  # 首页背景图
  header_image = 'img/home-bg.jpg'

  # 作者信息
  author = '作者名'
  avatar = 'img/avatar.jpg'
  bio = '全栈开发者，热爱开源'

  # 侧边栏显示
  showSidebar = true

  # 默认暗黑模式
  darkMode = true

  # 分类/标签页面标题
  titleCategories = '文章分类'
  titleTags = '标签'
```

### 导航菜单

```toml
[menu]
  [[menu.main]]
    name = '首页'
    url = '/'
    weight = 10

  [[menu.main]]
    name = '内容文章'
    url = '/posts/'
    weight = 20

  [[menu.main]]
    name = '文章分类'
    url = '/categories/'
    weight = 30

  [[menu.main]]
    name = '归档册'
    url = '/archive/'
    weight = 40
```

### 侧边栏配置

侧边栏会自动显示以下内容（可在 `showSidebar` 中控制）：

- 作者信息（头像、简介、社交链接）
- 友情链接
- 分类列表

```toml
[params.social]
  github = 'https://github.com/yourusername'
  email = 'mailto:you@example.com'
```

### 友情链接

```toml
[[params.links]]
  name = 'Hugo 官方'
  url = 'https://gohugo.io'

[[params.links]]
  name = 'Hugo CMS'
  url = 'https://github.com/heheboy/hugo-cms-theme'
```

### 页脚信息

```toml
[params.footerInfo]
  [params.footerInfo.site]
    enabled = true
    text = 'Hugo CMS'
    url = 'https://github.com/heheboy/hugo-cms-theme'

  [params.footerInfo.theme]
    enabled = true
    text = 'hugo-cms-theme'
    url = 'https://github.com/heheboy/hugo-cms-theme'
    showStar = true
    githubUser = 'heheboy'
    githubRepo = 'hugo-cms-theme'
```

---

## 🗂️ 内容组织

### 目录结构

```
content/
├── _index.md              # 首页配置
├── about.md               # 关于页面
├── archive.md             # 归档页面
├── search.md              # 搜索页面
└── posts/                 # 文章目录
    ├── _index.md
    ├── post-1.md
    └── post-2.md
```

### 特殊页面 Front Matter

**关于页面** (`about.md`):

```yaml
---
title: "关于本站"
layout: "page"
---
```

**归档页面** (`archive.md`):

```yaml
---
title: "归档"
layout: "archive"
---
```

**搜索页面** (`search.md`):

```yaml
---
title: "搜索"
layout: "search"
---
```

### 文章 Front Matter

```yaml
---
title: "文章标题"
subtitle: "副标题（可选）"
date: 2024-01-15T10:00:00+08:00
draft: false
author: "作者名"
image: "img/post-bg.jpg"      # 文章头图（可选）
categories: ["技术", "编程"]   # 分类
tags: ["hugo", "博客"]         # 标签
---
```

---

## 🎨 自定义选项

### 自定义 CSS

在 `assets/css/custom.css` 中添加自定义样式：

```css
/* 自定义样式 */
```

### 自定义头部

在 `layouts/partials/head_custom.html` 中添加自定义头部内容：

```html
<!-- 自定义统计代码等 -->
```

---

## 🖼️ 截图

> **注意：** 截图占位符，请替换为实际截图。

### 首页

```
images/screenshot-home.png
```

### 文章页

```
images/screenshot-post.png
```

### 暗黑模式

```
images/screenshot-dark.png
```

---

## 📝 更新日志

### v1.0.0 (2024-XX-XX)

- ✨ 初始版本发布
- 📱 响应式布局支持
- 🌓 暗黑/亮色模式切换
- 🔍 站内搜索功能
- 📊 侧边栏小工具
- 🏷️ 分类和标签支持
- 📅 归档页面
- 🔗 RSS 订阅和网站地图

---

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建你的特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交你的修改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 打开一个 Pull Request

---

## 📄 许可证

本项目基于 [MIT](LICENSE) 许可证开源。

---

<p align="center">
  用 ❤️ 和 Hugo 构建
</p>
