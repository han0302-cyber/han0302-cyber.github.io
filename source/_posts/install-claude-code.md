---
title: 06 安裝 Claude Code｜讓 AI 進入你的知識庫
date: 2026-07-07 09:00:00
tags:
  - AI課程
  - 安裝教學
  - Claude-Code
categories:
  - AI x Obsidian 系列
---

作者｜有澤法律事務所 林廷翰律師

> **💡 本篇重點**
> 安裝一行指令、啟動打一個字 `claude`。核心觀念只有一個——**在哪個資料夾啟動，AI 的主場就是哪個資料夾**。所以要在 Obsidian Vault 裡啟動它。


<!-- more -->
本篇是純操作指南，前提是你已依 [Obsidian 入門｜安裝、Vault 與基本操作](/posts/obsidian-basics/) 建好 Vault。全程約二十分鐘。

## 事前準備：帳號

Claude Code 需要 **Claude 付費方案**（Pro、Max、Team 或 Enterprise）或 API 帳號，**免費帳號無法使用**。個人入門選 Pro 即可；資安考量與方案選擇的關係（消費者方案 vs 商用方案的資料條款差異），詳見 [資安與倫理｜律師使用 AI Agent 的紅線](/posts/security-ethics-red-lines/)，建議在放入真實資料前先讀過。

另外先說明版本：Claude Code 有**終端機版（CLI）**與**桌面版**（Mac／Windows 應用程式）兩種介面，引擎與帳號相同（見 [什麼是終端機 AI Agent｜認識 Claude Code 與 Codex](/posts/terminal-ai-agent/) 的介面比較）。本篇安裝的是終端機版——功能最完整，也是本系列所有示範的基準；偏好圖形介面者可從官網下載桌面版，之後各篇的提示詞照用，僅操作介面不同。

> **💡 小提示**
> Codex 使用者：需要 ChatGPT 付費方案或 OpenAI API，安裝指令與細節以 OpenAI 官方文件為準；本篇之後的觀念完全通用。

### 模型與額度：導入前該懂的兩件事

- **模型分級**：Claude Code 可用 `/model` 指令切換模型——旗艦模型推理最強、消耗額度也最快；中階模型處理日常整理任務通常已足夠。心法：**批次整理用中階、關鍵法律分析用旗艦**。
- **額度上限**：訂閱方案有用量上限（按時段輪替計算），大量編纂判決時可能撞到，稍等即恢復。重度使用者可升級較高方案，或改用 API 依用量計費。建議：先用基本付費方案試跑一個月，依實際用量再決定要不要升級——這跟採購任何事務所軟體的評估邏輯相同。

> **💡 用狀態列顯示額度與容量**
> Claude Code 支援自訂「狀態列」——畫面底部常駐一行資訊，可顯示目前使用的模型、**對話容量水位**與**額度剩餘**，就像開車時的油表與時速表。輸入 `/statusline` 請 AI 幫忙生成一個即可，不必自己寫。看得到水位，後面幾篇談的「容量管理」才有依據。

## 步驟一：打開終端機（2 分鐘）

- **Mac**：`Cmd + 空白鍵` 打開 Spotlight，輸入「Terminal」（終端機），Enter。
- **Windows**：開始選單搜尋「PowerShell」，開啟。

黑（或白）底的文字視窗出現了。接下來你只需要打幾行東西，而且以後跟 AI 的互動都是中文。

## 步驟二：安裝與登入（10 分鐘）

### 2-1 安裝

依官方文件（[code.claude.com/docs](https://code.claude.com/docs)）目前推薦的安裝方式：

**Mac / Linux（擇一）：**
```bash
curl -fsSL https://claude.ai/install.sh | bash
```
或使用 Homebrew：`brew install --cask claude-code`

**Windows（PowerShell，擇一）：**
```powershell
irm https://claude.ai/install.ps1 | iex
```
或使用 WinGet：`winget install Anthropic.ClaudeCode`

安裝方式可能隨版本更新（例如早期常見的 npm 安裝法已不再是官方首推），若指令失效，以官方文件為準——或直接問任何一個 AI「Claude Code 現在怎麼安裝」。

### 2-2 啟動與登入

```bash
claude
```

第一次啟動會開啟瀏覽器引導登入，用你的 Claude 帳號授權即可。看到對話提示符出現，安裝就完成了。輸入 `/exit` 或按 `Ctrl+C` 可隨時離開。

## 步驟三：進入你的 Vault（5 分鐘）

關鍵觀念：**Claude Code 的工作範圍，以「你啟動它時所在的資料夾」為主場。** 所以要先切換到 Vault 再啟動。

### 3-1 切換資料夾

```bash
cd ~/Documents/LawVault
```

> **💡 小提示**
> 省力技巧：打 `cd `（後面留一個空格），把 Vault 資料夾從 Finder／檔案總管**直接拖進終端機視窗**，路徑自動貼上，Enter。

「cd 進 Vault、再打 claude」這兩步，日後可以合併成一個自訂指令——見本篇文末的「進階設定：把啟動流程縮成一個指令」，建議先把本篇主流程走完再回頭設定。

補充兩點，之後會用到：

- 主場之外的檔案並非碰不到——你在對話中**給它其他資料夾的路徑**（同樣可以用拖曳的），經你按下同意後，它就能讀取。例如在 Vault 裡工作時，臨時要它讀「下載」資料夾裡剛拿到的檔案，貼路徑即可。
- 常用的額外資料夾，可以用 `/add-dir` 指令正式加入本次工作範圍。

### 3-2 啟動並下達第一個任務

```bash
claude
```

然後用中文打下第一個任務：

```
你好，這是我的 Obsidian 知識庫。請看一下目前的資料夾結構，
然後幫我建立一則名為「歡迎使用」的筆記，
內容說明這個知識庫未來的用途：法律知識管理。
```

它會先請求你的同意（按 Enter 允許），然後動手建立檔案。切回 Obsidian——筆記已經出現了。

後面所有進階應用，本質上都是這個動作的放大。

### 3-3 認識權限確認

Claude Code 預設在**寫入檔案、執行指令**前都會逐次徵求同意（單純讀取檔案不會問）——這是安全設計，不是故障。日常使用的授權模式有三種，按 `Shift+Tab` 循環切換，可以用「帶助理的三個階段」來理解：

| 模式 | 相當於 | 適合 |
| --- | --- | --- |
| **手動（Manual，預設）** | 新進助理：每個動作都送核 | 初學階段，順便看懂 AI 都在做什麼 |
| **自動修改（Accept Edits）** | 信任的助理：工作資料夾內的檔案修改放手做，其餘指令仍送核 | 上手之後的日常，效率與安全兼顧 |
| **計畫（Plan）** | 先交辦案計畫，核可後才動卷 | 大工程（詳見 [從檢索到編纂｜讓知識庫自己長大](/posts/from-retrieval-to-compilation/)） |

另外還有一種「**全放行（Bypass Permissions）**」——什麼都不問、全部照做。它刻意**不在** `Shift+Tab` 的循環裡，必須用特殊參數啟動才會出現，官方文件也把它定位為隔離環境（容器、虛擬機）專用。⚠️ 律師在放著真實資料的電腦上，別碰這個模式。（模式的名稱與種類隨版本更新略有調整，例如官方也在實驗更聰明的自動授權模式，以你畫面上實際顯示的為準。）

建議路徑：第一週用手動模式，把每次確認當成「看懂 AI 想做什麼」的練習；熟練後切到自動修改模式；細部放行規則可用 `/permissions` 調整（例如把某些安全的唯讀指令設為免詢問）。原則不變：**寧可多按幾次 Enter，也不要一開始就全部放行。**

## 步驟四：第一批練習任務（當天就能試）

從司法院裁判書系統複製 2–3 則與工程承攬工期遲延、違約金酌減相關的**公開判決**——這也是在為主案例 2026-015 的研究鋪底——在 Obsidian 各存成一則筆記，然後：

> **💡 省下複製貼上：司法院裁判書閱讀助手**
> 筆者自行開發的免費 Chrome 擴充功能「**司法院裁判書閱讀助手**」（[Chrome 線上應用程式商店](https://chromewebstore.google.com/detail/nigjaldhpljkcgedolepmhmifaplpadn)｜[GitHub 原始碼](https://github.com/han0302-cyber/judicial-outline-extension/)），可以在司法院法學資料檢索系統**一鍵複製判決全文，或直接把整份裁判書下載成 `.md` 檔**，存進 Vault 就是 Obsidian 能用的格式。這個練習用手動複製即可完成；之後要批次建判決知識庫（見 [實戰｜打造判決知識庫：從裁判書到 WIKI 索引](/posts/judgment-knowledge-base/)），它會省下大量時間。順帶一提：這個擴充功能本身就是用 Claude Code 開發的。

```
請閱讀 Vault 裡的判決筆記，為每一份在開頭加上「## 摘要」段落，
包含：判決字號、法院、案由、主要爭點、法院見解，各一到兩句話。
```

再試一個進階的：

```
請根據這幾則判決的共同主題建立一則主題筆記，
整理它們在主要爭點上的異同，並以 [[wikilink]] 連結到各判決筆記。
```

切回 Obsidian 打開知識圖譜——筆記已連成一張小網。

## 進階設定：把啟動流程縮成一個指令

每天啟動的固定動作是兩步：「cd 進 Vault、再打 claude」。這兩步可以合併成一個自訂的短指令，術語叫**別名（alias）**。設定一次之後，輸入 `law` 三個字母，即完成切換資料夾並啟動 Claude Code。

以下指令中的 `＜Vault路徑＞` 要換成**你自己的** Vault 完整路徑——取得方式就用步驟三的拖曳技巧：把 Vault 資料夾拖進終端機，路徑就出現了，複製起來備用。

### Mac：終端機執行一次

```bash
echo "alias law='cd ＜Vault路徑＞ && claude'" >> ~/.zshrc && source ~/.zshrc
```

這行指令的層次：定義 `law` ＝「切換到 Vault、成功後啟動 `claude`」，把這條定義追加寫入終端機每次開啟都會自動讀取的個人設定檔（`~/.zshrc`），再立刻重讀設定檔讓它馬上生效。

### Windows：PowerShell 執行一次

PowerShell 的別名不能帶動作，等效做法是在設定檔裡加一個小函式：

```powershell
if (!(Test-Path $PROFILE)) { New-Item -Type File -Path $PROFILE -Force }
Add-Content $PROFILE 'function law { Set-Location "＜Vault路徑＞"; claude }'
. $PROFILE
```

邏輯與 Mac 相同：把 `law` 函式寫進 PowerShell 的個人設定檔（`$PROFILE`，地位等同 `.zshrc`），再重讀生效；設定檔不存在時，第一行會先建立它。

若日後開新視窗出現「無法載入設定檔」的紅字，是 Windows 預設的指令碼執行原則擋住了，執行一次 `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` 即可解除。

### 變化款：不綁路徑的就地啟動

`law` 固定切換到 Vault 再啟動；但有時你已經在別的資料夾（例如先 `cd` 進了某個案件資料夾），希望直接在該處啟動。`claude` 這個指令本身就是「在目前所在的資料夾啟動」，不綁任何路徑。所以這個變化款只是把六個字母縮短成純縮寫（以 `cc` 為例，縮寫可自訂）：

**Mac**：

```bash
echo "alias cc='claude'" >> ~/.zshrc && source ~/.zshrc
```

**Windows**（PowerShell；這種「單純改名」的縮寫用 `Set-Alias` 就夠，不需要函式）：

```powershell
Add-Content $PROFILE 'Set-Alias cc claude'
. $PROFILE
```

兩個縮寫可以並存，分工明確：**`law` 不論目前位置，一律切換到 Vault 後啟動；`cc` 則在目前所在的資料夾就地啟動**——處理知識庫用前者，已在某個案件資料夾工作時用後者。

看懂結構之後，其實不必手打：對 AI 說「我的 Vault 在＜路徑＞，我用 Mac／Windows，請給我設定 law 與 cc 兩個啟動別名的完整指令」，讓它代入路徑生成，貼上執行即可。

## 常見問題排除

| 狀況 | 解法 |
| --- | --- |
| 終端機說找不到 `claude` 指令 | 關掉終端機重開；仍不行則重跑安裝指令 |
| 頻繁詢問是否允許，覺得繁瑣 | 正常的安全設計，初期建議保留；熟練後用 `/permissions` 調整 |
| 想知道 AI 剛剛做了什麼 | 直接問它「請列出你剛剛做的所有變更」 |
| 回應到一半想打斷 | 按 `Esc` |
| 想開新話題 | 輸入 `/clear` 清空對話（檔案不受影響） |
| 對話很長，想回找 AI 剛剛說過的內容 | 按 `Ctrl+O` 叫出對話工具，可搜尋、匯出整段對話 |

## 小結

- 需求：付費方案帳號；安裝一行指令；啟動打 `claude`。
- 鐵則：先 `cd` 進 Vault 再啟動；主場外的資料給路徑（或 `/add-dir`）即可參照。
- 權限確認是護欄：初期逐次同意，理解它在做什麼。
- 進階：設定 `law`（切換至 Vault 後啟動）與 `cc`（就地啟動）兩個別名，啟動只需一個指令。
- 下一篇：寫一份讓 AI「一次到位」的到職須知——CLAUDE.md。

## 參考資料

- [Claude Code 官方文件：Quickstart](https://code.claude.com/docs/en/quickstart)
- [Claude Code 官方文件：安裝與設定（Setup）](https://code.claude.com/docs/en/setup)
- [Claude Code 官方文件：權限（Permissions）](https://code.claude.com/docs/en/permissions)
- [Claude Code 官方文件：授權模式（Permission modes）](https://code.claude.com/docs/en/permission-modes)
- [Claude Code 官方文件：狀態列（Status line）](https://code.claude.com/docs/en/statusline)

---

⬅️ 上一篇：[什麼是終端機 AI Agent｜認識 Claude Code 與 Codex](/posts/terminal-ai-agent/)
➡️ 下一篇：[CLAUDE.md｜寫給 AI 助理的到職須知](/posts/claude-md-onboarding/)
🏠 回到 [總覽｜AI x Obsidian 律師實戰系列](/posts/series-overview/)
