---
title: 建立具有Brand Concierge許可權的角色
description: 瞭解如何建立角色，並授予其存取Brand Concierge所需的許可權。
source-git-commit: 591bd1600e586a0a4ce484dbff3f9fb97e24d43d
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 1%

---


# 建立具有Brand Concierge許可權的角色

在Adobe Experience Platform許可權中建立角色，以授與使用者對Brand Concierge的存取權。

## 先決條件

* 您必須擁有管理角色和許可權所需的管理員許可權。
* 必須先將使用者新增到Adobe Experience Platform組織。 如需詳細資訊，請參閱「將使用者新增至組織」（連結）。

## 建立角色

1. 登入`experienceplatform.adobe.com`。

   >[!NOTE]
   >
   >在發佈此程式之前，請先透過工程確認生產URL。 來源記錄使用非正式或可能轉錄錯誤的URL。

2. 在左側導覽列中，捲動至並選取&#x200B;**許可權**。
3. 選取&#x200B;**角色**&#x200B;以檢視現有的角色，然後選取&#x200B;**建立新角色**。
4. 輸入角色的名稱，例如`Brand Concierge Access Users`，新增說明，並確認建立。
5. 開啟新角色並指派許可權：

   1. 搜尋&#x200B;**Brand Concierge**&#x200B;的許可權清單。
   2. 選取&#x200B;**管理Brand Concierge**。

   目前，**管理Brand Concierge**&#x200B;是唯一可用的Brand Concierge許可權。 目前無法使用精細的許可權層級。

6. 選取角色可存取的一個或多個沙箱。

   組織可包含多個沙箱，這些沙箱為隔離的工作區。 僅選取適用於此角色的沙箱。

7. 選取「**儲存**」。

## 後續步驟

建立角色後，新增使用者至該角色。 如需詳細資訊，請參閱「將使用者新增至角色」（連結）。

## 相關考量事項

* 建立及管理沙箱的流程不在此程式的範圍內。
* 定義長期角色模型之前，請先確認是否計畫了其他精細的Brand Concierge許可權。
