# 🦞 OpenClaw (Moltbot) 雲端佈署與啟動指南

本文件旨在提供一個詳盡的指南，協助您在 **GitHub Codespaces** 上快速部署並啟動您的個人 AI 助理 **OpenClaw**（原名 Moltbot）。透過 Codespaces，您可以實現**免本地環境、免複雜設定**的雲端運行體驗，非常適合初次嘗試或尋求便捷部署方案的使用者。

---

## 一、 Codespaces 快速啟動

GitHub Codespaces 提供了一個強大的雲端開發環境，它已預先配置好運行 OpenClaw 所需的 Node.js 環境，並自動處理了依賴安裝。

| 步驟 | 說明 |
| :--- | :--- |
| **1. 前往儲存庫** | 點擊此連結前往您的專屬儲存庫：[https://github.com/111534106/hahahahah](https://github.com/111534106/hahahahah) |
| **2. 啟動 Codespace** | 點擊頁面上的綠色 **`< > Code`** 按鈕，選擇 **`Codespaces`** 分頁，然後點擊 **`Create codespace on main`**。 |
| **3. 環境準備** | Codespaces 將自動建立一個虛擬機，並執行以下初始化操作：<br> - 安裝 Node.js 22+。<br> - 自動解壓縮 `moltbot_light.zip` 原始碼。<br> - 安裝所有專案依賴 (`pnpm install`)。 |
| **4. 進入環境** | 整個過程可能需要幾分鐘。完成後，您將看到一個完整的 VS Code 介面，這就是您的雲端運行環境。 |

## 二、 配置與啟動 OpenClaw Gateway

OpenClaw 是一個依賴大型語言模型 (LLM) 的應用程式。您需要提供一個 API Key 才能使其運作。我們建議使用 **Anthropic Claude** 或 **OpenAI GPT**。

### 1. 配置 API Key

在 Codespace 內建的終端機中，執行以下指令來設定您的 API Key。

```bash
# 範例：設定 Anthropic API Key (建議使用，因為 OpenClaw 最初是為 Claude 設計)
export ANTHROPIC_API_KEY="您的 Anthropic API Key"

# 範例：設定 OpenAI API Key (可選)
export OPENAI_API_KEY="您的 OpenAI API Key"
```

> **重要提示**：請將 `您的 Anthropic API Key` 替換為您實際的密鑰。

### 2. 建立配置檔

接著，使用以下指令將您的 API Key 寫入 OpenClaw 的配置檔 `config.yaml`：

```bash
echo "models.anthropic.apiKey: \"$ANTHROPIC_API_KEY\"" > config.yaml
echo "models.openai.apiKey: \"$OPENAI_API_KEY\"" >> config.yaml
```

### 3. 啟動 Gateway

在終端機中，執行初始化指令：

```bash
pnpm openclaw onboard
```

此指令將引導您完成 OpenClaw 的初始設定。

> **提示**：如果 Codespace 提示您端口 `18789` 已轉發，請點擊 **`Open in Browser`** 即可存取 **Control UI** 介面，並在該介面中完成 **Device Pairing** 和 **Channel Setup**（例如 Telegram, Discord, 或 WebChat）。

## 三、 進階：GitHub Actions 運行

我們已在儲存庫中配置了一個 GitHub Actions 工作流 (`.github/workflows/run_moltbot.yml`)。

**請注意**：GitHub Actions 主要用於自動化測試或短暫任務，**不適合運行 24/7 的常駐服務**。

1.  **前往 Actions 分頁**：在您的儲存庫中，點擊 **`Actions`**。
2.  **選擇工作流**：在左側欄中選擇 **`Run OpenClaw (Moltbot)`**。
3.  **手動運行**：點擊 **`Run workflow`** 按鈕，並在彈出的對話框中填入您的 `ANTHROPIC_API_KEY`。
4.  **查看結果**：您可以在工作流運行日誌中看到 OpenClaw 的啟動輸出。

**結論**：若您追求持續運行和互動式操作，**Codespaces 是最佳選擇**。若僅需短暫測試，可使用 GitHub Actions。

---

## 參考資料

[1] [GitHub Codespaces 官方文件](https://docs.github.com/zh/codespaces)
[2] [OpenClaw (Moltbot) 官方儲存庫](https://github.com/openclaw/openclaw)
[3] [Anthropic Claude API 文件](https://docs.anthropic.com/claude/reference/getting-started)
[4] [OpenAI API 文件](https://platform.openai.com/docs/quickstart)
