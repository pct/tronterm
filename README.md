# TronTerm

**為「活在 AI 工具裡」的開發者而生的 macOS 原生終端機。**
免費下載,Developer ID 簽章 + Apple 公證,打開就能用。

如果你整天泡在 Claude Code、Codex 或其他 AI CLI 裡,TronTerm 是為你打造的。它不打算
在功能上贏過 iTerm2,也不想取代 Ghostty —— 那是兩個優秀又成熟的終端機。TronTerm 是
**AI 座艙**:把 AI 當一等公民,而且長時間跑的 agent 不會因為你關了視窗就死掉。

## 安裝

**Homebrew(建議)**

```sh
brew install --cask pct/tap/tronterm
```

**直接下載** — 到 [Releases](https://github.com/pct/tronterm/releases/latest) 抓
`TronTerm-x.y.z.zip`,解壓後把 `TronTerm.app` 拖進「應用程式」。已經過 Apple 公證,
不會跳 Gatekeeper 警告。

需 macOS 13 (Ventura) 以上,Apple Silicon。

## AI 灌爆輸出也不會凍住

AI TUI 一秒重繪畫面上千次,ghostty / iTerm2 這時候會卡。TronTerm 的三道防線讓卡頓在
架構上不可能發生:

1. **背景解析** —— PTY 讀取與 VT 解析都在背景 queue,主執行緒只管輸入與繪圖。
2. **Frame coalescing** —— 解析即時消化所有輸出,渲染最多 60fps 只畫最新畫面。
3. **硬性資源上限** —— scrollback 封頂,記憶體有可計算的上界。

渲染只走 CoreText + NSView 這條系統成熟路徑,不碰自訂 GPU pipeline。

## 內建、而且廠商中立的 AI

其他加了 AI 的終端機都把你綁死在單一廠商、還要你自己貼 API key。TronTerm 不會。

- **⌘I — 自然語言 → 指令。** 描述你想做的事,AI 附上目前畫面、工作目錄與歷史當上下文,
  轉成 shell 指令填進輸入列 —— 你按 Enter 之前什麼都不會執行。
- **⌘E — 解釋畫面。** 問 AI 這個錯誤是什麼意思、該怎麼修。
- **你裝的每一家 AI,自動偵測。** 啟動時掃你的 PATH,把 `claude`、`codex`、`gemini`、
  `llm`、`ollama` 等已安裝的 CLI 全加進來,從 **AI ▸ 引擎** 選單一鍵秒切。不用貼
  API key、不綁 SDK、不被任何廠商綁架。
- **記憶留在本機。** 指令歷史與 AI 互動記在本地 SQLite(`~/.tronterm/tronterm.db`),
  一個位元組都不外流。

## 讓 agent 跑整晚 —— 關掉視窗它也不會死

內建的 `tt-daemon` 讓工作階段獨立於視窗存活。啟動一個 agent、關掉視窗,之後重開
TronTerm 再重新連接 —— shell 和你的 agent 都還在跑。不必安裝、也不必學 tmux。

## 同時也是一個真正好用的終端機

分割窗格、Quick Terminal(全域熱鍵下拉)、搜尋、滑鼠回報、prompt 標記與跳轉、
resize reflow、undercurl 波浪底線、24-bit 全彩、完整 CJK 與輸入法支援、可設定的配色
主題,以及乾淨的 iTerm 風格設定面板。介面支援 7 國語言。

## 隱私

TronTerm 在本機執行,不會把終端機內容傳回原廠。AI 功能呼叫的是你自己設定的命令列工具,
資料流向由你選的那家 AI 決定。

---

<sub>Copyright © 2026 1Tron System Co., Ltd. 本 repo 為發行與問題回報用途,原始碼未公開。</sub>
