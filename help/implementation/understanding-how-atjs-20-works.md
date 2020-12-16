---
title: 瞭解Adobe Target的at.js 2.0運作方式
seo-title: 瞭解Adobe Target的at.js 2.0運作方式
description: at.js 2.0增強了Adobe Target對單頁應用程式(SPA)的支援，並與其他Experience Cloud解決方案整合。 這段視頻和隨附的圖解說明了一切如何匯集在一起。
audience: developer
difficulty: 3
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 11%

---


# 瞭解Adobe Target的at.js 2.0運作方式

`at.js` 2.0增強了Adobe Target對單頁應用程式(SPA)的支援，並與其他Experience Cloud解決方案整合。這段視頻和隨附的圖解說明了一切如何匯集在一起。

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## 體系結構圖

![at.js 2.0頁面載入行為](assets/pageload.png)

1. 呼叫會傳回Experience Cloud ID(ECID)。 如果使用者經過驗證，則另一個呼叫會同步客戶ID。

1. `at.js` 程式庫會同步載入並隱藏檔案內`at.js` 文（也可以使用頁面上實作的選擇性預先隱藏程式碼片段，以非同步方式載入）。

1. 會提出「頁面載入」要求，包括所有已設定的參數、ECID、SDID和客戶ID。

1. 配置檔案指令碼執行並饋送到[!UICONTROL Profile Store]中。 「商店」會向[!UICONTROL 觀眾程式庫]要求合格的觀眾（例如，從[!DNL Analytics]、Audience Manager等共用的觀眾）。 [!UICONTROL 客戶] 屬性會在批處理 [!UICONTROL 中] 傳送至描述檔儲存。
1. [!DNL Target]會根據URL、請求參數和描述檔資料，決定要針對目前頁面和未來檢視返回訪客的活動和體驗

1. 目標內容傳回至頁面，可選擇包含個人檔案值以進行其他個人化。

   目前頁面上目標內容會儘快出現，不會有忽隱忽現的預設內容。

   針對未來單一頁面應用程式檢視的目標內容會在瀏覽器中快取，如此當觸發檢視時，就可立即套用，而不需額外的伺服器呼叫。 （請參閱下圖瞭解`triggerView()`行為）。

1. [!DNL Analytics] 從頁面傳送至資料收集伺服 [!UICONTROL 器的] 資料
1. [!DNL Target] 資料會透過 SDID 來比對 資料，然後經過處理放入 Analytics 報表儲存體中。[!DNL Analytics][!DNL Analytics] 然後，您就可以透過A4T報 [!DNL Analytics] 表 [!DNL Target] 同時檢視資料。

![at.js 2.0行為，當使用triggerView()函式時](assets/triggerview.png)

1. `adobe.target.triggerView()` 在單頁應用程式中呼叫
1. 從快取讀取視圖的目標內容

1. 盡快呈現目標內容，而不會閃爍預設內容

1. 通知請求會傳送至[!DNL Target] [!UICONTROL 描述檔商店]，以計算活動中的訪客並增加量度
1. [!DNL Analytics] 資料會從SPA傳送至資料收 [!UICONTROL 集伺] 服器

1. [!DNL Target] 資料會從後端傳 [!DNL Target] 送至資 [!UICONTROL 料收] 集伺服器。[!DNL Target] 資料會透過 SDID 來比對 [!DNL Analytics] 資料，然後經過處理放入 [!DNL Analytics] 報表儲存體中。[!DNL Analytics] 然後，您就可以透過A4T報 [!DNL Analytics] 表 [!DNL Target] 同時檢視資料。

## 其他資源

* [在單頁應用程式中實作at.js 2.0](implement-atjs-20-in-a-single-page-application.md)
* [使用Adobe Target的Visual Experience Composer進行單頁應用程式(SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [at.js的運作方式說明檔案](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/at-js/how-atjs-works.html)