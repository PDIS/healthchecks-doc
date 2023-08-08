# healthchecks

### 主機規格需求
* 主機：一台 LB （或使用 LB 服務替代），至少三台 8G RAM，4vCPU，200GB Disk 主機。
* 穩定
* 網路順暢

### 使用單位需準備項目

* 技術上，healthcheck 使用 HTTP GET 作為健康回報方式，在不同情境下可使用不同的方式回報。比如在 cronjob 可使用 curl 進行回報，在 C#.NET 中[使用 System.Net.Http.HttpClient 回報](https://healthchecks.io/docs/csharp/)。因此，確保網路能外連 `<healthcheck 平台網址>` 並有適當的 HTTP client 工具即可。在規劃回報方式時，建議[一併規劃 timeout 及 retry 機制](https://healthchecks.io/docs/reliability_tips/)，並考慮進行非同步回報，避免回報的 HTTP 請求阻礙使用流程的進行。
* 需求面，建議預先規劃「監測目的」，擬定「需要監測的項目」。比如若期望監測「關鍵使用路徑」順暢程度（這是比較複雜的監測情境），建議定義好各步驟（A -> B -> C），規劃每個步驟要如何插入非同步回報機制，規劃要如何[監測各步驟時間](https://healthchecks.io/docs/measuring_script_run_time/)等。
* 人力面，請預先安排開發、部署人力。需求確認後，開發時程視複雜程度而不同，簡易的監測機制約可在 1 個人月以內開發、部署完成，複雜的監測情境則需個別評估。

### 範例使用情境：
* 監測某些 cronjobs 是否正確執行（[說明](https://healthchecks.io/docs/monitoring_cron_jobs/)）
* 監測某個工作執行多久（[說明](https://healthchecks.io/docs/measuring_script_run_time/)）
* 監測每個功能階段是否正常
* 監測某個網站頁面是否能正常存取
* 監測是否有正確收到 email
* 監測 build、部署等步驟是否正確執行
* 引用 healthchecks 的 badge 在頁面上呈現服務健康狀態（[說明](https://healthchecks.io/docs/badges/)）

### 通知方式：
* email
* 即時通訊
* 簡訊
* 電話語音
* 其它（支援以 API 串接）

### FAQ
* 多久回報一次資料？
  * 視使用情境及 SLO (Service-Level Objective) 而定
* 回報的資料中，是否含有機敏資料？
  * 沒有。回報僅是一個抽象的事件，代表某個預先定義的 [Check](https://healthchecks.io/docs/configuring_checks/) 在某一時間點有回報的事件發生，無其它資料。但對於嚴格禁止外連的主機，為了避免網路連線增加額外的風險，可（非同步地，比如經由監聽 log server 的特定 log）透過專屬的外連主機進行回報。 
* 如何移除？
  * 無論未來是否有移除的需求，我們均建議在回報機制的程式中，加上[開關機制](https://en.wikipedia.org/wiki/Feature_toggle)，讓回報可以被簡單地啟用及關閉。
