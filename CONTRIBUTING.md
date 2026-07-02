# CONTRIBUTING.md — 本仓库的版本维护规则

本文件告诉任何 Agent（Claude、Codex、Gemini……）和人类贡献者，如何一致地维护这个仓库的版本。规则借鉴自 [paper-research-skill](https://github.com/Geek96/paper-research-skill) 的 `CLAUDE.md`。

---

## ⚠️ 版本号 — 每次 commit 前必须检查

> **强制**：Agent 每次 commit 前必须执行版本检查。不执行 = 违规。
> **禁止跳版本号**：Agent 只能递增 PATCH（最后一位），绝对不能跳版本（如 1.0.5 → 1.4.0 ❌）。

版本号格式：`MAJOR.MINOR.PATCH`，存放在根目录 [`version.json`](version.json) 的 `version` 字段——这是唯一真源（single source of truth）。

| 位 | 规则 | 谁来改 |
|----|------|--------|
| **PATCH** | 每次 commit 改动了用户可见内容（`AGENTS.md` / `personas/` / `templates/` / `README*.md`）就 +1 | Agent（自动） |
| **MINOR** | PATCH 达到 **10** 时自动进位，PATCH 归零 | Agent（自动进位） |
| **MAJOR** | 仅当用户明确说"升大版本 / breaking change"时才改 | **仅人类授权** |

### 🔴 Pre-Commit Checklist（每次 commit 前必做）

```
□ 1. cat version.json → 读取当前版本号
□ 2. 本次 commit 是否改了 AGENTS.md / personas/ / templates/ / README.md / README.zh-CN.md？
     → 是：PATCH +1（只 +1，不跳）
     → 否：不 bump（见下方"跳过 bump"清单）
□ 3. PATCH = 10？→ PATCH 归零，MINOR +1，同时汇总写 CHANGELOG.md
□ 4. 在同一个 commit 中更新 version.json
□ 5. 同步更新 README.md 与 README.zh-CN.md 顶部 badge 中的版本号
□ 6. commit message 末尾带上版本号
```

**跳过 bump 的改动**：`.gitignore`、`LICENSE`、`sessions/` 下的对局记录、纯 typo（无实质内容变化）。

### 例子

| 改动前 | 动作 | 改动后 | 是否合规 |
|--------|------|--------|:--:|
| `1.0.3` | 改了 AGENTS.md 里一条规则 | `1.0.4` | ✅ |
| `1.0.9` | 改了某人物 persona | `1.1.0`（进位） | ✅ |
| `1.0.5` | Agent 自己跳成 `1.4.0` | — | ❌ 禁止 |
| `1.3.0` | Agent 自己升成 `2.0.0` | — | ❌ 需用户明确授权 |

---

## Changelog & Release

### 三层记录体系

| 层级 | 文件 | 粒度 | 何时写 |
|------|------|------|--------|
| **Git log** | git commit messages | 每次 commit | 自动 |
| **CHANGELOG.md** | [`CHANGELOG.md`](CHANGELOG.md) | 每次 MINOR 进位 | 进位时汇总该轮所有 patch |
| **GitHub Release** | GitHub Releases | 每次 MINOR 进位 | 与 CHANGELOG 同步，用 `gh release create` |

### CHANGELOG 规则

> **不逐 PATCH 写 CHANGELOG**。只在 MINOR 进位时（如 1.3.9 → 1.4.0），回顾该 MINOR 周期内所有 commit，汇总为一条 release entry。

写入内容（汇总时）：
- ✅ 新增/调整的人物 persona（`personas/`）
- ✅ 新增/调整的茶会模式或模板（`templates/`）
- ✅ `AGENTS.md` 里协议行为的变化（发言格式、desire 机制、场景与神态规则等）
- ✅ 影响使用体验的 bug fix
- ✅ Breaking change（标记 `⚠️ Breaking`）

跳过：
- ❌ `.gitignore`、`LICENSE`、`CONTRIBUTING.md` 内部编辑
- ❌ 非协议文字的 typo 修复
- ❌ `sessions/` 下新增的对局记录

格式采用 [Keep a Changelog](https://keepachangelog.com/en/1.0.0/)，条目分组为 `Added` / `Changed` / `Fixed` / `Removed`。

### Release 规则

MINOR 进位时执行：
1. 更新 `CHANGELOG.md`（汇总本轮所有 patch）
2. `git tag v{{version}}`
3. `gh release create v{{version}}`，release notes 复用 CHANGELOG 内容
4. 不在 PATCH 级别打 tag 或发 release

---

## Commit Messages

使用 [Conventional Commits](https://www.conventionalcommits.org/)：

```
feat(agents): short description
fix(persona-nietzsche): short description
docs: short description
chore: short description
```

版本 bump 必须和触发它的改动在同一个 commit 里，不单独开"bump version"的 commit。
**版本号必须出现在 commit message 末尾**，格式：`(v1.0.4)`。例如：`feat(agents): add 场景与神态描写 rules (v1.0.4)`。

---

## 文件角色对照

| 本仓库 | 对应 paper-research-skill 里的角色 |
|--------|-----------------------------------|
| `AGENTS.md` | 相当于 `skills/*/SKILL.md`——核心协议内容 |
| `personas/`、`templates/` | 相当于 `skills/paper-wiki/templates/`——可复用子模块 |
| `version.json` | 相当于 `.claude-plugin/plugin.json` 里的 `version` 字段 |
| `CONTRIBUTING.md`（本文件） | 相当于 `CLAUDE.md` |
