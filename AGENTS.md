# Agent Guide

本文件给 AI 代理使用，说明本仓库内必须遵守的开发和提交规则。面向人的项目说明见 [README.md](README.md)。

## 基本规则

- 默认在 `master` 上开发；提交前确认 `git status --short` 只包含本次任务相关文件。
- 不要回滚用户已有改动；遇到无关脏工作区直接忽略，除非它直接阻塞当前任务。
- `pyproject.toml` 里的 `akshare==` 版本号由每日定时的 GitHub Actions 自动更新并打 tag，不要手动改这个版本号，除非确实需要在本地验证新版本兼容性。

## 提交规则

- 提交信息统一使用中文，subject 和 body 都必须写中文。
- 格式：`<type>(<scope>): <中文摘要>`；type 用 `feat`/`fix`/`refactor`/`docs`/`test`/`build`/`ci`/`chore`，不随意新增。
- 摘要简洁说明实际行为；能用 subject 说清楚的不写 body，涉及原因/影响/结构变更时再写 body，用中文列表说明要点。
- 需要 body 时用单个 `git commit -m $'...\n\n...'` 传入完整信息，避免交互式编辑器或多次 `-m` 产生多余换行。
- 不要加入 AI 署名、生成标识、协作者 trailer 或工具标记。
- akshare 函数名等专有名词保持原文，不要翻译或改写。

## 常用校验

```bash
pytest
pytest --cov=app --cov-report=html
```

CI（`update-akshare-and-build.yml`）在 push/PR 时会跑一次 `pytest -v --tb=short`，改动后本地先跑一遍再提交。

## 禁止事项

- 不要绕过 `ENABLE_FUNCTION_WHITELIST`/`ALLOWED_FUNCTIONS` 白名单直接放行任意 akshare 函数调用。
- 不要硬编码凭据或把生产环境变量写进仓库。
