# Core — Agent System Prompts（執行環境核心）

本目錄是 **Personal AI Operations Hub** 的系統設定核心，承載 Agent 的「身體設定檔」。檔案分為兩個層級，遵循 **原始碼（Source）vs 執行檔（Binary）** 的分離原則。

---

## 檔案總覽

| 檔案 | 行數 | 用途 | 讀取時機 |
|---|---:|---|---|
| `AGENTS.md` | 113 | 完整版 — 全域 Agent 行為準則（第一性原理 + 決策脈絡） | 維護 / 重設計時 |
| `AGENTS_tiny.md` | 22 | 精簡版 — 給 Agent 直接載入的執行檔 | **執行環境** |
| `CLAUDE.md` | 146 | 完整版 — Claude Code CLI 專屬工程紀律與協作規範 | 維護 / 重設計時 |
| `CLAUDE_tiny.md` | 42 | 精簡版 — 給 Claude Code 載入的護欄與協定 | **執行環境** |
| `SOUL.md` | 201 | 完整版 — 使用者身份、價值觀與長期策略（北極星） | 維護 / 哲學重定義時 |
| `SOUL_tiny.md` | 23 | 精簡版 — 給 Agent 載入的角色與通訊風格 | **執行環境** |
| `PRINCIPLES.md` | 1 | 核心工程哲學一覽（持久保留） | 隨時可參考 |
| `README.md` | — | 本檔 | — |

---

## 使用原則

### 1. 執行環境（Runtime）— 只用 `*_tiny.md`

日常 Agent 啟動時，僅載入 `_tiny` 版本。

理由：

- **Token 效率與 KV Cache**：精簡的 System Prompt 降低 TTFT，釋放 Context Window 給真正的任務內容（架構手冊、程式碼、對話）。
- **注意力集中**：高密度條列護欄（Constraints、Environment Checks）強制模型聚焦於邊界防護與執行紀律，降低幻覺與越權風險。
- **邏輯無損**：`_tiny` 已繼承所有關鍵護欄（禁用破壞性 Git、強制硬體驗證、系統化除錯、記憶萃取），未犧牲工程邊界。

> 部署時請去掉 `_tiny` 後綴後再放到對應位置：
> - `~/.claude/CLAUDE.md` ← `CLAUDE_tiny.md`
> - `~/.hermes/AGENTS.md` ← `AGENTS_tiny.md`
> - `~/.hermes/SOUL.md` ← `SOUL_tiny.md`

### 2. 知識庫與文檔（Repository/Docs）— 封存完整版

完整版是 **原始碼母版（Source of Truth）**，角色為靜態歸檔：

- **保留第一性原理與決策脈絡**：當轉移至新模型、重定義工程哲學、或追溯歷史設計動機時，完整版是不可或缺的參考依據。
- **不可刪除、不可就地運行**：完整版不應被任何 Agent 當作 Runtime 設定載入；它僅供人類閱讀與版本控制。
- **建議同步歸檔至**：`/docs/AI_OS_Architecture/`，與架構筆記、決策記錄（ADR）並列。

### 3. 維護流程

當你需要調整護欄或行為準則時：

1. 先修改完整版（`AGENTS.md` / `CLAUDE.md` / `SOUL.md`），保留動機與脈絡。
2. 再同步精簡版（`*_tiny.md`），確保兩者一致。
3. 提交時一次 commit，訊息說明動機（例如：「tighten git safety guard」）。
4. 同步歸檔至 `/docs/AI_OS_Architecture/`。

> 永遠從完整版 → 精簡版單向同步，避免精簡版「漂移」成無人理解的謎樣設定。

---

## 設計取捨摘要

| 面向 | 完整版 | 精簡版 |
|---|---|---|
| Token 成本 | 高 | **低** |
| 首次推論延遲（TTFT） | 較高 | **最低** |
| 注意力分散風險 | 中（敘述多） | **低（條列聚焦）** |
| 決策脈絡可追溯性 | **完整保留** | 不可考 |
| 適用情境 | 維護 / 重設計 / 入庫 | **日常執行** |
| 部署位置 | `/docs/`、`/core/` 歸檔 | Agent 配置目錄（Runtime） |

---

## 版本歷史

- 2026-07-10：建立 `*_tiny.md` 三檔，採用 Source / Binary 分離策略。
- 2026-07-10：`SOUL.md` 重寫為正式個人系統提示。

---

維護者：verygoodman  
核心理念：科學、理性、客觀、邏輯、工程。
