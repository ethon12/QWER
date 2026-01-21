---
title: 如何在这个博客里写作并发布（完整指南）
description: 这篇文章教你如何在这个博客项目里新建文章、预览、提交并自动部署到线上。
summary: ✍️ 写作 -> 预览 -> 提交 -> 自动上线
series_tag: '从零开始搭建博客'
published: '2026-01-21T00:00:00.000+08:00'
updated: '2026-01-21T00:00:00.000+08:00'
tags:
  - [写作, 教程]
---

这套博客是“文件即内容”的写法：每篇文章就是一个文件夹里的 `index.md`。

## 1. 一篇文章放在哪里？

文章目录在：`user/blogs/`

每篇文章一个文件夹，例如：

```
user/blogs/how-to-write/index.md
```

其中 `how-to-write` 就是文章的 URL 路径：

- 线上地址：`/how-to-write`

## 2. 如何新建一篇文章（手动方式）

1) 在 `user/blogs/` 下新建一个文件夹（建议用英文/短横线）：

- 例如：`user/blogs/my-new-post/`

2) 在这个文件夹里新建 `index.md`

3) 在 `index.md` 开头写“文章信息”（frontmatter），然后写正文。

最小模板（可复制）：

```md
---
title: 文章标题
description: 一句话介绍文章
tags:
  - [随笔]
published: '2026-01-21T00:00:00.000+08:00'
---

## 文章开始

从这里开始写正文...
```

你可以用 Markdown 语法，比如：

- **加粗**：`**加粗**`
- *斜体*：`*斜体*`
- 链接：[GitHub](https://github.com/)：`[GitHub](https://github.com/)`

代码块：

```bash
pnpm dev
```

## 3. 本地预览（推荐）

在项目根目录运行：

```bash
pnpm dev
```

然后打开浏览器访问本地地址（终端会显示类似 `http://localhost:5173/`）。

## 4. 发布到线上（提交并推送）

发布的核心就是：把你新增的文章文件提交到 GitHub。

在项目根目录运行：

```bash
git add .
git commit -m "Add post: my-new-post"
git push
```

你已经把 GitHub 仓库和 Vercel 连好了，所以：

- 只要 `git push` 到 `master`，Vercel 会自动构建并部署
- 部署完成后，线上就能看到新文章

## 5. 常见问题

### 5.1 为什么我新建了文章但线上 404？

这个项目当前使用了 `prerender.entries`（预渲染白名单）。
也就是说：要让某篇文章在生产环境稳定生成静态页面，可能需要把路径加到 `svelte.config.js` 的 `entries` 里。

如果你遇到这种情况，把文章路径（例如 `/my-new-post`）加进去，然后重新提交推送即可。

### 5.2 图片怎么放？

最简单的方式：把图片放到文章文件夹里，然后在 Markdown 里引用。

例如：

```
user/blogs/my-new-post/cover.jpg
```

Markdown 里写：

```md
![封面](./cover.jpg)
```

---

如果你愿意，我也可以把“新建文章”做成最简流程（例如只需要复制一个模板文件夹、改标题就能发）。
