---
title: 如何實作資料提供者來整合協力廠商資料
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
source-wordcount: '285'
ht-degree: 0%

---

# 實作 [!UICONTROL 資料提供者] 將協力廠商資料整合至Adobe Target

實作詳細資料和如何使用Adobe Target的範例 [!UICONTROL 資料提供者] 功能，可從第三方資料提供者擷取資料，並將其傳遞至Target請求。

>[!NOTE]
>
>[!UICONTROL 資料提供者] 需要 `at.js` 1.3或更高版本

## 實作資料提供者的基本元件

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

的基本元件快速概覽 `dataProvider` 以及如何以正確的順序取得程式碼。\
視訊中使用的程式碼使用範例可在此處找到：
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## 與協力廠商API整合

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

更逼真的範例，整合氣象API。\
視訊中使用的程式碼使用範例可在此處找到：
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## 與多個提供者整合

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

如何將來自多個提供者的資料整合至您的全域 [!DNL Target] 要求。\
視訊中使用的程式碼使用範例可在此處找到：
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## 將頁面載入影響最小化

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

將資料儲存在工作階段儲存物件中，將對頁面載入時間的影響降至最低。 或者，您也可以使用 `profile.` 首碼，並在第一個首碼中傳遞它們 [!DNL Target] 工作階段的要求。 不過，每個請求只能傳遞50個設定檔引數。

視訊中使用的程式碼使用範例可在此處找到： [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## 支援材料

* [透過Adobe Target使用資料提供者](use-data-providers-to-integrate-third-party-data.md)
