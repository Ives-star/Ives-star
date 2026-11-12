# Ives-star

## Product Playbook（Claude Code 專案 skill）

本 repo 內含 [product-playbook](https://github.com/kaminoikari/product-playbook) v2.4.0（MIT 授權），已從 plugin 轉成一般的專案 skill、專案 agents 與專案 hooks。原因：專案範圍的 skills-directory plugin 在工作區未受信任時會被略過，雲端 session 因此載入不到。

| 元件 | 位置 |
|---|---|
| Skill（入口） | `.claude/skills/product-playbook/SKILL.md`，導向 `skills/product-playbook/SKILL.md`（meta-skill）與 `skills/<lens>/SKILL.md` |
| Agents | `.claude/agents/pre-mortem-runner.md`、`.claude/agents/strategy-critic.md` |
| Hooks | `.claude/settings.json`，執行 `.claude/skills/product-playbook/hooks/*.py` |

### 使用

```
/product-playbook 我想做一個記帳 App
```

也可以直接描述需求（例如「這個功能值不值得做」「幫我寫 PR-FAQ」），Claude 會自動選用對應的 lens：JTBD、PR-FAQ、positioning、pre-mortem、RICE、North Star、MVP、GTM 等。

### 已啟用的 hooks

| Hook | 作用 |
|---|---|
| SessionStart | 載入規劃進度、注入 meta-skill 與開發紀律提示 |
| UserPromptSubmit | 偵測換題或需要連帶修改的提示 |
| PreToolUse（Write/Edit） | 規劃進行中時提醒不要寫程式碼；TDD 提醒（沒有對應測試時提示，不會擋下）；機密掃描（偵測到疑似金鑰時要求確認） |

- TDD 提醒只針對程式碼副檔名（`.ts`、`.js`、`.py` 等），不含 `.html`。在 repo 根目錄放 `.product-tdd-waived` 檔可關閉。
- 要停用某個 hook，請編輯 `.claude/settings.json`。`hooks/hooks.json` 是上游 plugin 的原始定義，僅供參考，不會生效。

### 更新或移除

- 更新：用新版套件內容取代 `.claude/skills/product-playbook/`，然後重做轉換：保留入口 `SKILL.md`、刪除 `.claude-plugin/`、把 `agents/*.md` 移到 `.claude/agents/`、把 `${CLAUDE_PLUGIN_ROOT}` 改成 `.claude/skills/product-playbook`、依新版 `hooks/hooks.json` 更新 `.claude/settings.json`。檢查差異後再 commit。
- 移除：刪除 `.claude/skills/product-playbook/`、`.claude/agents/pre-mortem-runner.md`、`.claude/agents/strategy-critic.md`，並移除 `.claude/settings.json` 的 `hooks` 區塊，然後 commit。
