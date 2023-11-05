# Batch VS Streaming
###### tags: `Data Engineering` `Streaming` `ETL`

## Batch 
確保了資料的精準度，且對於延遲 (Data Latency) 有一定包容度的場景。
### 應用特性:
- 最新資料、即時資料沒有迫切需求，但要求高度的資料正確性。
- 必須等待資料完整收集後才能處理情境
- 具體且反覆的執行條件(Daily , Hourly ...)

### 應用場景:
- 定期資料備份
- 中長期趨勢預測
- 較少異動的表格

## Streaming
資料在第一時間處理並使用，對於延遲 (Data Latency)不包容。
### 應用特性:
- 持續性的Trigger，且Trigger後立即反應。
- 紀錄每次觸發後執行的時間點。
- 需要訊息佇列(Message Quene)來保存因大量資料湧入造成的排隊現象。
- 資料量無法預期及不規律。
### 應用場景:
- 影音與串流媒體的資料處理
- 詐騙提醒與可疑刷卡通知
- 基於使用者行為的即時廣告或推薦
- 股市金融高頻交易

## Micro-Batch VS Streaming

有個 Batch Processing 為每秒就執行一次。那在極端條件的情形下，是否可以宣稱這個pipeline 就是一個 Streaming 的服務？ 差別在哪裡？

- 有可能是因為運算資源有限，或是有特別的業務考量，又或是有其他資料流造成只能使用 Batch 的瓶頸。

，Micro-Batch 也就是不想等太久，幾分鐘的資料延遲又不影響服務，那也許可以考慮這種架構。

雖然名稱當中有 Batch，但因為資料聚集的時間非常短，所以提供一種趨近於 Streaming 的感受。

範例: 

Spark Streaming 就是一種 Micro-Batch 的實現，雖名為 Streaming 但卻是由我們自行決定 Batch 的大小。

而這個數值大小正好體現了 Latency 與 Throughput 間的取捨。


而關於 Kafka Stream 的討論，有些人認為這才是真正的 Streaming，原因就是它是真的 record-by-record 的進行處理