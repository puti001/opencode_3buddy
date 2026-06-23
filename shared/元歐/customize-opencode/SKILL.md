---
name: customize-opencode
description: 編輯 opencode 設定檔（opencode.json、opencode.jsonc、.opencode/、~/.config/opencode/）。建立或修復 agents、subagents、skills、plugins、MCP servers、permission rules。當使用者提到「改設定」「改 opencode 設定」「裝技能」「加 agent」「加 MCP」時載入。
---

# Customizing opencode

opencode 驗證設定很嚴格，填錯就無法啟動。以下涵蓋常用設定，完整內容請參考 JSON Schema：

**<https://opencode.ai/config.json>**

所有 `opencode.json` 都應該加上 `"$schema": "https://opencode.ai/config.json"` 讓編輯器即時檢查。

## 生效方式

設定只在啟動時載入一次。修改後需要重啟 opencode 才會生效。

## 檔案存放位置

| 範圍 | 路徑 |
|------|------|
| 專案設定 | `./opencode.json`、`./opencode.jsonc` 或 `.opencode/opencode.json` |
| 全域設定 | `~/.config/opencode/opencode.json` |
| 專案 agents | `.opencode/agent/<name>.md` 或 `.opencode/agents/<name>.md` |
| 全域 agents | `~/.config/opencode/agent(s)/<name>.md` |
| 專案 commands | `.opencode/command/<name>.md` 或 `.opencode/commands/<name>.md` |
| 全域 commands | `~/.config/opencode/command(s)/<name>.md` |
| 專案 skills | `.opencode/skill(s)/<name>/SKILL.md` |
| 全域 skills | `~/.config/opencode/skill(s)/<name>/SKILL.md` |
| 外部 skills（自動載入） | `~/.claude/skills/<name>/SKILL.md`、`~/.agents/skills/<name>/SKILL.md` |

專案設定會覆蓋全域設定。

## opencode.json 常用欄位

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "provider/model-id",
  "instructions": ["AGENTS.md"],
  "skills": {
    "paths": [".opencode/skills", "/abs/path/to/skills"]
  },
  "permission": {
    "edit": "deny",
    "skill": { "*": "allow" }
  },
  "agent": {
    "my-agent": {
      "model": "...",
      "mode": "subagent",
      "description": "..."
    }
  },
  "command": {
    "deploy": { "description": "...", "template": "..." }
  },
  "mcp": {
    "playwright": {
      "type": "local",
      "command": ["npx", "-y", "@playwright/mcp"]
    }
  }
}
```

## Skills 格式

```
~/.config/opencode/skills/<name>/SKILL.md
```

```markdown
---
name: my-skill
description: 一句話說明技能做什麼 AND 何時觸發。前面放關鍵字。
---

# My Skill

(技能本體：指示、範例、參考資料)
```

- `name` 必填，小寫 hyphen 分隔，最長 64 字，需與資料夾同名
- `description` 必填，沒寫就不會被載入

## 疑難排解

如果設定壞掉 opencode 開不起來，用這些環境變數救援：

- `OPENCODE_DISABLE_PROJECT_CONFIG=1`：跳過專案設定，只載入全域
- `OPENCODE_CONFIG=/path/to/file.json`：載入額外設定檔
- `OPENCODE_PURE=1`：跳過所有外掛
