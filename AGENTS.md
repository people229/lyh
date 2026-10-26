# AGENTS.md

Static HTML/CSS classroom exercises for《高级网页设计》. Flat directory of standalone pages: no build step, no package manager, no tests, no linter, no dev server (open files directly in a browser to verify), and the directory is not a git repo.

## Structure

- `index.html` — hub page: a `.link-grid` of `<a class="card" href="./N-M 名称.html">` cards. All UI text is Chinese (`lang="zh-CN"`).
- `N-M 名称.html` — one self-contained file per lesson exercise (inline `<style>`).
- `img/` — images, referenced only by `7-1 上图下文.html`, `7-2 左图右文.html`, `10-2.html`.

## When adding or renaming a page

- Update `index.html`: add a card to `.link-grid` **and** bump the badge text `共 N 个页面` (currently 23; all pages through `11-2.html` are linked).
- Filenames mix Chinese and spaces (e.g. `4-1 css2.html`, `6-1 try.html`). Existing hrefs are raw/unencoded (`./5-1 层叠与继承.html`) — match names exactly; don't rename casually.

## Conventions & gotchas

- Files are UTF-8 without BOM, `<meta charset="UTF-8">`, Chinese content. Preserve encoding and language when editing.
- Pages are self-contained: put CSS in an inline `<style>` block. The only shared stylesheet is `css.css`, linked solely by `5-1 层叠与继承.html`.
- Image filenames have a quirk: `img/1 .jpg` and `img/2 .jpg` contain a literal space before `.jpg` (images 3–9 don't). Copy references exactly.
- Naming: `<chapter>-<exercise>`; a `try` suffix marks practice/experiment pages (e.g. `2-2try.html`).

## Standing user rules

- **Every newly created `.html` file must be linked from the homepage** `index.html` (add a card + bump the badge — see “When adding or renaming a page”). The owner requires all new pages to be reachable from index; a new page without its index link counts as unfinished work.
- All CSS class names, id names, and JS variable names in new/edited pages **must start with `lyh_`** (e.g. `.lyh_page`). Older exercise pages predate this rule; don't rename them unless asked.
- **No third-party libraries or CDNs.** All pages must use only native HTML, CSS, and JavaScript. No Bootstrap, no Tailwind, no external `<script src="...">` / `<link href="...">` from CDN (iconfont is the only exception — load it from the local `font/` directory).
- **Icons must use the local iconfont** under `font/font_5244708_zkj0shedp19/`. Link `<link rel="stylesheet" href="./font/font_5244708_zkj0shedp19/iconfont.css">` in `<head>` and use `<i class="iconfont icon-xxx"></i>` to render. Do not use Font Awesome CDN, Lucide CDN, or any other icon source.
- Every newly created `.html` page **must include a block comment at the top** stating: 姓名、建立时间、使用的大模型、功能名称（示例见下方注释模板）。
- Before executing any user prompt, **append** (never overwrite) an entry to `liang_prompt.md` containing: timestamp (`yyyy-MM-dd HH:mm`), model (`opencode/mimo-v2.6-flash-free`), and the full prompt text. This is a hard requirement of the repo owner.

## 新页面头部注释模板

```html
<!--
  姓名: 梁月虹
  建立时间: yyyy-MM-dd HH:mm
  使用大模型: <创建该页面时实际使用的大模型名称>
  功能: <本页面功能简述>
-->
```
