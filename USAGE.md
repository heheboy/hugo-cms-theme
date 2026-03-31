# Hugo CMS Theme 使用指南

## 目录

- [快速开始](#快速开始)
- [完整配置参考](#完整配置参考)
- [文章写作指南](#文章写作指南)
- [功能特性说明](#功能特性说明)
  - [搜索功能](#搜索功能)
  - [Sitemap 站点地图](#sitemap-站点地图)
  - [分类与标签](#分类与标签)
  - [深色模式](#深色模式)
  - [侧边栏](#侧边栏)
  - [评论系统](#评论系统)
  - [页脚信息](#页脚信息)
  - [分页](#分页)
  - [归档页面](#归档页面)
- [文件结构](#文件结构)
- [自定义 CSS](#自定义-css)

---

## 快速开始

### 最小化配置

在站点根目录创建 `hugo.toml`：

```toml
baseURL = 'https://yourdomain.com'
languageCode = 'zh-CN'
title = '我的博客'

[params]
  author = "作者名"
  description = "站点描述"

[[params.menus]]
  name = "首页"
  url = "/"

[[params.menus]]
  name = "文章"
  url = "/posts/"

[[params.menus]]
  name = "归档"
  url = "/archive/"
```

### 创建第一篇文章

```bash
hugo new content posts/hello.md
```

在生成的文件中添加 frontmatter：

```markdown
---
title: "你好，世界"
date: 2026-03-30T10:00:00+08:00
draft: false
---

文章内容...
```

### 创建搜索页面（可选）

```bash
hugo new content search.md
```

修改生成的文件：

```markdown
---
title: "搜索"
layout: "page"
---
```

---

## 完整配置参考

### 站点级配置

| 配置项 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| `title` | string | 是 | 网站标题，显示在导航栏和页头 |
| `languageCode` | string | 是 | 语言代码，如 `zh-CN`、`en-US` |
| `params.author` | string | 否 | 作者名称，显示在侧边栏和页脚 |
| `params.description` | string | 否 | 站点描述，用于 SEO meta 标签 |
| `params.slogan` | string | 否 | 站点副标题，显示在首页大图上 |
| `params.summaryLength` | int | 否 | 摘要长度，默认 150 字符 |

### 头部背景图配置

支持为不同页面类型设置不同的背景图：

```toml
[params.headerImages]
  home = "img/home-bg.jpg"      # 首页
  post = "img/post-bg.jpg"      # 文章详情页
  list = "img/list-bg.jpg"      # 列表页（文章列表、分类、标签）
  archive = "img/archive-bg.jpg" # 归档页
  page = "img/page-bg.jpg"      # 单页面（关于、搜索等）
  default = "img/default-bg.jpg" # 默认背景图
```

如果不配置特定页面的背景图，会按以下优先级使用：`特定页面 > default > 内置默认`

### 功能开关

| 配置项 | 类型 | 默认值 | 说明 |
|--------|------|--------|------|
| `params.showSidebar` | bool | false | 是否显示侧边栏 |
| `params.showCategories` | bool | false | 是否在侧边栏显示分类列表 |
| `params.showTags` | bool | false | 是否在侧边栏显示标签云 |
| `params.darkMode` | bool | false | 是否启用深色模式切换按钮 |

### 输出格式配置（搜索功能必需）

启用搜索功能需要在配置中添加 JSON 输出格式：

```toml
[outputs]
  home = ['HTML', 'RSS', 'JSON']
```

这会为首页生成 `index.json` 文件，作为搜索的数据源。

### 导航菜单配置

```toml
[[params.menus]]
  name = "首页"
  url = "/"

[[params.menus]]
  name = "文章"
  url = "/posts/"

[[params.menus]]
  name = "关于"
  url = "/about/"
```

### 侧边栏作者信息

```toml
[params]
  avatar = "img/avatar.jpg"      # 头像图片路径
  bio = "这是我的个人简介"       # 个人简介
```

### 社交链接

```toml
[params.social]
  github = "https://github.com/username"
  email = "mailto:email@example.com"
  twitter = "https://twitter.com/username"
  linkedin = "https://linkedin.com/in/username"
```

### 评论系统（Giscus）

```toml
[params.comments]
  enabled = true
  provider = "giscus"
  [params.comments.giscus]
    repo = "username/repo"
    repoId = "xxx"              # 从 Giscus 网站获取
    category = "Announcements"
    categoryId = "xxx"          # 从 Giscus 网站获取
```

### Sitemap 站点地图

```toml
[sitemap]
  changefreq = 'monthly'
  filename = 'sitemap.xml'
  priority = 0.5
```

配置项说明：
- `changefreq`: 更新频率（always, hourly, daily, weekly, monthly, yearly, never）
- `filename`: Sitemap 文件名
- `priority`: 页面优先级（0.0-1.0）

### 404 页面

```toml
[params]
  title_404 = "抱歉，您访问的页面不存在。"
```

### 页脚信息

在页脚显示网站制作信息和主题信息：

```toml
[params.footerInfo]
  # 网站制作信息
  [params.footerInfo.site]
    enabled = true
    text = "本网站由 Hugo 驱动"
    url = "https://gohugo.io/"

  # 主题信息
  [params.footerInfo.theme]
    enabled = true
    text = "主题采用 hugo-cms-theme"
    url = "https://github.com/yourusername/hugo-cms-theme"
    showStar = true           # 显示 GitHub Star 按钮
    githubUser = "yourusername"
    githubRepo = "hugo-cms-theme"
```

显示效果：

```
© 2026 作者名. All rights reserved.
本网站由 Hugo 驱动 | 主题采用 hugo-cms-theme ⭐
```

---

## 文章写作指南

### Frontmatter 完整示例

```markdown
---
title: "文章标题"                    # 必填：文章标题
subtitle: "副标题"                   # 可选：副标题，显示在标题下方
date: 2026-03-30T10:00:00+08:00      # 必填：发布日期
lastmod: 2026-03-31T10:00:00+08:00   # 可选：最后修改日期
author: "作者名"                     # 可选：文章作者（覆盖站点默认值）
description: "文章描述"              # 可选：用于 SEO 和分享卡片
image: "img/cover.jpg"               # 可选：封面图，用于详情页和分享卡片
categories:                          # 可选：分类列表
  - "技术"
  - "教程"
tags:                                # 可选：标签列表
  - "hugo"
  - "博客"
  - "前端"
draft: false                         # 可选：是否为草稿
layout: ""                           # 可选：特殊布局（如设置为 "page" 会隐藏侧边栏）
---

正文内容...
```

### 摘要控制

主题支持三种方式控制文章摘要：

#### 方式一：自动摘要（默认）

Hugo 自动截取文章前 70 个单词作为摘要。

#### 方式二：手动截取

在文章中插入 `<!--more-->` 分隔符：

```markdown
这是摘要内容，会显示在列表页...

<!--more-->

这是正文内容，只在详情页显示...
```

#### 方式三：Frontmatter 摘要

```markdown
---
summary: "这是自定义摘要内容"
---
```

### 图片使用

#### 文章内图片

```markdown
![图片描述](img/example.jpg)
```

或使用 Hugo 的 figure 短代码：

```markdown
{{< figure src="img/example.jpg" title="图片标题" >}}
```

#### 封面图

在 frontmatter 中设置：

```markdown
---
image: "img/cover.jpg"
---
```

封面图会用于：
- 文章详情页头部大图
- SEO Open Graph 分享卡片
- Twitter Card

---

## 功能特性说明

### 搜索功能

主题内置基于 Fuse.js 的客户端搜索功能，无需额外配置。

#### 启用搜索

1. 确保输出格式包含 JSON（用于生成搜索索引）：

```toml
[outputs]
  home = ['HTML', 'RSS', 'JSON']
```

2. 创建搜索页面 `content/search.md`：

```markdown
---
title: "搜索"
layout: "page"
---
```

3. 重新构建站点后，导航栏会出现搜索图标，点击可进入搜索页面。

#### 搜索功能特点

- 支持实时模糊搜索，无需回车
- 搜索范围：文章标题、内容、摘要、标签
- 结果高亮显示匹配关键词
- 支持通过 URL 参数直接搜索，如 `https://yourdomain.com/search/?q=关键词`

#### 搜索权重配置

搜索结果的排序权重（不可配置，内置）：
- 标题：权重 0.4（最高）
- 内容：权重 0.3
- 摘要：权重 0.2
- 标签：权重 0.1（最低）

---

### Sitemap 站点地图

Hugo 内置生成 Sitemap 功能。

#### 启用 Sitemap

在 `hugo.toml` 中添加：

```toml
[sitemap]
  changefreq = 'monthly'
  filename = 'sitemap.xml'
  priority = 0.5
```

构建后会自动生成 `sitemap.xml`，可通过 `https://yourdomain.com/sitemap.xml` 访问。

#### 配置项说明

| 配置项 | 默认值 | 说明 |
|--------|--------|------|
| `changefreq` | monthly | 页面更新频率，可选值：always, hourly, daily, weekly, monthly, yearly, never |
| `filename` | sitemap.xml | Sitemap 文件名 |
| `priority` | 0.5 | 页面优先级，范围 0.0-1.0 |

---

### 分类与标签

主题内置完整的分类（categories）和标签（tags）功能。

#### 配置

确保 `hugo.toml` 中启用了分类和标签：

```toml
[taxonomies]
  category = 'categories'
  tag = 'tags'
```

#### 在文章中添加分类和标签

```markdown
---
title: "文章标题"
categories:
  - "技术"
  - "教程"
tags:
  - "hugo"
  - "博客"
---
```

#### 分类列表页

访问 `/categories/` 查看所有分类，每个分类显示包含的文章数量。

#### 分类文章列表页

点击任意分类（如 `/categories/技术/`），会显示该分类下的所有文章，效果与首页一致。

#### 标签功能

标签功能与分类完全相同：
- `/tags/` - 所有标签列表
- `/tags/标签名/` - 该标签下的文章列表

#### 侧边栏分类/标签云

启用侧边栏分类云：

```toml
[params]
  showSidebar = true
  showCategories = true  # 显示分类云
  showTags = true        # 显示标签云
```

---

### 深色模式

在配置中启用：

```toml
[params]
  darkMode = true
```

启用后，导航栏会显示主题切换按钮。用户的主题偏好会自动保存在浏览器本地存储中。

### 侧边栏

启用侧边栏：

```toml
[params]
  showSidebar = true
  showCategories = true  # 显示分类云
  showTags = true        # 显示标签云
```

侧边栏包含：
- 作者信息区（头像、名称、简介、社交链接）
- 分类云（当 `showCategories = true` 时显示）
- 标签云（当 `showTags = true` 时显示）

注意：404 页面不会显示侧边栏。

### 评论系统

目前支持 Giscus 评论系统（基于 GitHub Discussions）：

1. 确保仓库已启用 Discussions
2. 访问 https://giscus.app 获取配置参数
3. 在 hugo.toml 中填写配置

### 页脚信息

在页脚显示网站制作信息和主题信息：

```toml
[params.footerInfo]
  [params.footerInfo.site]
    enabled = true
    text = "本网站由 Hugo 驱动"
    url = "https://gohugo.io/"

  [params.footerInfo.theme]
    enabled = true
    text = "主题采用 hugo-cms-theme"
    url = "https://github.com/yourusername/hugo-cms-theme"
    showStar = true
    githubUser = "yourusername"
    githubRepo = "hugo-cms-theme"
```

显示效果：
- 版权声明下方显示网站制作信息和主题信息
- 如果配置 `showStar = true`，会显示 GitHub Star 按钮

### 分页

首页和列表页自动启用分页，每页显示文章数由 Hugo 配置控制：

```toml
[pagination]
  pagerSize = 10  # 每页显示 10 篇文章
```

### 归档页面

创建 `content/archive.md`：

```markdown
---
title: "归档"
layout: "page"
---
```

主题会自动生成按年份分组的文章归档。

---

## 文件结构

```
hugo-cms-theme/
├── assets/
│   └── css/                    # SCSS 样式文件
│       ├── main.scss           # 主样式入口
│       ├── _layout.scss        # 布局相关
│       ├── _post.scss          # 文章相关样式
│       ├── _nav.scss           # 导航栏样式
│       ├── _sidebar.scss       # 侧边栏样式
│       ├── _header.scss        # 页头样式
│       ├── _footer.scss        # 页脚样式
│       ├── _pagination.scss    # 分页样式
│       ├── _archive.scss       # 归档页样式
│       └── _responsive.scss    # 响应式样式
├── layouts/
│   ├── _partials/              # 模板片段
│   │   ├── head.html           # HTML 头部
│   │   ├── nav.html            # 导航栏
│   │   ├── header.html         # 页头（大图区域）
│   │   ├── footer.html         # 页脚
│   │   ├── sidebar.html        # 侧边栏
│   │   ├── pagination.html     # 分页组件
│   │   ├── seo.html            # SEO meta 标签
│   │   ├── comments.html       # 评论系统
│   │   ├── scripts.html        # JS 脚本
│   │   └── social.html         # 社交链接图标
│   ├── _markup/
│   │   └── render-image.html   # 图片渲染钩子
│   ├── baseof.html             # 基础模板
│   ├── index.html              # 首页模板
│   ├── single.html             # 文章详情页
│   ├── list.html               # 列表页（分类/标签）
│   ├── page.html               # 单页面
│   ├── archive.html            # 归档页
│   └── 404.html                # 404 页面
├── static/                     # 静态文件
│   └── img/                    # 图片目录
└── theme.toml                  # 主题元信息
```

---

## 自定义 CSS

### 方法一：覆盖 CSS 变量

在站点根目录创建 `assets/css/custom.scss`：

```scss
:root {
  // 主色调
  --color-primary: #0066cc;
  --color-primary-hover: #0055aa;

  // 背景色
  --color-bg: #ffffff;
  --color-bg-secondary: #f5f5f5;

  // 文字颜色
  --color-text: #333333;
  --color-text-secondary: #666666;

  // 边框颜色
  --color-border: #e0e0e0;
}

// 深色模式变量
[data-theme="dark"] {
  --color-bg: #1a1a1a;
  --color-bg-secondary: #2a2a2a;
  --color-text: #e0e0e0;
  --color-text-secondary: #a0a0a0;
  --color-border: #444444;
}
```

### 方法二：添加自定义样式

```scss
// 自定义样式示例
.post-item-simple {
  // 修改文章列表项样式
  padding: 2rem 0;
}

.post-title {
  // 修改标题样式
  font-size: 1.8rem;
}

// 隐藏阅读更多按钮
.read-more {
  display: none;
}
```

### 可用的 CSS 变量列表

| 变量名 | 说明 | 默认值 |
|--------|------|--------|
| `--color-primary` | 主题色 | `#2563eb` |
| `--color-primary-hover` | 主题色悬停 | `#1d4ed8` |
| `--color-bg` | 背景色 | `#ffffff` |
| `--color-bg-secondary` | 次要背景色 | `#f8fafc` |
| `--color-text` | 主文字色 | `#1f2937` |
| `--color-text-secondary` | 次要文字色 | `#6b7280` |
| `--color-border` | 边框色 | `#e5e7eb` |
| `--font-family-base` | 基础字体 | system-ui 等 |
| `--font-family-mono` | 等宽字体 | monospace |
| `--container-max-width` | 容器最大宽度 | `1200px` |
| `--sidebar-width` | 侧边栏宽度 | `280px` |
| `--spacing-xs` | 超小间距 | `0.25rem` |
| `--spacing-sm` | 小间距 | `0.5rem` |
| `--spacing-md` | 中间距 | `1rem` |
| `--spacing-lg` | 大间距 | `1.5rem` |
| `--spacing-xl` | 超大间距 | `2rem` |
| `--spacing-xxl` | 最大间距 | `3rem` |
| `--radius-sm` | 小圆角 | `4px` |
| `--radius-md` | 中圆角 | `8px` |
| `--shadow-sm` | 小阴影 | `0 1px 2px rgba(0,0,0,0.05)` |
| `--shadow-md` | 中阴影 | `0 4px 6px rgba(0,0,0,0.1)` |

### 修改模板中的 SCSS 文件

如果需要深度定制，可以直接修改主题内的 SCSS 文件：

- `_layout.scss` - 修改整体布局
- `_post.scss` - 修改文章列表和详情页样式
- `_nav.scss` - 修改导航栏样式
- `_header.scss` - 修改页头大图区域
- `_sidebar.scss` - 修改侧边栏样式

修改后 Hugo 会自动重新编译样式。

---

## 常见问题

### Q: 首页文章列表不显示摘要？

A: 确保文章正文有足够内容，或使用 `<!--more-->` 手动设置摘要截止位置。

### Q: 如何隐藏特定页面的侧边栏？

A: 在该页面的 frontmatter 中设置 `layout: "page"`。

### Q: 评论系统不显示？

A: 检查：
1. `params.comments.enabled` 是否为 `true`
2. Giscus 配置参数是否正确
3. 仓库是否已启用 Discussions
4. 网站是否部署在公网（本地测试无法加载 Giscus）

### Q: 搜索功能不工作？

A: 检查：
1. 是否在 `hugo.toml` 中配置了 `[outputs]` 包含 `'JSON'`
2. 是否创建了 `content/search.md` 页面
3. 构建后站点根目录是否有 `index.json` 文件
4. 网络是否能访问 Fuse.js CDN (cdn.jsdelivr.net)

### Q: 搜索结果不准确？

A: 搜索使用模糊匹配算法，尝试使用更精确的关键词。搜索范围包括标题、内容、摘要和标签，其中标题权重最高。

### Q: Sitemap 未生成？

A: 检查：
1. `hugo.toml` 中是否配置了 `[sitemap]` 区块
2. 是否设置了 `disableSitemap = false`（或删除此行）
3. 构建后查看 `public/sitemap.xml` 是否存在

### Q: 如何修改首页头部背景图？

A: 在 `hugo.toml` 中设置：

```toml
[params.headerImages]
  home = "img/your-image.jpg"
```

图片路径相对于 `static` 目录。

### Q: 如何为不同页面设置不同的背景图？

A: 使用 `headerImages` 配置块：

```toml
[params.headerImages]
  home = "img/home-bg.jpg"      # 首页
  post = "img/post-bg.jpg"      # 文章详情页
  list = "img/list-bg.jpg"      # 列表页
  archive = "img/archive-bg.jpg" # 归档页
  page = "img/page-bg.jpg"      # 单页面
  default = "img/default-bg.jpg" # 默认背景图
```

如果不配置特定页面的背景图，会使用 `default` 配置或内置默认图片。

---

*最后更新：2026-03-30*
