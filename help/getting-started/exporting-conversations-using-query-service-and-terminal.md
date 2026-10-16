---
title: 使用查詢服務和終端機匯出交談
description: 瞭解如何使用Brand Concierge查詢服務和終端機，連同認證和個人資料的指引，將Experience Platform交談匯出為CSV。
topic: Development
role: Developer
level: Experienced
doc-type: Tutorial
duration: 260
last-substantial-update: 2026-10-15
jira: KT-22874
source-git-commit: 04c844e16a8fb13e54dfcbb29c776896674532b9
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%
---
# 使用查詢服務和終端機匯出交談

瞭解如何使用Adobe Experience Platform查詢服務和終端機儲存和匯出Adobe Brand Concierge交談。 此影片說明如何尋找資料集表格名稱、設定PostgreSQL命令列使用者端，以及將日期範圍的交談資料匯出至CSV檔案。

## 這部影片是給誰看的？

* 需要使用命令列工具匯出Brand Concierge交談資料的開發人員

## 視訊內容

* 在Experience Platform中尋找交談資料集並複製其表格名稱
* 安裝PostgreSQL使用者端與Homebrew，並設定其命令列路徑
* 從[查詢服務認證]索引標籤複製PSQL連線命令
* 選取資料集和日期範圍，然後將查詢結果匯出至本機CSV檔案
* 檢查匯出的結果，並在必要時重新整理過期的認證

>[!VIDEO](https://video.tv.adobe.com/v/3504652?captions=chi_hant)

```bash
psql "sslmode=require host=... password=..." --csv -o ~/brand-concierge-conversation-export/oct-1-2026-till-today-responses.csv -c "SELECT * FROM cja_brand_concierge_responses_dataset_b4c15126_bd9b_4d52_8151_26 WHERE timestamp >= TIMESTAMP '2026-10-01 00:00:00' AND timestamp <= NOW() ORDER BY timestamp ASC LIMIT 1000"
```

>[!IMPORTANT]
>
> PSQL connection指令包含即時密碼。 請勿將其共用或貼到聊天、AI代理程式或電子郵件中。 如果驗證在密碼過期後失敗，請從[查詢服務認證]索引標籤複製新的命令。

>[!NOTE]
>
> 匯出的交談可能包含個人識別資訊(PII)。 儲存CSV檔案時，請遵循您組織的資料處理原則。

如需相關檔案，請參閱[Brand Concierge說明](../documentation/overview.md)。

## 相關教學課程

* [使用Adobe CX Enterprise Coworker匯出交談](exporting-conversations-using-adobe-cx-enterprise-coworker.md)
