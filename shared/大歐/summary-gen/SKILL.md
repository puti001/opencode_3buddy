---
name: summary-gen
description: 從網址、檔案或純文字內容，自動產生結構化的重點摘要。當用戶提到「產生摘要」、「總結文章」、「重點整理」時載入。
dependencies: [requests, beautifulsoup4]
---

# 重點摘要產生器技能

當用戶要求「產生摘要」、「總結這篇文章」、「幫我整理重點」或類似指令時，請使用此技能。

## 執行流程

1. **解析用戶輸入**：
   - **網址模式**：以 `http://` 或 `https://` 開頭 → 使用 `--url` 參數
   - **檔案模式**：提供本地路徑 → 使用 `--file` 參數
   - **純文字模式**：直接貼上文字 → 使用 `--text` 參數
   - 可選參數：`--audience` 指定目標受眾、`--custom-prompt` 附加自訂指示

2. **執行 Python 產生器**：
   ```
   python C:\antigravity\human\opencode-tutorial-generator\summary_generator.py --url "<網址>"
   python C:\antigravity\human\opencode-tutorial-generator\summary_generator.py --file "<路徑>"
   python C:\antigravity\human\opencode-tutorial-generator\summary_generator.py --text "<文字>"
   ```

3. **回報結果**：
   - 輸出摘要文字內容（Markdown 格式）
   - 直接在此對話中呈現給用戶
