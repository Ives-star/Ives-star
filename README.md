# Ives-star

## Product Playbook（Claude Code plugin）

本 repo 內含 [product-playbook](https://github.com/kaminoikari/product-playbook) v2.4.0（MIT 授權），位置在 `.claude/skills/product-playbook/`。在這個 repo 開啟 Claude Code 時會以專案範圍的 plugin 自動載入，不需另外安裝。

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
| PreToolUse（Write/Edit） | 規劃階段擋下程式碼寫入、TDD 檢查（沒有對應測試就擋下程式碼修改）、機密掃描 |

PreToolUse hooks 會擋下部分寫入，包括 `index.html` 這類程式碼檔案。要停用某個 hook，請編輯 `.claude/skills/product-playbook/hooks/hooks.json`。

### 更新或移除

- 更新：用新版套件內容取代 `.claude/skills/product-playbook/`（不要放入 `install.sh` 與 `.claude-plugin/marketplace.json`），檢查差異後再 commit。
- 移除：刪除 `.claude/skills/product-playbook/` 並 commit。
