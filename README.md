# healthchecks

### 主機規格需求
* 主機：兩台 8G RAM，4vCPU，200GB Disk 主機
* 穩定
* 網路順暢

### 使用單位需準備項目

* 技術上，healthcheck 使用 HTTP GET 作為健康回報方式，在不同情境下可使用不同的方式回報。比如在 cronjob 可使用 curl 進行回報，PHP 中可使用 file_get_contents 作為回報。因此，確保網路能外連 `<healthcheck 平台網址>` 並有適當的 HTTP client 工具即可。在規劃回報方式時，建議[一併規劃 timeout 及 retry 機制](https://healthchecks.io/docs/reliability_tips/)，並考慮進行非同步回報，避免回報的 HTTP 請求阻礙使用流程的進行。
* 需求面，建議預先規劃「監測目的」，擬定「需要監測的項目」。比如若期望監測「關鍵使用路徑」順暢程度（這是比較複雜的監測情境），建議定義好各步驟（A -> B -> C），規劃每個步驟要如何插入非同步回報機制，規劃要如何[監測各步驟時間](https://healthchecks.io/docs/measuring_script_run_time/)等。
* 人力面，請先安排開發人力，以便進行有效的監測。需求確認後，開發時程視複雜程度而不同，但一般約在 1 個人月以內可完成。

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
