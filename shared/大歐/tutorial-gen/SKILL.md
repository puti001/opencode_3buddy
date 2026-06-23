---
name: tutorial-gen
description: 將輸入內容（文字、網址或檔案）轉化為互動翻轉卡片網頁的技能。當用戶提到「製作翻轉卡片」、「產生教學網頁」、「翻轉卡片」、「教學模版」時載入。
---

# 互動翻轉卡片教學網頁產生器技能

當用戶要求「製作翻轉卡片」、「生成翻轉卡片教學網頁」或類似指令時，請使用此技能。

## 執行流程

1. **解析與處理用戶輸入**：
   - **純文字 / 網址**：可以直接使用對應的純文字或網址模式。
   - **多模態檔案 (圖片、音訊、影片、PDF、PPT 等)**：
     - 若用戶提供了圖片（如筆記截圖、心智圖）、音訊檔（課堂錄音）、影片檔（教學影片）或文件檔案；
     - 請**先利用你的多模態 LLM 理解能力**，將該多模態資料中的核心知識點、摘要或逐字稿，詳細整理成一份結構清晰的**繁體中文文字大綱**。
     - 接著，將這份整理好的文字大綱，寫入一個臨時文字檔案中。
     - 最後，使用 **檔案模式** 來執行產生器，將該臨時檔案路徑作為參數傳入。

2. **執行 Python 產生器**：
   - 產生器指令腳本位於：`C:\antigravity\human\opencode-tutorial-generator\generator.py`。
   - 請根據輸入類型，在終端機中運行對應的命令：
     - **網址模式**：
       `python C:\antigravity\human\opencode-tutorial-generator\generator.py --url "<網址>"`
     - **檔案模式**：
       `python C:\antigravity\human\opencode-tutorial-generator\generator.py --file "<檔案路徑>"`
     - **純文字模式**：
       `python C:\antigravity\human\opencode-tutorial-generator\generator.py --text "<文字內容>"`
       *(注意：若文字內容很長或含有換行，請將其寫入一個臨時文字檔，然後使用 `--file` 模式執行，以防命令列長度限制或換行解析錯誤)*

3. **回報結果**：
   - 執行成功後，腳本會輸出生成的 HTML 檔案路徑（例如：`💾 輸出檔案：C:\...`）。
   - 請向用戶報告生成成功，並提供該 HTML 檔案的完整本地路徑（請以 Markdown 連結格式輸出，例如 `[點此打開網頁](file:///C:/path/to/generated.html)`，方便用戶直接點擊瀏覽）。
