---
title: at.js 2.0如何運作？
description: at.js 2.0增強了Adobe Target對單頁應用程式(SPA)的支援，並與其他Experience Cloud解決方案整合。 此影片和隨附的圖表說明一切如何結合。
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
source-git-commit: a6b645b6d9693a4c8882fd47ee0d61698c0b834d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 11%

---

# 了解Adobe Target的at.js 2.0如何運作

`at.js` 2.0增強了Adobe Target對單頁應用程式(SPA)的支援，並與其他Experience Cloud解決方案整合。此影片和隨附的圖表說明一切如何結合。

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## 架構圖

![at.js 2.0頁面載入時的行為](assets/pageload.png)

1. 呼叫會傳回Experience CloudID(ECID)。 如果使用者已驗證，則另一個呼叫會同步客戶ID。

1. `at.js` 程式庫會同步載入並隱藏檔案內文(`at.js` 也可以使用頁面上實作的選用預先隱藏程式碼片段，以非同步方式載入)。

1. 提出頁面載入請求，包括所有已設定的參數、ECID、SDID和客戶ID。

1. 設定檔指令碼執行並饋送至[!UICONTROL 設定檔存放區]。 存放區會從[!UICONTROL 對象資料庫]要求合格對象(例如從[!DNL Analytics]共用的對象、Audience Manager等)。 [!UICONTROL 客戶] 屬性會透過批 [!UICONTROL 次程] 式傳送至設定檔儲存。
1. [!DNL Target]會根據URL、請求參數和設定檔資料，決定要針對目前頁面和未來檢視傳回給訪客的活動和體驗

1. 傳回至頁面的目標內容，選擇性地包括其他個人化的設定檔值。

   目前頁面上目標內容會儘快出現，不會有忽隱忽現的預設內容。

   系統會在瀏覽器中快取單頁應用程式未來檢視的目標內容，以便在觸發檢視時立即套用，而不需額外的伺服器呼叫。 （請參閱下一張`triggerView()`行為圖表）。

1. [!DNL Analytics] 從頁面傳送至資料收集伺 [!UICONTROL 服] 器
1. [!DNL Target] 資料會透過 SDID 來比對 資料，然後經過處理放入 Analytics 報表儲存體中。[!DNL Analytics][!DNL Analytics] 然後，即可在和中透 [!DNL Analytics] 過 [!DNL Target] A4T報表檢視資料。

![at.js 2.0使用triggerView()函式時的行為](assets/triggerview.png)

1. `adobe.target.triggerView()` 在單頁應用程式中呼叫
1. 從快取讀取檢視的目標內容

1. 目標內容會盡快出現，不會有忽隱忽現的預設內容

1. 通知請求會傳送至[!DNL Target] [!UICONTROL 設定檔存放區]，以計算活動中的訪客數並增加量度
1. [!DNL Analytics] 資料會從SPA傳送至Data  [!UICONTROL CollectionServer] s

1. [!DNL Target] 資料會從後端 [!DNL Target] 傳送至 [!UICONTROL Data ] CollectionServers。[!DNL Target] 資料會透過 SDID 來比對 [!DNL Analytics] 資料，然後經過處理放入 [!DNL Analytics] 報表儲存體中。[!DNL Analytics] 然後，即可在和中透 [!DNL Analytics] 過 [!DNL Target] A4T報表檢視資料。

## 其他資源

* [在單頁應用程式中實作at.js 2.0](implement-atjs-20-in-a-single-page-application.md)
* [針對單頁應用程式(SPA VEC)使用Adobe Target的可視化體驗撰寫器](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [at.js如何運作檔案](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en)
