---
title: 開發人員和自訂指南
description: 瞭解如何安裝Brand Concierge Web SDK和Web使用者端、自訂外觀和內容、處理使用者端事件以及匯出交談資料。
role: Developer,Admin
level: Experienced
toc: true
source-git-commit: 13db0491c987a08492820ac216e20feb87f30e44
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 4%

---


# 開發人員和自訂指南 {#developer-customization-guide}

本指南適用於實作或自訂Brand Concierge部署的開發人員和技術團隊。 內容包括安裝Web SDK和Web使用者端、自訂外觀和內容、透過回呼函式聆聽使用者端事件，以及匯出交談資料以供報告。

## Web SDK和Web使用者端安裝 {#installation}

### 先決條件 {#prerequisites}

* 組織是Adobe Experience Platform (AEP)客戶。
* 此頁面會使用Adobe Experience Platform Web SDK來檢測。
* 頁面上使用的資料串流ID已啟用Brand Concierge。

### 步驟1：插入網頁SDK {#inject-web-sdk}

新增下列內容至頁面的`<head>`區段：

```html
<script>
  !(function (n, o) {
    o.forEach(function (o) {
      n[o] ||
        ((n.__alloyNS = n.__alloyNS || []).push(o),
        (n[o] = function () {
          var u = arguments;
          return new Promise(function (i, l) {
            n[o].q.push([i, l, u]);
          });
        }),
        (n[o].q = []));
    });
  })(window, ["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.31.1/alloy.min.js"></script>
```

### 步驟2：插入網頁使用者端 {#inject-web-client}

在網頁SDK指令碼後新增以下內容，仍在`<head>`區段中：

```html
<script src="https://experience.adobe.net/solutions/experience-platform-brand-concierge-web-agent/static-assets/main.js"></script>
```

### 步驟3：設定網頁SDK {#configure-web-sdk}

使用您組織自己的值來呼叫`alloy("configure", ...)`，以取代下列預留位置：

```javascript
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "edge.adobedc.net",
  edgeBasePath: "ee",
  datastreamId: "YOUR_DATASTREAM_ID",
  orgId: "YOUR_IMS_ORG_ID",
  debugEnabled: true,
  idMigrationEnabled: false,
  thirdPartyCookiesEnabled: false,
  prehidingStyle: ".personalization-container { opacity: 0 !important }",
  onBeforeEventSend: (options) => {
    const x = options.xdm;
    const params = new URLSearchParams(window.location.search);
    const titleParam = params.get("title");
    if (titleParam) {
      x.web.webPageDetails.name = titleParam;
    } else {
      x.web.webPageDetails.name = "default-page";
    }
    return true;
  }
});
alloy("sendEvent", {});
```

| 欄位 | 說明 |
|---|---|
| `datastreamId` | 為此頁面設定的資料串流ID，已為Brand Concierge啟用。 |
| `orgId` | 在下設定接待的IMS組織ID。 |
| `debugEnabled` | 在驗證整合後，在生產環境中設定為`false`。 |
| `prehidingStyle` | 在個人化內容載入之前套用CSS，以避免無樣式內容的Flash。 |
| `onBeforeEventSend` | 選用的勾點，可在傳送前修改XDM裝載 — 通常用於設定頁面名稱或內容。 |

### 步驟4：初始化Web使用者端 {#initialize-web-client}

在Web SDK設定呼叫後，呼叫啟動程式API以初始化Web使用者端：

```javascript
window.adobe.concierge.bootstrap({
  instanceName: "alloy",
  stylingConfigurations: window.styleConfigurations,
  selector: "#brand-concierge-mount"
});
```

| 參數 | 類型 | 必要 | 說明 |
|---|---|---|---|
| `instanceName` | string | 是 | Web SDK執行個體名稱。 |
| `stylingConfigurations` | json物件 | 是 | Web使用者端樣式設定（請參閱[視覺化與內容自訂](#customization)）。 |
| `selector` | string | 是 | 網頁使用者端掛載之HTML元素的CSS選取器。 |
| `onEvent` | 函式 | 否 | 使用者端事件的回呼（請參閱[使用者端事件和回呼函式](#events)）。 |

## 視覺化與內容自訂 {#customization}

傳遞至`bootstrap()`的`stylingConfigurations`物件可控制整個Web使用者端的外觀、行為和文字。 它可組織為數個區域。

### 中繼資料 {#metadata}

```javascript
"metadata": {
  "brandName": "Your Brand",
  "version": "1.0.0",
  "language": "en-US",
  "namespace": "brand-concierge"
}
```

### 行為 {#behavior}

控制個別聊天功能的功能行為。

```javascript
"behavior": {
  "input": {
    "enableVoiceInput": true
  },
  "chat": {
    "messageAlignment": "left",
    "messageWidth": "80%"
  },
  "privacyNotice": {
    "title": "Privacy Notice",
    "text": "By using this automated chatbot, you consent that any personal information you provide in the chat may be collected, used, analyzed, disclosed, and retained by Adobe and its service providers, in accordance with the Adobe Privacy Policy. Please do not enter any sensitive personal information (e.g., financial or health data)."
  },
  "disclaimer": {
    "attachWithInput": true
  },
  "chatTranscript": {
    "enabled": true,
    "maxSessions": 1,
    "maxMessagesPerSession": 20,
    "cleanupInterval": 24
  },
  "meetingForm": {
    "fieldsPerRow": 2,
    "title": { "text": "Schedule meeting", "alignment": "left" },
    "subtitle": { "text": "I'd be happy to help you schedule a meeting! Please fill out the form below, and we'll follow up with a calendar to confirm your day and time.", "alignment": "left" },
    "buttons": {
      "submit": { "text": "Schedule meeting", "alignment": "left" },
      "cancel": { "text": "Cancel", "alignment": "left" }
    }
  },
  "calendarWidget": {
    "title": { "text": "Book a meeting", "alignment": "left" },
    "subtitle": { "text": "Thanks! Here's a calendar where you can choose a time that works best for your schedule:", "alignment": "left" },
    "postTitle": { "text": "Once confirmed, you'll receive a calendar invite with all the details.", "alignment": "left" },
    "buttons": {
      "confirm": { "text": "Schedule a meeting", "alignment": "left" },
      "cancel": { "text": "Cancel", "alignment": "left" }
    }
  }
}
```

### 免責聲明 {#disclaimer}

```javascript
"disclaimer": {
  "text": "AI responses may be inaccurate or misleading. Be sure to double check answers and sources."
}
```

### 文字字串 {#text-strings}

透過`text`物件可覆寫所有面向使用者的復本。 公用鍵：

| 索引鍵 | 目的 |
|---|---|
| `welcome.heading` / `welcome.subheading` | 歡迎熒幕標題和副文字 |
| `input.placeholder` | 輸入欄位預留位置文字 |
| `input.messageInput.aria` / `input.send.aria` / `input.mic.aria` | 輸入控制項的協助工具標籤 |
| `error.network` / `error.general` | 向訪客顯示的錯誤訊息 |
| `loading.message` | 產生回應時顯示的文字 |
| `feedback.dialog.title.positive` / `.negative` | 意見回饋對話方塊標題 |
| `feedback.dialog.question.positive` / `.negative` | 意見回饋對話方塊提示文字 |
| `feedback.toast.success` | 提交意見反應後的確認快顯通知 |
| `feedback.thumbsUp.aria` / `feedback.thumbsDown.aria` | 意見按鈕的協助工具標籤 |

### 陣列 {#arrays}

可設定的內容清單：

```javascript
"arrays": {
  "welcome.examples": [
    {
      "text": "I want to edit and enhance my photos",
      "image": "https://example.com/idea-1.png",
      "backgroundColor": "#66BFE7"
    }
  ],
  "feedback.positive.options": [
    "Helpful and relevant recommendations",
    "Clear and easy to understand",
    "Friendly and conversational tone",
    "Visually appealing presentation",
    "Other"
  ],
  "feedback.negative.options": [
    "Not helpful or relevant",
    "Confusing or unclear",
    "Too formal or robotic",
    "Poor visual presentation",
    "Other"
  ]
}
```

### 資產 {#assets}

```javascript
"assets": {
  "icons": {
    "company": "<svg>...</svg>"
  }
}
```

### 主題 {#theme}

CSS自訂屬性可控制顏色、字型和版面：

```css
"theme": {
  "--color-primary": "#1473e6",
  "--color-primary-hover": "#0056b3",
  "--color-button-primary": "#3B63FB",
  "--color-accent": "#9085ED",
  "--color-button-submit": "#4759e6",
  "--color-button-submit-hover": "#3a4bce",
  "--color-message-user": "#1473e6",
  "--font-family": "'Adobe Clean', adobe-clean, 'Trebuchet MS', sans-serif",
  "--main-container-background": "linear-gradient(135deg, #66ccff, #cc99ff, #ffcc99, #ccff99)",
  "--submit-button-fill-color": "white",
  "--card-text-background": "var(--color-background)",
  "--card-text-border-radius": "var(--border-radius-card)",
  "--message-concierge-link-decoration": "underline",
  "--message-max-width": "100%"
}
```

## 使用者端事件和回呼函式 {#events}

事件回呼系統可讓頁面即時觀察Web使用者端生命週期事件、使用者互動、回應、回饋和錯誤，適合用來將參與資料傳送至Adobe Analytics、Google Analytics或其他協力廠商系統。

### 主要特性 {#key-characteristics}

* **單一回呼** — 一個`onEvent`函式會接收所有事件型別（由`event.eventType`區分）。
* **唯讀** — 事件資料是複製的快照，無法用來修改使用者端行為。
* **錯誤隔離** — 擷取並記錄回撥中擲回的例外狀況；它們不會中斷Web使用者端。
* **已透過`bootstrap()`**&#x200B;註冊 — 傳遞的方式與`onBeforeEventSend`相同。

### 快速入門 {#quick-start}

```javascript
window.adobe.concierge.bootstrap({
  instanceName: "my-instance",
  selector: "#brand-concierge-mount",
  stylingConfigurations: { /* ... */ },
  onEvent: (event) => {
    console.log(event.eventType, event.timestamp, event.data);
  }
});
```

### 依事件型別篩選 {#filtering}

```javascript
onEvent: (event) => {
  switch (event.eventType) {
    case "query:submitted":
      console.log("User query:", event.data.query);
      break;
    case "response:completed":
      console.log("Response received:", event.data.conversationId);
      break;
    case "card:clicked":
      console.log("Card clicked:", event.data.element.entity_info.productName);
      break;
    case "error:occurred":
      console.log("Error:", event.data.errorMessage);
      break;
  }
}
```

### 事件類型 {#event-types}

| 事件型別 | 值 | 類別 | 當它觸發時 |
|---|---|---|---|
| `WEBCLIENT_INITIALIZED` | `webclient:initialized` | 生命週期 | 使用者端完成初始化（已裝載DOM，已載入內容） |
| `QUERY_SUBMITTED` | `query:submitted` | 使用者互動 | 使用者提交訊息（輸入或來自建議） |
| `PROMPT_SUGGESTION_CLICKED` | `promptSuggestion:clicked` | 使用者互動 | 使用者按一下提示建議藥丸 |
| `CARD_CLICKED` | `card:clicked` | 使用者互動 | 使用者按一下卡片 |
| `HISTORY_CLEARED` | `history:cleared` | 使用者互動 | 使用者清除聊天記錄 |
| `RESPONSE_STARTED` | `response:started` | 回應 | 第一個串流區塊來自API |
| `RESPONSE_COMPLETED` | `response:completed` | 回應 | 已接收並轉譯完整回應 |
| `CARDS_RENDERED` | `cards:rendered` | 回應 | 卡片（單一影像或輪播）完成呈現 |
| `FEEDBACK_SUBMITTED` | `feedback:submitted` | 意見反應 | 使用者提交意見表單（拇指朝上/朝下，並附上詳細資料） |
| `ERROR_OCCURRED` | `error:occurred` | 錯誤 | 發生錯誤（網路、API或執行階段） |

### 生命週期事件 {#lifecycle-events}

使用者端已完全初始化後會引發`webclient:initialized`：已載入內容、插入CSS、在DOM中呈現聊天UI。

```json
{
  "eventType": "webclient:initialized",
  "timestamp": 1741638123789,
  "data": {
    "instanceName": "my-instance"
  }
}
```

### 使用者互動事件 {#user-interaction-events}

使用者根據提示建議或Widget選項提交訊息（不論是輸入的訊息）時，`query:submitted`會引發。

```json
{
  "eventType": "query:submitted",
  "timestamp": 1741638124000,
  "data": {
    "query": "What photo editing tools do you offer?"
  }
}
```

使用者按一下提示建議藥丸時，`promptSuggestion:clicked`會引發。 它會在&#x200B;*之前*&#x200B;引發後續`query:submitted`事件。

```json
{
  "eventType": "promptSuggestion:clicked",
  "timestamp": 1741638124100,
  "data": {
    "suggestion": "Tell me more about Photoshop"
  }
}
```

使用者按一下卡片時，`card:clicked`會引發。

```json
{
  "eventType": "card:clicked",
  "timestamp": 1741638124200,
  "data": {
    "element": {
      "entity_info": {
        "productName": "Adobe Photoshop",
        "productDescription": "Photo editing software",
        "productPageURL": "https://www.adobe.com/products/photoshop.html",
        "productImageURL": "https://example.com/photoshop.png"
      }
    }
  }
}
```

`history:cleared`會在使用者按一下clear-chat-history按鈕時引發。

```json
{
  "eventType": "history:cleared",
  "timestamp": 1741638124400,
  "data": {}
}
```

### 回應事件 {#response-events}

第一個串流區塊從API到達時，`response:started`會引發。

```json
{
  "eventType": "response:started",
  "timestamp": 1741638125000,
  "data": {
    "conversationId": "conv-abc-123",
    "interactionId": "int-xyz-456"
  }
}
```

收到完整回應時，`response:completed`會引發。

```json
{
  "eventType": "response:completed",
  "timestamp": 1741638126000,
  "data": {
    "conversationId": "conv-abc-123",
    "interactionId": "int-xyz-456"
  }
}
```

在DOM中轉譯卡片後，`cards:rendered`會引發。 它與`response:completed`分開觸發，並指示使用的顯示模式。

```json
{
  "eventType": "cards:rendered",
  "timestamp": 1741638126100,
  "data": {
    "element": [
      { "entity_info": { "productName": "Adobe Photoshop" } },
      { "entity_info": { "productName": "Adobe Illustrator" } }
    ],
    "displayMode": "carousel"
  }
}
```

### 意見反應事件 {#feedback-events}

使用者完成並提交意見表單（在縮圖上/下後）時，`feedback:submitted`會引發。

```json
{
  "eventType": "feedback:submitted",
  "timestamp": 1741638127000,
  "data": {
    "conversationId": "conv-abc-123",
    "interactionId": "int-xyz-456",
    "feedbackType": "negative",
    "selectedOptions": ["Incorrect information", "Not relevant"],
    "notes": "The response did not address my question about pricing."
  }
}
```

### 錯誤事件 {#error-events}

使用者端發生網路、API或執行階段錯誤時，`error:occurred`會引發。

```json
{
  "eventType": "error:occurred",
  "timestamp": 1741638128000,
  "data": {
    "errorMessage": "Something went wrong. Please try again."
  }
}
```

### 事件物件結構 {#event-object-structure}

每個事件會共用相同的頂層圖形：

```typescript
interface BrandConciergeEvent {
  eventType: string;  // e.g. "query:submitted"
  timestamp: number;  // Unix epoch, milliseconds
  data: object;       // Event-specific payload
}
```

### 資料型別參考：元素（產品卡） {#element-reference}

```typescript
interface Element {
  id?: string;
  type?: string;
  entity_info: {
    productName: string;
    productDescription: string;
    description: string;
    productPageURL: string;
    details: string;
    backgroundColor: string;
    learningResource: string;
    productImageURL: string;
    logo: string;
    variants?: Record<string, ElementVariant>;
    primary: ElementAction;
    secondary: ElementAction;
  };
}

interface ElementAction {
  label: string;
  url: string;
}
```

### 最佳實務 {#best-practices}

* **用於分析和監視。** 追蹤參與、查詢模式和產品興趣；將`error:occurred`轉送到錯誤追蹤服務；追蹤卡片點選以進行轉換分析。
* **保持回撥快速。** 它會在主要執行緒上同步執行，因此請避免封鎖網路呼叫：

```javascript
// Good — fire and forget
onEvent: (event) => {
  navigator.sendBeacon("/analytics", JSON.stringify(event));
}

// Avoid — blocking network call
onEvent: async (event) => {
  await fetch("/analytics", { body: JSON.stringify(event) });
}
```

* **對於狀態機器不要依賴嚴格的事件順序**。 事件會以邏輯順序引發，但使用`conversationId`和`interactionId`來關聯相關事件，而非假設順序。
* **處理您自己的回呼中的錯誤。** 使用者端會隔離並記錄回呼錯誤，但回呼中未處理的錯誤仍會遺失分析資料：

```javascript
onEvent: (event) => {
  try {
    myAnalytics.track(event);
  } catch (e) {
    console.warn("Analytics tracking failed", e);
  }
}
```

## 使用AEP查詢服務匯出交談 {#export-conversations}

Brand Concierge會將對話資料（提示、回應和意見回饋）寫入Adobe Experience Platform (AEP)資料集。 您可以使用查詢服務(SQL)直接查詢這些專案，以建置自訂報表。

### 尋找資料集和表格名稱 {#find-dataset}

1. 開啟Adobe Experience Platform。

1. 移至&#x200B;**[!UICONTROL 資料集]**。

1. 搜尋`cja_brand_concierge`以列出與Brand Concierge相關的資料集。

1. 開啟您需要的資料集（例如，如果存在多個資料流，回應會比對其他資料流）。

1. 在資料集詳細資料檢視上，尋找Query Service使用的&#x200B;**[!UICONTROL 資料表名稱]**，並檢查範例或預覽資料以確認資料行（提示、回應、回饋、時間戳記等）。

>[!NOTE]
>
>表格名稱會繫結至每個資料集，而且會因環境和沙箱而異。 如果您有多個沙箱或部署，請在正確的沙箱中重複這些步驟，讓表格名稱與資料寫入位置相符。

### 範例查詢 {#example-query}

```sql
SELECT *
FROM cja_brand_concierge_responses_dataset_5f5105bd_1c38_4ebc_8505_bd
WHERE timestamp >= TIMESTAMP '2026-03-16 00:00:00'
  AND timestamp <= NOW()
ORDER BY timestamp ASC;
```

>[!IMPORTANT]
>
>上方的表格名稱只是圖例，請勿對其硬式編碼。 先在AEP中確認資料集的實際資料表名稱（請參閱[尋找資料集和資料表名稱](#find-dataset)），然後調整時間篩選、排序順序或其他子句，以符合您的報告需求。 使用與資料集相同的沙箱，從您組織的查詢服務工作流程（UI、API或連線使用者端）執行查詢。

### 在查詢服務UI中執行查詢 {#run-query-ui}

如果您需要手動提取資料才能進行報告，查詢服務UI提供一種直接執行和下載結果的方式：

1. 在Adobe Experience Platform中，移至&#x200B;**[!UICONTROL 查詢]**。

1. 在編輯器中輸入查詢，然後按一下&#x200B;**[!UICONTROL 執行查詢]**。

1. 查詢完成後，結果會顯示在編輯器下方的&#x200B;**[!UICONTROL 結果]**&#x200B;索引標籤中。 從那裡，您可以下載結果。

### 進一步閱讀 {#further-reading}

* [查詢服務API檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/query/home){target="_blank"} — Adobe的查詢服務行為、限制、驗證和API路徑的官方參考，這些內容會隨著時間而改變，與本指南無關。
