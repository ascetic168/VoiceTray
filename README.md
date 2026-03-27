# Voice Input Tray

> 跨平台系統托盤語音輸入工具 - 支援騰訊雲 ASR 及 Google Gemini 多引擎語音辨識

## 專案狀態

✅ **已發布 v0.2.3** - 新增 Google Gemini 多模態語音辨識，修復設定持久化問題。

## 為什麼使用這個程式

與市面上其他語音輸入工具相比，Voice Input Tray 解決了三個核心痛點：

### 1. 連續麥克風錄音，隨按隨講不吃字
採用持續監聽技術，按下熱鍵的瞬間即可開始說話，完全沒有啟動延遲。同時，其他應用程式也能同時使用麥克風，不會有麥克風獨佔問題——您可以一邊通話、一邊使用語音輸入。

### 2. 單鍵 CTRL，微秒級啟動，智能判斷使用意圖
只需按住 Ctrl 鍵即開始錄音，程式會自動判斷您的使用意圖：
- 按下 Ctrl 後 2 秒內按其他鍵 → 自動取消，不影響 Ctrl+C、Ctrl+V 等快捷鍵
- **支持並發錄音** - 在 ASR 處理期間可繼續錄音，結果按佇列順序依次貼上

您再也不會看到「沒有錄到聲音」之類的訊息——從您按下的那一刻起，錄音就已經在進行了；即便取消錄音，也是安靜的處理，不會干擾使用者。

### 3. 多引擎支援，AI 加持更智能
支援騰訊雲 ASR 及 Google Gemini 兩種辨識引擎，並可自訂優先順序自動切換。Gemini 引擎利用多模態 AI 能力，自動添加標點符號並移除語氣詞，讓輸出更乾淨。

## 功能特色

- **跨平台支援** - 支援 Windows、macOS、Linux
- **多引擎 ASR** - 支援騰訊雲 ASR 及 Google Gemini 多模態語音辨識
- **Gemini AI 增強** - 自動標點符號、移除語氣詞、支援多語言
- **自動 Fallback** - 設定優先順序，前一引擎失敗自動嘗試下一個
- **GUI 設置界面** - 友好的圖形設置窗口
- **快捷鍵觸發** - 按住 Ctrl 鍵即可開始錄音，放開自動識別並貼上
- **系統托盤運行** - 背景運行，不干擾日常工作流程
- **繁簡轉換** - 自動根據系統地區轉換中文繁簡體（Gemini 可指定輸出語言）
- **多語言 UI** - 支援繁體中文、简体中文、English 介面
- **開機自啟** - 支援系統開機自動啟動功能
- **並發錄音** - 在 ASR 處理期間可繼續錄音，結果按順序依次貼上

## 支援的 ASR 引擎

### Google Gemini（推薦）
- **gemini-2.5-flash** - 多模態 AI 語音辨識（推薦）
- **gemini-2.5-flash-lite** - 輕量版，速度更快
- 特色：自動標點符號、移除語氣詞、支援多語言
- 憑證：Google AI Studio API Key
- [取得 Gemini API Key](https://aistudio.google.com/apikey)

### 騰訊雲 ASR
| 引擎代碼 | 說明 |
|---------|------|
| `16k_zh` | 普通話（預設） |
| `16k_zh_video` | 普通話（視頻場景） |
| `16k_en` | 英文 |
| `16k_yue` | 粵語 |
| `16k_ca` | 川渝方言 |
- 憑證：騰訊雲 Secret ID / Secret Key
- [取得騰訊雲 API 憑證](https://console.cloud.tencent.com/cam/capi)

## 系統需求

- **Windows**: Windows 10/11
- **macOS**: macOS 10.15+ (Catalina 或更新版本)
- **Linux**: 主流發行版 (Ubuntu、Fedora 等)
- 麥克風設備
- 至少一種 ASR 引擎的 API 憑證

## 下載與安裝

### Windows 用戶

前往 [Releases 頁面](https://github.com/ascetic168/Voice_Input_Tray/releases) 下載最新版本：

雙擊安裝包完成安裝後，程式會自動啟動並在系統托盤顯示藍色麥克風圖示。

### macOS / Linux 用戶

目前需要自行編譯，請參考下方的「從原始碼編譯」章節。

### 取得 API 憑證

#### Google Gemini API Key（推薦）

1. 前往 [Google AI Studio](https://aistudio.google.com/)
2. 登入 Google 帳號
3. 點擊「Get API Key」取得金鑰

#### 騰訊雲 API 憑證

1. 前往 [騰訊雲官網](https://cloud.tencent.com/) 註冊帳號
2. 完成實名認證
3. 開通語音識別服務
4. 前往 [雲 API 密鑰控制台](https://console.cloud.tencent.com/cam/capi) 建立 Secret ID / Secret Key

> 💡 **提示**：如果不想進行中國大陸實名認證，可以使用 [騰訊雲國際版](https://www.tencentcloud.com/)，註冊流程更簡單。

### 設置 API 憑證

安裝完成後，右鍵點擊系統托盤中的藍色麥克風圖示，選擇「設置」，在設置窗口中輸入 API 憑證。

也可使用環境變數：

| 變數名稱 | 說明 |
|---------|------|
| `GEMINI_API_KEY` | Google Gemini API Key |
| `TENCENTCLOUD_SECRET_ID` | 騰訊雲 Secret ID |
| `TENCENTCLOUD_SECRET_KEY` | 騰訊雲 Secret Key |

```powershell
setx GEMINI_API_KEY "your_gemini_api_key"
setx TENCENTCLOUD_SECRET_ID "your_secret_id"
setx TENCENTCLOUD_SECRET_KEY "your_secret_key"
```

> **注意：** 設定環境變數後需要重新啟動程式才能生效。

## 使用方法

### 啟動程式

安裝後程式會自動啟動。手動啟動方式：

- **Windows**: 開始選單 → Voice Input Tray
- 或雙擊安裝目錄中的執行檔

程式啟動後會在系統托盤顯示藍色麥克風圖示。

### 語音輸入操作

1. 按住 **Ctrl** 鍵開始錄音（可立即說話）
2. 說話
3. 放開 **Ctrl** 鍵停止錄音
4. 識別完成的文字會自動貼上到焦點視窗

#### Ctrl 單鍵模式說明

- **按下 Ctrl** → 立即開始錄音（可同時開始說話）
- **在 2 秒內按其他鍵**（如 C、V）→ 自動取消錄音，不影響 Ctrl+C、Ctrl+V 等快捷鍵操作
- **超過 2 秒放開 Ctrl** → 進行語音識別

### 設置窗口

通過設置窗口可以配置：

- **Provider 優先順序** - 拖曳調整引擎優先順序，失敗自動 Fallback
- **API 憑證** - 各引擎的 API 憑證輸入
- **模型選擇** - 各引擎可選的模型
- **繁簡轉換** - 自動檢測、強制正體、不轉換
- **UI 語言** - 繁體中文、简体中文、English
- **熱鍵** - Ctrl、Ctrl+Win、Ctrl+Shift 等

## 開機自動啟動

### Windows

安裝包會自動創建開機自動啟動項。如需手動設置：

**方法一：使用設置窗口（推薦）**
1. 右鍵點擊托盤圖示，選擇「設置」
2. 在「系統設置」中勾選「系統開機時載入執行」
3. 點擊「保存設置」

**方法二：手動設置**
1. 按 `Win + R`，輸入 `shell:startup`
2. 將程式捷徑移動到開啟的資料夾

## 從原始碼編譯

### 開發環境需求

- Node.js 18+
- Rust 1.70+
- (Windows) Visual Studio C++ Build Tools
- (macOS) Xcode Command Line Tools
- (Linux) libwebkit2gtk-4.0-dev libssl-dev libgtk-3-dev libayatana-appindicator3-dev librsvg2-dev

### 編譯步驟

```bash
# 克隆專案
git clone https://github.com/ascetic168/Voice_Input_Tray.git
cd Voice_Input_Tray

# 安裝依賴
npm install

# 開發模式運行
npm run tauri:dev

# 構建發布版本
npm run tauri build
```

構建完成後，安裝包會在 `src-tauri/target/release/bundle/` 目錄中。

## 故障排除

**Q: 程式無法啟動？**
A: 請檢查 API 憑證是否正確設定。可通過設置窗口或環境變數設置。

**Q: 無法錄音？**
A: 請確認系統有可用的麥克風設備，且 Windows 設定 > 隱私權 > 麥克風已啟用。

**Q: Gemini 辨識結果不正確？**
A: 確認已設定正確的 API Key，並在設置中選擇 gemini-2.5-flash 模型。

**Q: 設定保存後重啟丟失？**
A: v0.2.3 已修復設定持久化問題，請更新至最新版本。

**Q: 如何查看詳細執行訊息？**
A: 啟動程式時加上 `--debug` 參數，debug log 會寫入 exe 同目錄的 `voice_input_debug.log`。

## 版本資訊

| 版本 | 發布日期 | 變更說明 |
|------|----------|----------|
| v0.2.3 | 2026-03-27 | 新增 Google Gemini 多模態語音辨識，修復設定持久化，修復 Provider 模型覆寫問題 |
| v0.2.2 | 2026-03-26 | 並發錄音支援，修復 Ctrl+V 衝突，優化連續錄音體驗 |
| v0.2.1 | 2026-03-25 | 修復視窗最大化狀態丟失問題 |
| v0.2.0 | 2026-03-24 | Tauri v2 跨平台版本，GUI 設置界面，開機自啟功能 |
| v0.1.0 | 2026-03-24 | Tauri v2 跨平台版本 |
| v0.0.2 | 2026-03-23 | 優化貼上延遲，新增引擎選單切換功能 |
| v0.0.1 | 2026-03-20 | 初始發布版本 |

## 授權

本軟體尚未開源，但可免費使用。
版權所有 © 2026 朱國棟 (Charlie Chu)。

未經授權，禁止複製、修改、散布或以任何形式使用本軟體及其相關文件。

---
**聯絡信箱**：charliechu1688@gmail.com
