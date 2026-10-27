---
title: 聊天收件匣
description: 瞭解銷售代表如何在Adobe Marketo Qualifier聊天收件匣中接收、處理、評分及結束Brand Concierge即時聊天。
role: User
level: Beginner
product_v2:
  - id: b6ee73fe-bdc6-47d9-99a2-80194514dd40
    internal-label: Brand Concierge
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: 91cbec8d6f4e4800e3bdc8c8f60bfe9ed168a963
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%
---
# 聊天收件匣 {#chat-inbox}

當訪客要求與某人交談時，聊天會進入[!DNL Adobe Marketo Qualifier]中的&#x200B;**[!UICONTROL 聊天收件匣]**。 此頁面是代表對即時聊天內容的檢視：您到達時所看到的內容、取得的內容以及在關閉前必須執行的動作。

若要開啟聊天收件匣，請在&#x200B;**[!UICONTROL 活動]**&#x200B;下方的左側面板中，選取&#x200B;**[!UICONTROL 聊天收件匣]**。

## 接收聊天 {#receive}

您的狀態會顯示在收件匣的右上角。 **[!UICONTROL 可用]**&#x200B;表示您現在可以接收聊天。 您的即時聊天可用性時數決定您是否完全符合資格；請參閱[設定即時聊天可用性](representative-setup.md#chat-availability)。

您的聊天方式取決於&#x200B;**[!UICONTROL 即時聊天]**&#x200B;整合上設定的路由型別：

* 若使用循環配置資源，所有符合資格的代表都會同時收到通知，而第一個接受者會進行交談。
* 透過直接代理程式，聊天一律會連絡指定的代表。
* 若使用自訂路由，聊天內容會傳送給指派給訪客相符的最高優先順序規則的代表。

兩個索引標籤可組織您的交談：

* **[!UICONTROL 作用中]** — 目前正在進行中的交談。
* **[!UICONTROL 全部]** — 每個交談，包括已結束的交談。

## 接聽交談 {#pick-up}

你從不冷靜。 在您輸入任何內容之前，收件匣會提供訪客對門房已告知的所有內容。

![聊天收件匣顯示訪客交談摘要，以及討論的主題和設定檔詳細資料面板](../assets/sales-handoff-inbox-1.png){width="800" zoomable="yes"}

| 您所看到的內容 | 它提供您什麼 |
| --- | --- |
| **[!UICONTROL 訪客交談回顧]** | 訪客與禮賓處交談的&#x200B;**[!UICONTROL 摘要]**，以及討論的&#x200B;**[!UICONTROL 主題]** |
| 交談記錄 | 在即時聊天起始點上方，與門房進行完整交換 |
| **[!UICONTROL 表單詳細資料]** | 訪客在您加入之前在聊天前表單中輸入的內容，例如電子郵件、產品興趣和公司 |

文字記錄以兩個系統行`Live chat session has been initiated`和`Agent <name> has joined the chat`標示交接，因此您可以隨時分辨對話的哪一部分是服務人員，哪一部分是您的部分。

輸入訊息方塊並選取&#x200B;**[!UICONTROL 傳送]**&#x200B;以回覆。

![代表與訪客之間正在進行即時交談](../assets/sales-handoff-inbox-2.png){width="800" zoomable="yes"}

## 對交談評分 {#conversation-score}

在您結束聊天之前，請先評量訪客的資格。 此分數是由您設定的，此代表實際上與訪客交談，因此值得下游信任。

在&#x200B;**[!UICONTROL 設定檔詳細資料]**&#x200B;面板的&#x200B;**[!UICONTROL 交談分數]**&#x200B;下，選取評分。 破折號表示沒有分數，而火焰圖示會從最低等級到最高等級的對話評分。

![交談分數工具提示，說明分數儲存在潛在客戶記錄中為0、1、2和3](../assets/sales-handoff-inbox-4.png){width="600" zoomable="yes"}

| 選擇 | 儲存的值 | 含義 |
| --- | --- | --- |
| 虛線 | 0 | 最不合格 |
| 一個火焰 | 1 | 有點資格 |
| 兩個火焰 | 2 | 已符合資格 |
| 三種火焰 | 3 | 最合格 |

>[!IMPORTANT]
>
>評分為強制性。 如果您嘗試關閉聊天而不評分，則會顯示錯誤`Please score the conversation before you close the chat`，且聊天會保持開啟狀態。 分數後，會出現確認訊息，您可以關閉聊天。

![確認交談分數已儲存](../assets/sales-handoff-inbox-3.png){width="800" zoomable="yes"}

此分數會寫入[!DNL Marketo Engage]中的&#x200B;**[!UICONTROL Engage with Live Chat in Concierge]**&#x200B;活動，可作為篩選器和觸發器的限制。 使用它來推動重新目標定位、潛在客戶評分、個人化和CRM移交。 檢視Marketo Engage[&#128279;](marketo-activities.md)中的Brand Concierge資料。

## 結束聊天 {#end-chat}

選取&#x200B;**[!UICONTROL 結束交談]**&#x200B;以關閉交談。 訪客也可以從自己的側邊結束它，並會要求先確認。

當聊天結束時，其交談狀態會記錄為下列兩個值之一：

* **已結束** — 交談是由您或訪客蓄意關閉的。
* **已捨棄** — 訪客離開網站，交談因非使用中而逾時。

>[!NOTE]
>
>即時聊天對話會保留30天。

## 下一步 {#next}

在Marketo Engage的[Brand Concierge資料](marketo-activities.md)中，檢視這些會將哪些內容回寫至您的行銷資料庫。
