# Claude Statusline 工具說明

這是一個使用 Go 語言編寫的高效能狀態列 (Statusline) 工具，專為 Claude Code 環境設計。它能從標準輸入 (Stdin) 接收 JSON 資訊，並即時分析專案狀態、Git 資訊、Context 使用量以及工作時間。

## 🌟 核心功能

### 1. 模型智慧辨識
根據當前使用的 Claude 模型自動切換視覺風格：
- **💛 Opus**: 金色圖示
- **💠 Sonnet**: 青色圖示
- **🌸 Haiku**: 粉色圖示

### 2. 專案與 Git 狀態
- 自動擷取當前工作目錄名稱。
- 顯示當前 Git 分支（例如：`⚡ main`）。
- **效能優化**：內建 5 秒的分支資訊快取，避免頻繁呼叫 `git` 指令造成的延遲。

### 3. 自動會話追蹤 (Session Tracker)
- **時間累計**：自動計算今日投入在所有會話中的總時數。
- **活躍判斷**：10 分鐘內的活動會被視為連續區間，超過則另計新區間。
- **儲存位置**：資料持久化於 `~/.claude/session-tracker/sessions/*.json`。

### 4. Context / Token 視覺化進度條
- **即時分析**：從對話紀錄 (Transcript) 中精準提取最新的 Token 使用數據。
- **視覺回饋**：提供 10 格的彩色進度條（█/░）：
  - **綠色 (<60%)**：安全範圍。
  - **黃色 (60%-80%)**：建議準備總結或開啟新會話。
  - **紅色 (>80%)**：接近 200k Token 上限。

### 5. 使用者訊息預覽
- 擷取最近一次的使用者提問並顯示在狀態列下方。
- **智慧過濾**：自動過濾掉系統生成的 JSON、XML 標籤或命令列輸出，僅保留人類輸入的文字。
- **格式化顯示**：自動換行並限制最大顯示行數（3行），確保介面整潔。

## 🛠 技術特點

- **併發處理**：使用 Go Goroutines 同時處理 Git 檢查、檔案分析與時間計算，極大化反應速度。
- **ANSI 真彩色**：使用 24-bit 顏色定義，提供精緻的視覺體驗。
- **健壯性**：具備強大的 JSON 解析錯誤處理與長檔案讀取緩衝 (1MB buffer)。

## 🚀 安裝與使用

### 1. 前置需求
- 系統需安裝 [Go 語言](https://go.dev/dl/) (建議 1.20 以上版本)。
- 具備 Git 環境。

### 2. 編譯與安裝
在專案根目錄執行以下指令：

```bash
# 編譯程式碼
go build -o statusline-go statusline.go

# 將執行檔移動到系統路徑，方便全域呼叫
mv claude-statusline ~/.claude/
```

### 3. 如何在 Claude Code 中使用
此工具設計為接收 Claude Code 傳遞的 JSON 狀態資訊。如果你正在開發整合介面，可以將此程式設定為狀態列的渲染引擎。

### 4. 手動測試
把以下設定加入的 `~/.claude/settings.json` 來驗證輸出效果：

```bash
  "statusLine": {
    "type": "command",
    "command": "~/.claude/statusline-go",
    "padding": 0
  },
```

## 📥 輸入資料格式 (JSON)

程式預期透過 `Stdin` 接收以下格式：

```json
{
  "model": {
    "display_name": "Claude 3.5 Sonnet"
  },
  "session_id": "unique-session-uuid",
  "workspace": {
    "current_dir": "/path/to/project"
  },
  "transcript_path": "/path/to/transcript.jsonl"
}
```

## 🖥 輸出範例

```text
[💠 💛 Claude 3.5 Sonnet] 📂 project-name ⚡ main | █ ██░░░░░░░ 25% 50k | 1h 20m
｜這是我最近提問的問題內容...
```
