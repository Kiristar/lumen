# Lumen 流光歌詞

在特斯拉車機瀏覽器上，即時顯示你 Spotify 正在播放的歌詞。單一 `index.html`，沒有後端。

## 功能

- 即時同步 Spotify 播放進度（本地時鐘插值，約每 3 秒校正一次）
- 逐字填色的卡拉 OK 效果；歌詞若有逐字時間軸（Enhanced LRC）會精準到每個字
- 依專輯封面取色的流動極光背景，每唱到新的一句會輕輕「呼吸」
- 間奏時顯示呼吸點點、雙語翻譯行、簡體歌詞自動轉繁體（臺灣用字）
- 點任一句歌詞直接跳到那裡；播放／暫停／上下首；歌詞時間 ±0.2 秒微調
- 手機掃 QR Code 登入，車上不用打字
- 經典／沉浸兩種版面、深色／淺色主題、四種字級；車機效能不足時自動切換流暢模式

## 部署（約 5 分鐘，只需做一次）

### 1. 放上 GitHub Pages

1. 在 GitHub 建立一個新的 **Public** repository，例如 `lumen`
2. 上傳 `index.html`
3. 到 **Settings → Pages**，Source 選 **Deploy from a branch**，Branch 選 `main`、資料夾選 `/ (root)`，按 Save
4. 約一分鐘後，網址會是 `https://<你的帳號>.github.io/lumen/`

### 2. 建立 Spotify App

1. 到 <https://developer.spotify.com/dashboard> 按 **Create app**（App 擁有者需要 Spotify Premium）
2. **Redirect URI** 填 `https://<你的帳號>.github.io/lumen/`，必須一字不差，**包含結尾的斜線**
3. **Which API/SDKs** 勾選 **Web API**，然後儲存
4. 在 App 的 Settings 頁面複製 **Client ID**

### 3. 在車上使用

1. 用特斯拉的瀏覽器打開你的網址
2. 用手機掃描畫面上的 QR Code → 貼上 Client ID → 用 Spotify 登入
3. 車上畫面會自動接上。之後再打開網址，就會直接顯示歌詞

## 小技巧

- **叫出控制列**：點畫面空白處
- **歌詞太快或太慢**：控制列左邊的 − / +，每次 0.2 秒，會記住設定
- **不想每次貼 Client ID**：把它填進 `index.html` 最上方的 `DEFAULT_CLIENT_ID`
- **用另一個 Spotify 帳號登入**：到 App 的 User Management 加入該帳號的 Email（開發模式最多 5 人）
- **先看效果**：網址後面加上 `#demo`

## 運作方式與隱私

- 全部在瀏覽器執行。Spotify 授權用 PKCE，token 只存在車上瀏覽器的 localStorage
- 手機配對透過 ntfy.sh 中繼；內容用 QR Code 裡的金鑰做 AES-GCM 加密，金鑰從未送到伺服器
- 歌詞來自 [LRCLIB](https://lrclib.net) 社群資料庫；找不到同步歌詞時會改顯示純文字歌詞或提示

## 已知限制

- 不是每首歌都有同步歌詞，冷門歌曲覆蓋率較低
- 同步時間由社群提供，個別歌曲可能有誤差，用時間微調校正即可
- Spotify 開發模式需要 App 擁有者持續訂閱 Premium
- 行車時請以安全為先；車機瀏覽器在行駛中的可用性依特斯拉軟體版本而定
