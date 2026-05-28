# Code Wiki - Jekyll Blog Project

## 项目概述

这是一个基于 **Jekyll** 的静态博客网站项目，使用 GitHub Pages 进行托管部署。项目采用简洁的博客架构，支持 Markdown 文章编写和自动化站点生成。

**技术栈**: Jekyll (Ruby) | HTML | Liquid 模板引擎

---

## 1. 项目架构

```
/workspace/
├── _config.yml          # Jekyll 全局配置文件
├── index.html           # 网站首页（文章列表）
├── _layouts/            # HTML 模板布局目录
│   └── default.html     # 默认页面布局
├── _posts/              # 博客文章目录（Markdown/HTML）
│   └── 2012-08-25-hello-world.html  # 示例文章
├── _site/               # Jekyll 生成的静态站点输出目录
│   ├── index.html       # 生成的首页
│   └── 2012/08/25/      # 生成的文章页面
│       └── hello-world.html
└── .git/                # Git 版本控制目录
```

---

## 2. 核心模块说明

### 2.1 配置文件

**文件**: `_config.yml`

| 配置项 | 说明 | 值 |
|--------|------|-----|
| `baseurl` | 网站基础路径 | `/` |

**用途**: 定义 Jekyll 站点的全局配置参数。

```yaml
baseurl: /
```

### 2.2 页面模板

**文件**: `_layouts/default.html`

**职责**: 定义页面的 HTML 骨架结构，所有页面继承此布局。

**包含元素**:
- HTML5 文档声明
- 字符编码设置（UTF-8）
- 页面标题（使用 Liquid 变量 `{{ page.title }}`）
- 内容输出区域（`{{ content }}`）

### 2.3 首页逻辑

**文件**: `index.html`

**职责**: 展示博客文章列表。

**核心逻辑**:
- 使用 `site.posts` 遍历所有文章
- 显示文章发布日期（`date_to_string` 过滤器格式化）
- 生成文章链接

```liquid
{% for post in site.posts %}
  <li>{{ post.date | date_to_string }} <a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
```

### 2.4 文章存储

**目录**: `_posts/`

**命名规范**: `YYYY-MM-DD-文章标题.扩展名`

**示例**: `2012-08-25-hello-world.html`

**Front Matter 必需字段**:
- `layout`: 使用的布局模板
- `title`: 文章标题

---

## 3. 关键文件清单

| 文件路径 | 类型 | 说明 |
|----------|------|------|
| `_config.yml` | 配置文件 | Jekyll 全局配置 |
| `index.html` | 页面 | 网站首页/文章列表 |
| `_layouts/default.html` | 模板 | 页面布局模板 |
| `_posts/2012-08-25-hello-world.html` | 文章 | 示例博客文章 |
| `_site/` | 目录 | 生成的静态站点（不需手动编辑） |

---

## 4. 依赖关系

### 4.1 技术依赖

```
Jekyll (Ruby Gem)
├── Liquid (模板引擎)
├── Kramdown (Markdown 处理器)
└── Sass (可选样式预处理)
```

### 4.2 文件依赖链

```
文章源文件 (_posts/*.html)
    ↓
布局模板 (_layouts/default.html)
    ↓
Jekyll 引擎处理
    ↓
静态站点输出 (_site/)
```

**Front Matter 引用关系**:
- 文章指定 `layout: default`
- 布局模板通过 `{{ content }}` 嵌入文章内容
- 首页通过 `site.posts` 聚合所有文章

---

## 5. 运行环境

### 5.1 环境要求

| 组件 | 最低版本 | 说明 |
|------|----------|------|
| Ruby | 2.5.0+ | Jekyll 运行基础 |
| RubyGems | 最新版 | 包管理工具 |
| Git | 任意版本 | 版本控制 |

### 5.2 安装步骤

```bash
# 1. 安装 Jekyll 和 Bundler
gem install jekyll bundler

# 2. 进入项目目录
cd /workspace

# 3. 本地预览
jekyll serve --watch

# 4. 访问 http://localhost:4000
```

### 5.3 构建命令

| 命令 | 用途 |
|------|------|
| `jekyll build` | 生成静态站点到 `_site/` |
| `jekyll serve` | 本地开发服务器（热重载） |
| `jekyll new [name]` | 创建新 Jekyll 项目 |

---

## 6. 部署说明

### 6.1 GitHub Pages 部署

该项目已配置为 GitHub Pages 站点：

- **分支**: `gh-pages`
- **部署方式**: 将 `_site/` 目录内容推送到 `gh-pages` 分支
- **访问方式**: `https://用户名.github.io/仓库名/`

### 6.2 CNAME 配置

文件: `_site/CNAME`（如有自定义域名需求）

---

## 7. Jekyll 工作流程

```
1. 书写文章
   └─ 创建 _posts/YYYY-MM-DD-title.md

2. 定义布局
   └─ 在 Front Matter 指定 layout

3. 本地预览
   └─ jekyll serve --watch

4. 提交推送
   └─ git push origin gh-pages

5. GitHub 自动构建
   └─ GitHub Pages 自动部署
```

---

## 8. Front Matter 规范

Jekyll 文章必须在文件开头使用 YAML Front Matter：

```yaml
---
layout: default          # 必填：使用的布局模板
title: 文章标题          # 必填：页面标题
date: YYYY-MM-DD HH:MM:SS  # 可选：发布日期
categories: [分类]       # 可选：文章分类
tags: [标签1, 标签2]     # 可选：文章标签
---
```

---

## 9. Liquid 模板语法

| 语法 | 说明 | 示例 |
|------|------|------|
| `{{ variable }}` | 输出变量 | `{{ page.title }}` |
| `{{ variable \| filter }}` | 管道过滤器 | `{{ post.date \| date_to_string }}` |
| `{% tag %}` | 逻辑标签 | `{% for post in site.posts %}` |
| `{% endtag %}` | 结束标签 | `{% endfor %}` |

---

## 10. 扩展指南

### 10.1 添加新文章

```bash
# 在 _posts/ 目录创建新文件
touch _posts/2024-01-01-my-new-post.md
```

### 10.2 添加新页面

```bash
# 在根目录创建页面文件
touch about.md
```

### 10.3 添加样式

```bash
# 创建 CSS 文件
mkdir -p css
touch css/style.css
```

然后在 `_layouts/default.html` 中引入：
```html
<link rel="stylesheet" href="/css/style.css">
```

---

## 11. 最佳实践

1. **文章命名**: 严格遵循 `YYYY-MM-DD-title.md` 格式
2. **Front Matter**: 确保每篇文章都有完整的元数据
3. **布局继承**: 保持布局模板简洁，内容层负责具体展示
4. **版本控制**: 只提交源文件，`_site/` 已加入 `.gitignore`
5. **本地测试**: 推送前务必在本地运行 `jekyll serve` 验证

---

## 12. 故障排查

| 问题 | 解决方案 |
|------|----------|
| 构建失败 | 检查 Ruby 和 Jekyll 版本；运行 `bundle install` |
| 文章不显示 | 确认文件名格式正确；检查 Front Matter 完整性 |
| 布局异常 | 检查 Liquid 语法；确认模板路径正确 |
| 404 错误 | 检查 `_config.yml` 中的 `baseurl` 配置 |

---

**文档版本**: 1.0  
**生成日期**: 2026-05-28  
**项目类型**: Jekyll 静态博客
