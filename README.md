# healthchecks

### 主機規格
* 主機：兩台 8G RAM，4vCPU，200GB Disk 主機
* 穩定
* 網路順暢

### 準備項目

* 技術上，healthcheck 使用 HTTP GET 作為健康回報方式，在不同情境下可使用不同的方式回報。比如在 cronjob 可使用 curl 進行回報，PHP 中可使用 file_get_contents 作為回報。因此，確保網路能外連 `<healthcheck 平台網址>` 並有適當的 HTTP client 工具即可。
* 管理上，建議預先規劃「需要監測的項目」，並且安排開發人力，以便進行有效的監測。需求確認後，開發時程約在 1 個人月以內。

### 範例使用情境：
* 監測某些 cronjobs 是否正確執行
* 監測某個工作執行多久
* 監測每個功能階段是否正常
* 監測某個網站頁面是否能正常存取
* 監測是否有正確收到 email
* 監測 build、部署等步驟是否正確執行
* 引用 healthchecks 的 badge 在頁面上呈現服務健康狀態

### 通知方式：
* email
* 即時通訊
* 簡訊
* 電話語音
* 其它（支援以 API 串接）
