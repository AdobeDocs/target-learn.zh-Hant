---
title: 如何使用資料提供者來整合協力廠商資料
description: 本教學課程向使用者介紹資料提供者。 了解如何使用資料提供者功能，輕鬆將資料從協力廠商傳遞至Adobe Target。
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 23%

---

# 使用資料提供者將協力廠商資料整合至Adobe Target

[!UICONTROL 資料提供者這項功能可以讓您輕鬆將資料從第三方傳入 Target。]第三方可能是氣象服務、DMP，甚至是您自己的 Web 服務。接著，您就能使用此資料來建立對象、鎖定內容及擴充訪客設定檔。

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## 如何使用資料提供者

1. 實作專家在at.js之前新增程式碼（或在at.js的「資料庫標題」區段中），這會向協力廠商發出API呼叫、分析回應，並從回應中以名稱/值配對指定以傳送至[!DNL Target]。
1. at.js會處理忽隱忽現情況，並將名稱/值配對納入全域Target請求中的自訂參數。
1. 行銷人員根據這些自訂參數在[!DNL Target]介面中建立受眾。
1. 行銷人員使用這些對象來鎖定體驗、活動和量度，以及報表對象。

>[!NOTE]
>
>[!UICONTROL 資] 料提供者需要at.js 1.3或更新版本

## 支援材料

* [在at.js和Adobe Target中實作資料提供者](implement-data-providers-to-integrate-third-party-data.md)
* [資料提供者檔案](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en#data-providers)
