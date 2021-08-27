---
title: 如何實作資料提供者以整合協力廠商資料
description: 本教學課程提供實作詳細資料和範例，說明如何使用Adobe Target的資料提供者功能，從協力廠商資料提供者擷取資料，並將其傳遞至Target請求。
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
exl-id: fcf6d1a8-e2a7-41ce-9c1c-02985b7afb5a
source-git-commit: d1517f0763290eb61a9e4eef4f2eb215a9cdd667
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 實作[!UICONTROL 資料提供者]以將協力廠商資料整合至Adobe Target

實作詳細資料和範例，說明如何使用Adobe Target的[!UICONTROL 資料提供者]功能，從協力廠商資料提供者擷取資料，並將其傳入Target請求。

>[!NOTE]
>
>[!UICONTROL 資] 料提供 `at.js` 者需要1.3或更新版本

## 實作資料提供者的基本元件

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

快速概述`dataProvider`的基本元件，以及如何以正確的順序取得程式碼。\
若需影片中使用的程式碼的實用範例，請前往此處：
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## 與協力廠商API整合

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

整合氣象API的更實際範例。\
若需影片中使用的程式碼的實用範例，請前往此處：
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## 與多個提供者整合

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

如何將來自多個提供者的資料併入您的全域[!DNL Target]請求。\
若需影片中使用的程式碼的實用範例，請前往此處：
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## 將頁面載入影響降至最低

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

將資料儲存在工作階段儲存物件中，將對頁面載入時間的影響降至最低。 或者，您也可以使用`profile.`首碼，將值以描述檔參數的形式傳遞，然後在工作階段的第一個[!DNL Target]要求中傳遞。 不過，您只能針對每個請求傳遞50個設定檔參數。

若需影片中使用的程式碼的實用範例，請前往此處：[https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## 支援材料

* [透過Adobe Target使用資料提供者](use-data-providers-to-integrate-third-party-data.md)

* [資料提供者檔案](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en#data-providers)
