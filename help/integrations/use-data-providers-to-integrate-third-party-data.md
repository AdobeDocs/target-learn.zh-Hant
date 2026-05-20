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
TQID: https://experienceleague.adobe.com/XiUlJGHSFVxAMqdl6Y7hK9PoXOgiiUI43vrFeAj2Rpo
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 195
ht-degree: 16%

---

# 使用資料提供者將第三方資料整合至Adobe Target

[!UICONTROL Data Providers]是一種功能，可讓您輕鬆將資料從第三方傳遞至Target。  第三方可能是氣象服務、DMP，甚至是您自己的 Web 服務。 接著，您就能使用此資料來建立對象、鎖定內容及擴充訪客設定檔。

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
