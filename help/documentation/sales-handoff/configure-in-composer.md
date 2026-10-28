---
title: 啟動Live Chat和會議預訂
description: 在Composer中連結Live Chat和Meeting Booking整合，然後啟用銷售技能的移交，讓您的服務人員知道何時提供人力。
role: User, Admin
level: Beginner
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
source-git-commit: 91cbec8d6f4e4800e3bdc8c8f60bfe9ed168a963
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%
---
# 啟動即時聊天和會議預訂 {#configure-in-composer}

Composer中必須具備兩項功能。 **[!UICONTROL Meeting Booking]**&#x200B;與&#x200B;**[!UICONTROL Live Chat]**&#x200B;整合讓服務人員&#x200B;*能夠*&#x200B;檢查使用狀態、開始聊天以及預約時段。 **[!UICONTROL 移交銷售人員]**&#x200B;技能會告訴它&#x200B;*何時*&#x200B;使用該能力。

>[!NOTE]
>
>先完成[在Adobe Marketo Qualifier](representative-setup.md)中設定代表。 整合會檢查已連線的行事曆和即時聊天可用性，如果沒有這些行事曆，將無法啟用。

## 連線會議預約整合 {#connect-meeting-booking}

1. 在Composer中，開啟您的服務生，然後選取&#x200B;**[!UICONTROL 整合]** > **[!UICONTROL 瀏覽整合]**。

   **[!UICONTROL 會議預訂]**&#x200B;和&#x200B;**[!UICONTROL 即時交談]**&#x200B;出現在&#x200B;**[!UICONTROL 內建整合]**&#x200B;下。

   ![在Composer中瀏覽整合面板，在內建整合下顯示Live Chat和Meeting Booking卡片](../assets/sales-handoff-composer-1.png){width="800" zoomable="yes"}

1. 選取&#x200B;**[!UICONTROL 會議預訂]**，然後選取&#x200B;**[!UICONTROL 設定]**。

1. 輸入名稱和說明。

   為整合命名，以取得它在服務人員中的功能，例如`Meeting booking - US region`或`Meeting booking - round robin`。 您可以連線多個專案，名稱就是您稍後區分它們的方法。

1. 檢查行事曆連線狀態。

   整合會驗證貴組織中至少有一位代表已連線行事曆。

   * 如果沒有，錯誤會告訴您至少先連線一個行事曆，才能啟動會議預訂。 返回[!DNL Adobe Marketo Qualifier]並完成[連線您的行事曆](representative-setup.md#connect)。
   * 如果至少有一位代表出席，則會顯示有代表出席。

1. 選取路由型別： **[!UICONTROL 循環配置資源]**、**[!UICONTROL 直接代理程式]**&#x200B;或&#x200B;**[!UICONTROL 自訂路由]**。

   如果您選取&#x200B;**[!UICONTROL 直接代理程式]**，請選擇透過此服務生預約的每次會議的接收代表。 如果您選取&#x200B;**[!UICONTROL 自訂路由]**，則會套用您在[!DNL Adobe Marketo Qualifier]中建立的路由規則。 如需每個行為的詳細資訊，請參閱[將交談路由給代表](routing-rules.md)。

1. 選取&#x200B;**[!UICONTROL 連線]**。

## 連線即時聊天整合 {#connect-live-chat}

1. 在&#x200B;**[!UICONTROL 瀏覽整合]**&#x200B;中，選取&#x200B;**[!UICONTROL 即時交談]**，然後選取&#x200B;**[!UICONTROL 設定]**。

1. 輸入名稱和說明，例如`Live chat - round robin`。

1. 檢查即時聊天可用性狀態。

   整合會驗證至少有一位代表已設定即時聊天可用性。

   * 如果沒有，則會出現一則訊息，告訴您新增已設定其即時聊天可用性的代表。 返回[!DNL Adobe Marketo Qualifier]並完成[設定即時聊天可用性](representative-setup.md#chat-availability)。
   * 如果至少有一位代表出席，則會顯示有代表出席。

1. 選取製程型別。

   即時聊天支援與會議預約相同的三種路由型別。 透過&#x200B;**[!UICONTROL 循環配置資源]**，每個符合資格的代表都會立即收到通知，而且第一個接受的人會開始聊天。

1. 選取&#x200B;**[!UICONTROL 連線]**。

## 啟用銷售技能的移交 {#activate-skill}

整合現在已連線，但門房仍需知道何時提供。 這是技能的工作。

1. 在Composer中，選取&#x200B;**[!UICONTROL 技能]** > **[!UICONTROL 瀏覽技能]**，然後選取&#x200B;**[!UICONTROL 移交給銷售人員]**。

   詳細資料面板會顯示技能說明、其&#x200B;**[!UICONTROL 使用時機]**&#x200B;條件、建議的&#x200B;**[!UICONTROL 整合]**&#x200B;以及&#x200B;**[!UICONTROL 技能指示]**。

   ![瀏覽技能面板，已選取銷售技能的移交，顯示[使用時機]條件、建議的整合和技能指示](../assets/sales-handoff-composer-2.png){width="800" zoomable="yes"}

1. 選取&#x200B;**[!UICONTROL 修改]**。

   ![在修改模式中移交銷售技能，可編輯技能名稱、說明和使用條件](../assets/sales-handoff-composer-3.png){width="800" zoomable="yes"}

1. 檢閱技能名稱和說明，並視需要加以編輯。

1. 檢閱&#x200B;**[!UICONTROL Use when]**&#x200B;條件。

   這些是觸發移交的意圖。 此技能隨預設集提供：

   | 條件 | 觸發器於 |
   | --- | --- |
   | 顧問存取權 | 預約或排程會議、開始即時聊天，或要求與公司代表聯絡 |
   | 銷售與採購 | 定價、報價、折扣、採購協助或企業授權 |
   | 競爭比較 | 將您的解決方案與競爭對手的替代方案、差異或來自競爭對手平台的遷移進行比較 |
   | 試用和POC存取 | 試用設定、遊樂場存取、概念驗證或試行方案 |
   | 合約與授權變更 | 合約續約、期限延長或計畫升級 |
   | 採購RFP或RFI | RFP或RFI提交與回覆、廠商問卷、採購表單或法規遵循檔案 |
   | 示範 | 產品示範或逐步說明 |

   選取&#x200B;**[!UICONTROL 新增條件]**&#x200B;以新增您自己的目的，或刪除任何不適用於您企業的條件。

1. 新增您連線的整合。

   根據您想要此禮賓人員提供的內容，新增&#x200B;**[!UICONTROL 即時交談]**、**[!UICONTROL 會議預訂]**&#x200B;或兩者。

1. 檢閱&#x200B;**[!UICONTROL 技能指示]**。

   系統會根據您選取的條件和整合為您產生指示，因此多數情況下不需要編輯。

   當您想要更精細地控制哪些意圖會導致哪個選項時，請以純語言編輯它們。 例如，您可以指示服務生提供訂價問題的即時交談、提供示範要求的會議，以及提供採購問題的兩者。

1. 選取「**[!UICONTROL 儲存]**」。

## 測試並發佈 {#test-and-publish}

開啟預覽，並詢問服務人員符合&#x200B;**[!UICONTROL 使用時機]**&#x200B;條件之一的專案，例如要求示範。 禮賓部應提供與您連絡的專家服務、顯示聊天選項、會議選項或兩者，並提供實際可用性。

當行為正確時，請發佈您的服務人員，讓交接在您的網站上進行。

## 後續步驟 {#next-steps}

您的代表現在可以接收聊天和會議預約。 若要瞭解代表如何處理聊天，請參閱[聊天收件匣](chat-inbox.md)。
