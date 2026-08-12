# 乐可开源 GitHub 组织主页升级实施计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 把 `github.com/lekeopen` 升级为专业、克制、对开发者友好的公司技术名片，并准确展示核心产品、精选开源项目和开放边界。

**Architecture:** `profile/README.md` 是公开主页内容的唯一源码；仓库 description、homepage、topics 和组织置顶仓库是 GitHub 平台元数据。README 通过独立分支与 PR 交付，平台元数据逐仓库更新并保留旧值，最终以 Public 视角统一验收。

**Tech Stack:** GitHub Flavored Markdown、Git、GitHub CLI、GitHub 组织主页设置

## Global Constraints

- 中文优先，专业、直接、克制，不使用广告式文案、夸大能力或虚构数据。
- 不修改官网、产品功能、仓库可见性、私有源码、组织头像、组织名称或法律主体信息。
- Public 视角不得出现私有仓库入口；小乐 AI 与乐教库只链接公开产品或文档入口。
- “核心产品”与“精选开源与工程”必须分开，不能因为项目位于 GitHub 就统一称为开源。
- 归个类仓库必须明确是官方版本发布与下载仓库，不代表完整源码开放。
- 保留 `BLOG-POST-LIST:START` 和 `BLOG-POST-LIST:END` 标记，最近动态只展示三条。
- 不添加横幅、GIF、访问计数器、大量徽章或易过期数据。
- README 走独立分支与 PR；未经明确授权，不合并 PR、不修改元信息、不设置置顶仓库。
- 登录、MFA、CAPTCHA 和权限确认由组织所有者处理。

---

### Task 1: 重构公开组织主页 README

**Files:**
- Modify: `profile/README.md`
- Test: `profile/README.md`

**Interfaces:**
- Consumes: `docs/superpowers/specs/2026-08-12-github-organization-profile-upgrade-design.md` 的批准文案、结构和链接。
- Produces: Public 组织主页 Markdown，供 Task 4 最终验收。

- [ ] **Step 1: 创建独立分支并记录基线**

```bash
git status -sb
git switch -c codex/github-organization-profile-upgrade
git rev-parse HEAD
```

预期：从当前 `origin/main` 建立分支，不混入其他任务改动。

- [ ] **Step 2: 按规范重写页面**

页面严格采用以下顺序：

```text
# 👋 乐可开源 · LekeOpen
公司定位与四个快速入口
## 🚀 核心产品
乐可点名 / 归个类 / 小乐 AI / 乐教库
## 🛠️ 精选开源与工程
leke-picker / codex-skills / lekee-official-site / uvindex240370sensor
## 🧩 Codex Skills
品牌系统构建 / 开源工具评估 / 社交内容分发 / 查看全部
## 📰 最近动态
自动标记内最近三条
页尾稳定入口
```

所有精确文案和链接取自设计规范。不得链接 `lejiaoku-web`、`lejiaoku-backend`、`ai-file-organizer`、`classroom-random-picker` 或 `rockts/xiaole-ai`。

- [ ] **Step 3: 验证结构与公开边界**

```bash
test "$(grep -c '^# ' profile/README.md)" -eq 1
test "$(grep -c '<!-- BLOG-POST-LIST:START -->' profile/README.md)" -eq 1
test "$(grep -c '<!-- BLOG-POST-LIST:END -->' profile/README.md)" -eq 1
test "$(sed -n '/BLOG-POST-LIST:START/,/BLOG-POST-LIST:END/p' profile/README.md | grep -c '^- \[20')" -eq 3
! grep -E 'lejiaoku-(web|backend)|ai-file-organizer|classroom-random-picker|rockts/xiaole-ai' profile/README.md
git diff --check
```

预期：全部退出 0。

- [ ] **Step 4: 检查外链**

```bash
grep -oE 'https://[^) ]+' profile/README.md | sort -u
```

逐一执行有界 HEAD；不支持 HEAD 时回退 GET。任何 404、私有登录页或错误产品路径必须修正。

- [ ] **Step 5: 提交计划内文件**

```bash
git add profile/README.md docs/superpowers/specs/2026-08-12-github-organization-profile-upgrade-design.md docs/superpowers/plans/2026-08-12-github-organization-profile-upgrade.md
git diff --cached --check
git commit -m "docs: upgrade GitHub organization profile"
```

预期：提交只包含主页、设计规范和实施计划。

### Task 2: 审查并发布 README PR

**Files:**
- Review: `profile/README.md`
- Review: `docs/superpowers/specs/2026-08-12-github-organization-profile-upgrade-design.md`
- Review: `docs/superpowers/plans/2026-08-12-github-organization-profile-upgrade.md`

**Interfaces:**
- Consumes: Task 1 提交和验证证据。
- Produces: 可供人工审查的 PR，不自动合并。

- [ ] **Step 1: 进行规范和质量双重审查**

逐项确认：产品与开源边界准确、无私有链接、归个类性质明确、自动标记完整、页面长度适当、三份文档没有矛盾。Critical 或 Important 问题必须修复并复审。

- [ ] **Step 2: 推送分支并创建 PR**

```bash
git push -u origin codex/github-organization-profile-upgrade
gh pr create --base main --head codex/github-organization-profile-upgrade --title "docs: upgrade GitHub organization profile" --body-file /absolute/path/to/reviewed-pr-body.md
```

PR 正文记录目标、结构变化、私有链接边界、验证和回滚。创建后不自动合并。

- [ ] **Step 3: 等待合并授权**

报告 PR URL、审查结论和检查状态。只有用户明确授权后才能合并；合并后再进入外部元数据写入。

### Task 3: 更新四个公开仓库元信息

**Files:**
- Modify external metadata: `lekeopen/leke-picker`
- Modify external metadata: `lekeopen/codex-skills`
- Modify external metadata: `lekeopen/guigelei-releases`
- Modify external metadata: `lekeopen/lekee-official-site`
- Conditionally modify: `lekeopen/guigelei-releases/README.md`

**Interfaces:**
- Consumes: 设计规范第 5 节的精确 description、homepage 和 topics。
- Produces: 一致的公开仓库元信息和可回滚报告。

- [ ] **Step 1: 记录修改前值**

逐仓库记录 `nameWithOwner`、`description`、`homepageUrl`、`topics`、`visibility`。报告不得包含 token、Cookie、请求头或权限信息。

- [ ] **Step 2: 检查归个类 README**

若首屏已明确“官方发布与下载仓库、不代表完整源码开放”，不修改；若缺失，先创建独立 PR 补充，不直接改 `main`。

- [ ] **Step 3: 请求元信息写入授权**

向用户列出四个仓库旧值和设计规范中的精确新值。得到明确授权后才可写入。

- [ ] **Step 4: 逐仓库更新并回读**

每更新一个仓库，立即回读相同字段。任何字段不一致时停止后续更新，报告部分完成状态。

- [ ] **Step 5: 生成变更与回滚报告**

报告每个仓库的旧值、新值、结果和回滚值，不记录认证材料。

### Task 4: 设置置顶仓库并进行 Public 验收

**Files:**
- Modify external organization setting: `lekeopen` pinned repositories
- Read-only verify: `https://github.com/lekeopen`

**Interfaces:**
- Consumes: 已合并主页、Task 3 元信息、设计规范第 6 和第 9 节。
- Produces: Public 组织主页验收证据与回滚记录。

- [ ] **Step 1: 记录当前置顶基线**

通过 GraphQL 和 Public 页面记录当前 pinned repositories。若基线已变化，不覆盖未知更新。

- [ ] **Step 2: 请求置顶授权**

目标顺序：

```text
1. leke-picker
2. codex-skills
3. guigelei-releases
4. lekee-official-site
```

明确说明只改变主页展示，不改变仓库权限或内容。

- [ ] **Step 3: 保存 Public 置顶仓库**

在组织主页 Public 视角选择四个指定仓库并保存。若 UI 不支持显式排序，记录实际能力和最终展示顺序，不使用私有仓库填充。

- [ ] **Step 4: 回读数据**

通过 GraphQL 回读 `pinnedItems(first: 6, types: [REPOSITORY])`。预期只包含四个目标仓库；API 与页面顺序不同时，以 Public 页面呈现为展示证据并同时报告 API 返回。

- [ ] **Step 5: Public 页面验收**

确认：定位和快速入口清晰；四个核心产品完整；四个精选项目完整；Codex Skills 只有三个代表能力；动态只有三条；指定仓库已置顶；无私有入口；深色桌面端层级清楚。

- [ ] **Step 6: 最终交付**

报告 README 合并提交与 PR、四个仓库最终元信息、置顶状态、Public 验收结果、平台限制，以及 README、元信息、置顶设置各自的回滚方法。只有全部回读和验收通过后才能宣布完成。
