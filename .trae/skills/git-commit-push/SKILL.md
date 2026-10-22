---
name: git-commit-push
description: Automatically stage all changes, commit with a Chinese message, and push to Gitee remote. Use when the user says commit, push, 提交项目, or 推送代码. Do not use for interactive or partial commits.
---

# Git Commit & Push

Stage every change in the workspace, create a single commit with a concise Chinese message, and push to `origin/main`.

## Target

- Repository root: current workspace folder that contains this skill
- Remote: `origin` → `https://gitee.com/liang-yuehong/lyh.git`
- Branch: `main`

## Procedure

1. Run `git status --short --no-pager` to confirm there is something to commit. If the working tree is clean, skip to step 5 and report "没有需要提交的变更".
2. Stage everything: `git add -A`
3. Commit with a Chinese message: `git commit -m "<message>"`
   - `<message>` should briefly describe what changed, in Chinese. Examples:
     - `新增 13-1 至 13-4 图标练习页面`
     - `更新 index.html 页面导航和徽章数量`
     - `补充 14-1 JavaScript 基础练习`
   - If the user already provided a commit message, use it verbatim instead of inventing one.
4. Push: `git push origin main`
5. Report the commit hash and push result.

## Notes

- This project (`d:\web`) is not a git repo in the conventional sense — it is a flat classroom exercise folder that happens to be tracked by git. Do not create branches, tags, or merge commits unless the user explicitly asks.
- Never `git push --force`.
- If the push is rejected due to remote divergence, stop and ask the user — do not rebase or pull automatically.
- Windows PowerShell environment: all commands run without `cmd.exe` wrappers.
