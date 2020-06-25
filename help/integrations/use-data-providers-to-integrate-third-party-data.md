---
title: 使用資料提供者將協力廠商資料整合至Adobe Target
seo-title: 使用資料提供者將協力廠商資料整合至Adobe Target
description: 資料提供者這項功能可以讓您輕鬆將資料從第三方傳入 Target。第三方可能是氣象服務、DMP，甚至是您自己的 Web 服務。接著，您就能使用此資料來建立對象、鎖定內容及擴充訪客設定檔。
audience: marketer
difficulty: 5
author: Daniel Wright
doc-type: use
activity-type: feature-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 40%

---


# 使用資料提供者將協力廠商資料整合至Adobe Target

[!UICONTROL 資料提供者這項功能可以讓您輕鬆將資料從第三方傳入 Target。]第三方可能是氣象服務、DMP，甚至是您自己的 Web 服務。接著，您就能使用此資料來建立對象、鎖定內容及擴充訪客設定檔。

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## 如何使用資料提供者

1. 實作專家會在at.js之前（或在at.js的「程式庫標題」區段中）新增程式碼，以便對協力廠商進行API呼叫、分析回應並指定來自回應的名稱／值配對 [!DNL Target]。
1. at.js會管理閃爍，並將名稱／值配對包含為全域Target請求中的自訂參數。
1. 行銷人員會根據這些自訂 [!DNL Target] 參數，在介面中建立受眾。
1. 行銷人員使用這些對象來定位體驗、活動和量度，以及報告對象。

>[!NOTE]
>
>[!UICONTROL 資料提供者] at.js 1.3或更新版本

## 支援材料

* [在at.js和Adobe Target中實作資料提供者](implement-data-providers-to-integrate-third-party-data.md)
* [資料提供者檔案](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)