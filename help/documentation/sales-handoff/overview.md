---
title: Live Chat和Meeting預約概述
description: 瞭解Brand Concierge如何透過與可用代表的即時聊天或代表行事曆上的預約會議，將訪客交給人類。
role: User, Admin
level: Beginner
TQID: https://experienceleague.adobe.com/vfX6M2-ts7d2-AxKGjaP1Ygkk3FGSGRl4CHslcKYSXU
product_v2:
  - id: b6ee73fe-bdc6-47d9-99a2-80194514dd40
    internal-label: Brand Concierge
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: 4751ce408fb2aa6d1affae4dd7a5d81ca43ffc8a
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 0%
---
# Live Chat和會議預約總覽 {#overview}

門房可自行回答大多數問題。 某些對話需要人員：訂價交涉、採購問卷、示範請求。 Live Chat和Meeting Booking是Brand Concierge將交談傳遞給人的兩種方式，不會失去訪客已提供的內容。

* **即時聊天**&#x200B;會在相同的聊天視窗中，立即將訪客連線到可用的代表。
* **會議預訂**&#x200B;會從代表的行事曆提供訪客真正的開放位置，並預訂會議。

兩者皆由相同的技能提供，**[!UICONTROL 移交至銷售人員]**，且兩者都透過[!DNL Adobe Marketo Qualifier] （先前為[!DNL Sales Qualifier]）傳遞，代表可在此連線行事曆、設定其可用性，以及進行聊天。

## 移交的運作方式 {#how-it-works}

訪客與個人聯絡前，必須排列四個專案。

| 片段 | 作用 | 您的設定位置 |
| --- | --- | --- |
| 代表設定檔 | 連線行事曆並宣告代表何時可用於會議和聊天 | [!DNL Adobe Marketo Qualifier] > **[!UICONTROL 設定檔設定]** |
| 路由 | 決定&#x200B;*哪個*&#x200B;代表取得此訪客 | [!DNL Adobe Marketo Qualifier] > **[!UICONTROL 路由規則]**，以及每項整合的路由型別 |
| 整合 | **[!UICONTROL Meeting Booking]**&#x200B;與&#x200B;**[!UICONTROL 即時交談]**&#x200B;可讓服務人員檢查可用性、開始聊天以及預約時段 | 撰寫器> **[!UICONTROL 瀏覽整合]** |
| 技能 | 根據訪客的意圖，**[!UICONTROL 移交給銷售人員]**&#x200B;決定&#x200B;*何時*&#x200B;提供移交服務 | 撰寫者> **[!UICONTROL 瀏覽技能]** |

在執行階段：訪客說出了符合某項技能的&#x200B;**[!UICONTROL 使用時機]**&#x200B;條件，技能觸發，它會呼叫附加至它的整合專案，路由會解析代表，而訪客會獲得聊天、會議或兩者。

>[!NOTE]
>
>技能和整合是禮賓服務的一般建置組塊。 如需基礎模型，請參閱[技能與整合架構](../skills-and-integrations.md)。

## 訪客體驗 {#visitor-experience}

技能啟動時，服務生會說明選項，並在對話中顯示為按鈕。

![服務生回應提供移交，立即與專家聊天並安排會議按鈕](../assets/sales-handoff-visitor-1.png){width="800" zoomable="yes"}

### 即時交談 {#visitor-live-chat}

如果訪客選擇聊天，當路由找到可用的代表時，服務生會顯示連線狀態。

![在訪客選擇立即與專員聊天後，服務生顯示連線至專員狀態](../assets/sales-handoff-visitor-2.png){width="800" zoomable="yes"}

在代表加入之前，訪客會完成簡短的聊天前表單。 這些答案會隨著交談而移動，並在聊天收件匣中顯示為代表的&#x200B;**[!UICONTROL 表單詳細資料]**，因此訪客不必重複任何動作。

訪客可隨時結束聊天，並會要求確認。

![結束聊天確認對話方塊，要求訪客確認結束與專員的聊天](../assets/sales-handoff-visitor-4.png){width="800" zoomable="yes"}

### 會議預訂 {#visitor-meeting-booking}

如果訪客選擇預約會議，則接待人員會顯示在訪客自己的時區，包含路由代表行事曆上真正開啟的位置的行事曆。

![在對話中預約會議卡，顯示月份行事曆和可用時區清單](../assets/sales-handoff-visitor-3.png){width="800" zoomable="yes"}

訪客確認位置後，會傳送代表的確認電子郵件，選擇性地包括[!DNL Microsoft Teams]連結。 交談內容會傳送給收到邀請的代表。

## 開始前所需的專案 {#prerequisites}

* 存取[!DNL Adobe Marketo Qualifier]，您的代表已新增為[!DNL Adobe Admin Console]中的使用者。
* 至少有一個已連線行事曆的代表。 無法啟動&#x200B;**[!UICONTROL Meeting Booking]**&#x200B;整合，除非您有。
* 至少有一位代表已設定即時聊天可用性。 **[!UICONTROL 即時交談]**&#x200B;整合必須等到具備後才能啟用。
* 您可以在Composer中新增整合與技能的服務生。

>[!NOTE]
>
>Live Chat和會議預約不需要[!DNL Adobe Marketo Engage]。 如果沒有它，代表、會議和聊天資料會保留在[!DNL Adobe Marketo Qualifier]中。 有兩個專案確實需要[!DNL Marketo Engage]：建立在[!DNL Marketo]銷售機會和公司屬性的自訂路由規則，以及回寫至[!DNL Marketo]個人記錄的服務人員活動型別。

## 設定即時聊天和會議預訂 {#setup-path}

請依序處理這些專案。

1. [在Adobe Marketo Qualifier中設定代表](representative-setup.md) — 連線行事曆、定義確認電子郵件，並設定行事曆和即時聊天可用性。
1. [將交談路由給代表](routing-rules.md) — 選擇循環配置資源、直接代理程式或建立在[!DNL Marketo]屬性上的自訂規則。
1. [啟用Live Chat和會議預訂](configure-in-composer.md) — 連線兩個整合併啟用&#x200B;**[!UICONTROL 移交給銷售人員]**&#x200B;技能。
1. [聊天收件匣](chat-inbox.md) — 當聊天到達時，代表會做什麼，包括評分交談。
1. [Marketo Engage中的Brand Concierge資料](marketo-activities.md) — 回寫至[!DNL Marketo]的潛在客戶欄位和活動型別，以及如何在Smart Campaigns中使用它們。
1. [監視會議和即時聊天](monitor.md) — 預約清單和績效儀表板。

## 資料保留 {#retention}

即時聊天對話會保留30天。
