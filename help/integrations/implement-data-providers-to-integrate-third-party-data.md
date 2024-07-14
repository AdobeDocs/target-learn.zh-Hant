---
title: 如何實作資料提供者以整合協力廠商資料
description: 本教學課程提供實作詳細資訊，並舉例說明如何使用Adobe Target的資料提供者功能，從第三方資料提供者擷取資料，並將其傳遞至Target請求。
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: fcf6d1a8-e2a7-41ce-9c1c-02985b7afb5a
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 實作[!UICONTROL Data Providers]以將協力廠商資料整合至Adobe Target

實作詳細資料和範例，說明如何使用Adobe Target的[!UICONTROL Data Providers]功能從第三方資料提供者擷取資料，並將資料傳遞至Target請求。

>[!NOTE]
>
>[!UICONTROL Data Providers]需要`at.js` 1.3或更高版本

## 實作資料提供者的基本元件

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

快速概述`dataProvider`的基本元件，以及如何以正確順序取得您的程式碼。\
您可以在下列位置找到視訊中使用程式碼的工作範例：
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## 與協力廠商API整合

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

整合氣象API是較現實的範例。\
您可以在下列位置找到視訊中使用程式碼的工作範例：
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## 與多個提供者整合

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

如何將來自多個提供者的資料合併到您的全域[!DNL Target]要求中。\
您可以在下列位置找到視訊中使用程式碼的工作範例：
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## 將頁面載入影響降到最低

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

將資料儲存在工作階段儲存物件中，將對頁面載入時間的影響降至最低。 或者，您可以使用`profile.`首碼將值傳遞為設定檔引數，然後只在工作階段的前[!DNL Target]個要求中傳遞它們。 不過，每個請求只能傳遞50個設定檔引數。

您可以在下列位置找到使用視訊中所用程式碼的工作範例： [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## 支援材料

* [使用資料提供者搭配Adobe Target](use-data-providers-to-integrate-third-party-data.md)
