---
title: 如何實施資料提供者整合第三方資料
description: 本教學課程提供實作詳細資訊和範例，說明如何使用Adobe Target的資料提供者功能從第三方資料提供者擷取資料，並在Target要求中傳遞資料。
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# 實作[!UICONTROL 資料提供者]，將協力廠商資料整合至Adobe Target

實作詳細資訊和範例，說明如何使用Adobe Target的[!UICONTROL 資料提供者]功能，從第三方資料提供者擷取資料，並在Target要求中傳遞資料。

>[!NOTE]
>
>[!UICONTROL 資料] 提供者 `at.js` 需要1.3或更新版本

## 實作資料提供者的基本元件

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

快速概述`dataProvider`的基本元件，以及如何依正確順序取得程式碼。\
此處提供視訊中使用之程式碼的運作範例：
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## 與協力廠商API整合

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

更真實的例子，整合氣象API。\
此處提供視訊中使用之程式碼的運作範例：
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## 與多個提供者整合

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

如何將來自多個提供者的資料併入您的全域[!DNL Target]請求。\
此處提供視訊中使用之程式碼的運作範例：
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## 將頁面載入影響降至最低

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

將資料儲存在作業階段儲存物件中，將對頁面載入時間的影響降到最低。 或者，您也可以使用`profile.`首碼將值作為描述檔參數傳遞，並直接在工作階段的第一個[!DNL Target]請求中傳遞。 不過，每個請求只能傳遞50個描述檔參數。

此處提供視訊中使用之程式碼的運作範例：[https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## 支援材料

* [搭配Adobe Target使用資料提供者](use-data-providers-to-integrate-third-party-data.md)

* [資料提供者檔案](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)