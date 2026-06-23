---
name: shared-folder-convention
description: 大歐（ChromeOS OpenCode）、元歐（主電腦 OpenCode）、小歐（Telegram Bot）三兄弟的共用資料夾協定。路徑在 /mnt/shared/GoogleDrive/MyDrive/telegram/shared/。當使用者提到「共用資料夾」「三兄弟」「大歐」「元歐」「小歐」「共享」時載入。
---

# 三兄弟共用資料夾協定

## 角色

| 稱呼 | 身份 | 說明 |
|------|------|------|
| **元歐** | 主電腦 OpenCode | Puti 主要工作電腦上的 OpenCode |
| **大歐** | ChromeOS OpenCode | 現在這台 ChromeOS 上的 OpenCode |
| **小歐** | Telegram Bot | @PutiOpenCode_bot |
| **Puti 老師** | 使用者 | 黃朝榮師兄，三兄弟的主人 |

## 共用資料夾

路徑：`/mnt/shared/GoogleDrive/MyDrive/telegram/shared/`

```
shared/
├── PUTI_TEACHER.md    # Puti 老師個人設定與偏好
├── AGENTS.md          # 指向 PUTI_TEACHER.md
├── 大歐/              # 大歐的資料夾（元歐放技能給大歐的地方）
│   ├── <skill-name>/
│   │   └── SKILL.md
│   └── ...
├── 元歐/              # 元歐的資料夾（大歐放技能給元歐的地方）
│   ├── <skill-name>/
│   │   └── SKILL.md
│   └── ...
└── 小歐/              # 小歐的資料夾
    └── ...
```

## 協定

1. **推技能**：把 SKILL.md 放到對方的資料夾，對方重啟後就會看到
2. **留言**：可以在對方資料夾放 `.md` 檔案作為留言
3. **記憶**：各角色可以在自己資料夾放 `SELF.md` 記錄自我介紹與偏好，重啟後透過 `instructions` 載入
4. **即時性**：技能透過 Google Drive 同步，所以放上去後對方就能讀到（但需重啟 opencode 才會載入新技能）

## 注意事項

- 所有檔案路徑都在 Google Drive 上，會自動同步
- 技能 SKILL.md 需符合 opencode 的 frontmatter 格式
- 重啟 opencode 才能讀取新技能
