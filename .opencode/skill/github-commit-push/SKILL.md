---
name: github-commit-push
description: Stage all changes, create a Chinese commit, and push the whole project to the GitHub repository https://github.com/people229/lyh.git. Use when the user says 提交到github, 提交commit, push, 推送代码, 推送项目, or 提交项目.
---

# GitHub Commit & Push

Stage every change in the workspace, create a single commit with a concise Chinese
message, and push the whole project to the GitHub repository.

## Target

- Repository root: the current workspace folder
- Remote name: `github`
- Remote URL: `https://github.com/people229/lyh.git`
- Branch: `main`

Keep the existing `origin` remote (Gitee) untouched. This skill only adds/uses a
separate `github` remote.

## Procedure

1. Ensure the GitHub remote exists:
   - `git remote get-url github` → if it fails, run
     `git remote add github https://github.com/people229/lyh.git`
   - If it exists but the URL differs, run
     `git remote set-url github https://github.com/people229/lyh.git`
2. Check the working tree: `git status --short`
   - If there is nothing to commit, skip to step 5 and report
     "没有需要提交的变更，直接推送当前 main".
3. Stage everything: `git add -A`
4. Commit with a Chinese message: `git commit -m "<message>"`
   - `<message>` should briefly describe what changed, in Chinese. Examples:
     - `新增 13-1 至 13-4 图标练习页面`
     - `更新 index.html 页面导航和徽章数量`
     - `补充 14-1 JavaScript 基础练习`
   - If the user already provided a commit message, use it verbatim.
5. Push the whole project: `git push github main`
6. Report the commit hash (if any) and the push result, including the GitHub URL.

## Notes

- Never use `git push --force` / `--force-with-lease`.
- Do not create branches, tags, or merge commits unless the user explicitly asks.
- If the push is rejected because the remote has diverged, stop and ask the user;
  do not pull, rebase, or merge automatically.
- If authentication fails, report it and tell the user to configure GitHub
  credentials (PAT or SSH) instead of retrying blindly.
- On Windows, if push fails with `SSL certificate ... unable to get local issuer
  certificate`, retry once with the native Windows certificate store:
  `git -c http.sslBackend=schannel push github main`. Do not disable SSL
  verification globally.
- Windows PowerShell environment: use `cmd1; if ($?) { cmd2 }` for dependent steps.
