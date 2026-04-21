# 🤖 omg-claude

[![Claude Code](https://img.shields.io/badge/Claude-Code-purple?style=for-the-badge)](https://anthropic.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

`omg-claude` 是一個專門收集 **Claude Code** (Anthropic CLI) 相關增強工具、配置腳本與使用技巧的開源專案。

我們的目標是透過各種小工具與最佳實踐，讓開發者在使用 Claude Code 進行軟體開發時，擁有更流暢、更具資訊量的開發體驗。

---

## 🛠 已收錄工具

### 1. Claude Statusline
一個高效能的狀態列增強工具，為你的 Claude 對話介面提供即時的視覺回饋。
- **檔案路徑**: `build-in/statusline/statusline.go`
- **主要功能**:
  - 🎨 **模型辨識**: 自動識別 Opus/Sonnet/Haiku 並顯示專屬風格。
  - ⚡ **Git 整合**: 即時顯示當前分支狀態。
  - 📊 **Context 監控**: 視覺化 200k Token 使用量進度條。
  - ⏱️ **時間追蹤**: 統計今日總開發時數。
- **詳情請見**: [STATUSLINE.md](./STATUSLINE.md)

---

## 💡 使用技巧集錦

*(這裡預計收集各種系統提示詞優化、指令別名設定等內容)*

- **高效 Prompting**: 如何編寫針對 Claude Code 優化的 `.clauderc`。
- **工作流優化**: 結合 Git Hook 自動觸發程式碼審查。

---

## 🚀 快速開始

### 編譯狀態列工具
```bash
go build -o claude-statusline build-in/statusline/statusline.go
```

---

## 🤝 貢獻指南

如果你有任何關於 Claude Code 的好用工具、設定檔或技巧，歡迎透過 PR 或是 Issue 進行分享！

1. Fork 本專案。
2. 建立你的特性分支 (`git checkout -b feature/AmazingFeature`)。
3. 提交你的變更 (`git commit -m 'Add some AmazingFeature'`)。
4. 推送到分支 (`git push origin feature/AmazingFeature`)。
5. 開啟一個 Pull Request。

---

## 📄 授權協定

本專案採用 MIT 授權協定，詳情請參閱 [LICENSE](LICENSE) 檔案。
