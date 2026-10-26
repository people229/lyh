---
name: opencode-project-rules
description: Project conventions for the classroom HTML exercises. Use when creating editing or renaming any .html page in this workspace. Do not use outside this workspace.
---

# opencode 项目操作规范

本目录是《高级网页设计》课堂练习集合：扁平目录、纯静态、无构建工具、无包管理器、无测试。所有页面直接双击浏览器打开即可。

## 项目结构

- `index.html` — 导航首页，`.link-grid` 里是 `.card` 卡片，`lang="zh-CN"`，徽章文字形如 `共 N 个页面`
- `N-M 名称.html` — 每个练习一个独立文件，CSS 全部内联在 `<style>` 里
- `img/` — 图片目录，只有 7-1、7-2、10-2 引用
- `css.css` — 仅 `5-1 层叠与继承.html` 使用的共享样式
- `cdn/` — 本地下载的 Font Awesome / Lucide 资源
- `font/` — iconfont 图标资源

## 硬规则（必须遵守）

### 0. 只用原生技术栈（新增）

- 只能用 **原生 HTML + 原生 CSS + 原生 JavaScript**，不引任何第三方库或框架
- 禁止 Bootstrap / Tailwind / jQuery / Vue / React / Chart.js / 任何 `<script src="...">` / `<link href="...">` 形式的外部 CDN
- **图标唯一来源：** `./font/font_5244708_zkj0shedp19/iconfont.css`
  - 在 `<head>` 里写 `<link rel="stylesheet" href="./font/font_5244708_zkj0shedp19/iconfont.css">`
  - 渲染：`<i class="iconfont icon-xxx"></i>`（具体 icon-xxx 类名查 `font/font_5244708_zkj0shedp19/demo_index.html` 或 `iconfont.json`）
- 旧页面（如 `cdn/` 目录下的资源、13-1~13-4）历史遗留，不在新页面里继续用

### 1. 执行任何 prompt 前 → 追加 liang_prompt.md

写入模板（**追加**，不覆盖）：

```markdown

## yyyy-MM-dd HH:mm

- model: opencode/mimo-v2.6-flash-free
- prompt: 这里写完整的用户原始提示词
```

用 PowerShell `Add-Content` 追加，不要覆盖。

### 2. 新建/编辑 HTML → CSS 类名、id、JS 变量必须 `lyh_` 开头

示例：`.lyh_page`、`#lyh_header`、`var lyh_count = 0`。旧页面里没有 `lyh_` 前缀的代码不要主动改，除非用户明确要求。

### 2.5 新建 HTML → 头部必须加注释块

紧跟 `<!DOCTYPE html>` 之后、`<html>` 之前，加入：

```html
<!--
  姓名: 梁月虹
  建立时间: yyyy-MM-dd HH:mm
  使用大模型: <创建该页面时实际使用的大模型名称>
  功能: <本页面功能简述>
-->
```

姓名固定为 `梁月虹`；建立时间取当前系统日期和时间（精确到分钟）；使用大模型填写创建该页面时实际使用的模型名称（如实填写，不得编造）；功能根据页面实际用途写一句话。

### 3. 新建 HTML 页面 → 必须更新 index.html

1. 在 `.link-grid` 里加一个 `<a class="card" href="./N-M 名称.html">` 卡片，内含 `.file-name` 和 `.file-tag`
2. 把徽章文字 `共 N 个页面` 的 N 加 1
3. 文件名、href 里的路径**原样匹配**（含中文和空格，不做 URL 编码）

不更新 index = 没完成。

## 页面创建规范

- 文件编码：UTF-8 无 BOM，`<meta charset="UTF-8">`
- `<html lang="zh-CN">`，页面标题中文
- CSS 放内联 `<style>`，不要外链（除非复用 `css.css`）
- 图片引用注意：`img/1 .jpg` 和 `img/2 .jpg` 里有**空格**在 `.jpg` 前面，复制时一字不差
- 文件命名：`<章节>-<练习号> 名称.html`，例如 `4-1 css2.html`、`5-1 层叠与继承.html`；`try` 后缀表示尝试练习（如 `2-2try.html`）
- 目录不是 git 仓库（但实际有 `.git`），git 提交用另一个 skill `git-commit-push`

## 做什么 / 不做什么

- 做：按用户指令创建/修改练习页面、写内联 CSS、引用本地资源、更新 index、记录 prompt 日志
- 不做：引入 npm / vite / tailwind（除非用户明确要求）、自动 git push（除非调用了 git-commit-push skill）、重构旧页面的非 lyh_ 命名
