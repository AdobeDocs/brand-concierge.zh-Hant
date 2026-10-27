---
title: 將交談路由給代表
description: 選擇Brand Concierge如何使用循環配置資源、直接代理程式或自訂路由規則，決定哪個銷售代表會收到即時聊天或會議預訂。
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
source-wordcount: '771'
ht-degree: 0%
---
# 將交談路由給代表 {#routing}

路由可回答一個問題：當此訪客詢問個人時，*他們收到哪個*&#x200B;人？

您為&#x200B;**[!UICONTROL Meeting Booking]**&#x200B;整合與&#x200B;**[!UICONTROL 即時交談]**&#x200B;整合分別挑選路由型別，讓服務生將每一次交談均分給一位專家，或任何其他組合。

## 路由型別 {#routing-types}

| 路由型別 | 誰取得交談 | 需要[!DNL Marketo Engage] |
| --- | --- | --- |
| **[!UICONTROL 循環配置資源]** | 已分發給所有符合資格的代表 | 無 |
| **[!UICONTROL 直接代理程式]** | 請您指派一位代表 | 無 |
| **[!UICONTROL 自訂路由]** | 指派給訪客符合資格的最高優先順序路由規則的代表 | 是 |

循環配置資源預設為可用，不需要設定。 您可在整合本身上設定路由型別。 檢視[啟用即時聊天和會議預訂](configure-in-composer.md)。

### 循環配置資源 {#round-robin}

循環配置資源在會議中的行為與聊天中的行為不同，因為兩者的目標不同。

針對會議預訂，循環配置資源會平均分配會議。 首先提供已連線行事曆的第一個合格代表。 與他們預約會議後，他們就會被帶出泳池，並安排下一位代表。 前五個會議有五名代表，由五名不同的人參加。 每個人都收到一個後，集區會重設，然後週期會再次開始。

池也會每24小時重設一次，以便平均分配每日的會議。

>[!NOTE]
>
>24小時循環配置資源重設會在UTC執行，而不是在代表的當地時區執行。

對於即時交談，沒有循序輪換。 所有符合資格的代表都會同時收到傳入聊天通知，第一個接受的人會進行交談。

### 直接代理 {#direct-agent}

來自此服務生的每個會議或聊天都會轉至您選取的單一代表。 請將此用於一位客戶主管所擁有的行銷活動登陸頁面，或用於擁有一位專家的區域。

### 自訂路由 {#custom-routing}

自訂路由會根據訪客的[!DNL Marketo]銷售機會和公司屬性評估您在[!DNL Adobe Marketo Qualifier]中建立的規則。 當適當的代表需要依賴您瞭解的訪客相關資訊時，請使用此報表，例如：

* 地理位置：來自一組國家/地區的訪客會前往地區團隊。
* 產品興趣：對特定產品感興趣的訪客，請前往該產品專家。
* 業務單位、公司規模或產業：潛在客戶與公司屬性的任何組合。

>[!IMPORTANT]
>
>自訂路由是需要[!DNL Adobe Marketo Engage]的Live Chat和Meeting預約的一部份，因為規則是以[!DNL Marketo]銷售機會和公司屬性建置的。 循環配置資源與直接代理程式無需使用它即可運作。

## 建立自訂路由規則 {#create-rule}

1. 在[!DNL Adobe Marketo Qualifier]中的&#x200B;**[!UICONTROL 管理]**&#x200B;下，選取&#x200B;**[!UICONTROL 路由規則]**。

   清單會顯示貴組織中的每個規則及其優先順序、名稱、建立者和建立日期。

   ![路由規則頁面列出具有優先順序、名稱、建立者及建立於資料行](../assets/sales-handoff-routing-1.png){width="800" zoomable="yes"}的現有規則

1. 選取&#x200B;**[!UICONTROL 建立規則]**&#x200B;並為規則命名。

1. 建立條件。

   左側面板列出來自&#x200B;**[!UICONTROL 公司]**&#x200B;和&#x200B;**[!UICONTROL 潛在客戶]** （人員）物件的可用[!DNL Marketo]屬性。 搜尋屬性，然後將其拖曳至畫布以新增條件。

1. 為每個條件設定運運算元和值。

   運運算元包含&#x200B;**[!UICONTROL 等於]**、**[!UICONTROL 不等於]**&#x200B;和&#x200B;**[!UICONTROL 包含]**&#x200B;等。 例如，`Country` **[!UICONTROL 等於]** `United States`。

1. 將條件組合成群組。

   將數個條件新增至一個群組，並加入&#x200B;**[!UICONTROL AND]**&#x200B;或&#x200B;**[!UICONTROL OR]**。 新增更多群組並加入&#x200B;**[!UICONTROL AND]**&#x200B;或&#x200B;**[!UICONTROL OR]**&#x200B;的群組。 以這種方式在群組內巢狀條件可讓您表示複雜的條件，例如&#x200B;*（國家/地區為美國或加拿大）和（產品興趣包含Analytics）*。

1. 將規則指派給代表。

   在指派段落下，依名稱搜尋代表，並從清單中選取代表。 新增任意數目的代表。 任何人都可以接收符合規則的交談。

1. 選取「**[!UICONTROL 儲存]**」。

## 優先順序的套用方式 {#priority}

每個路由規則都有優先權。 只有在訪客符合多個規則的資格時，優先順序才重要。

發生這種情況時，只會套用最高優先順序的相符規則，且對話會路由至指派給該規則的代表。 訪客也符合資格，但排名較低的規則會被忽略。

>[!NOTE]
>
>數字越低，優先順序越高。 優先順序為1的規則會勝過優先順序為2的規則。 建立規則的人設定其優先順序。

在成功規則中，指派給它的代表是合格的集區，會議循環配置資源行為以及上述聊天通知所有人行為都適用於該集區。

## 下一步 {#next}

在代表設定並決定路由後，將權能新增至禮賓員。 檢視[啟用即時聊天和會議預訂](configure-in-composer.md)。
