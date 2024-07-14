---
title: 如何使用資料提供者來整合協力廠商資料
description: 本教學課程向使用者介紹資料提供者。 瞭解如何使用資料提供者功能，輕鬆將資料從第三方傳遞至Adobe Target。
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 16%

---

# 使用資料提供者將第三方資料整合至Adobe Target

[!UICONTROL Data Providers]是一種功能，可讓您輕鬆將資料從第三方傳遞至Target。  第三方可能是氣象服務、DMP，甚至是您自己的 Web 服務。接著，您就能使用此資料來建立對象、鎖定內容及擴充訪客設定檔。

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## 如何使用資料提供者

1. 實作專家會在at.js之前新增程式碼（或在at.js的Library Header區段中），對第三方發出API呼叫、剖析回應並從回應中指定以名稱/值配對來傳送至[!DNL Target]。
1. at.js可管理忽隱忽現的情形，並將名稱/值配對納入全域Target請求中作為自訂引數。
1. 行銷人員會根據這些自訂引數在[!DNL Target]介面中建置對象。
1. 行銷人員使用這些對象來鎖定體驗、活動和量度，以及用於報表對象。

>[!NOTE]
>
>[!UICONTROL Data Providers]需要at.js 1.3或更高版本

## 支援材料

* [在at.js和Adobe Target中實作資料提供者](implement-data-providers-to-integrate-third-party-data.md)
