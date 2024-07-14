---
title: at.js 2.0如何運作？
description: at.js 2.0增強了Adobe Target對單頁應用程式(SPA)的支援，並與其他Experience Cloud解決方案整合。 本影片和隨附的圖表說明各種元素的結合方式。
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# 瞭解Adobe Target的at.js 2.0如何運作

`at.js` 2.0增強了Adobe Target對單頁應用程式(SPA)的支援，並與其他Experience Cloud解決方案整合。 本影片和隨附的圖表說明各種元素的結合方式。

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## 架構圖

![at.js 2.0在頁面載入時的行為](assets/pageload.png)

1. 呼叫會傳回Experience CloudID (ECID)。 如果使用者已通過驗證，則另一個呼叫會同步客戶ID。

1. `at.js`資料庫會同步載入，並隱藏檔案本文（`at.js`也可以使用頁面上實作的選擇性預先隱藏程式碼片段來非同步載入）。

1. 提出頁面載入請求，包含所有已設定的引數、ECID、SDID和客戶ID。

1. 設定檔指令碼執行並加入[!UICONTROL Profile Store]。 存放區會從[!UICONTROL Audience Library]要求合格對象(例如從[!DNL Analytics]、Audience Manager等共用的對象)。 [!UICONTROL Customer Attributes]會以批次程式傳送至[!UICONTROL Profile Store]。
1. 根據URL、要求引數和設定檔資料，[!DNL Target]會決定可針對目前頁面和未來檢視傳回哪些活動和體驗給訪客

1. 目標內容會傳回至頁面，選擇性地包括其他個人化的設定檔值。

   目前頁面上目標內容會儘快出現，不會有忽隱忽現的預設內容。

   單頁應用程式未來檢視的目標內容會快取在瀏覽器中，因此可在觸發檢視時立即套用，不需額外的伺服器呼叫。 （請參閱下圖，瞭解`triggerView()`行為）。

1. 從頁面傳送至[!UICONTROL Data Collection]伺服器的[!DNL Analytics]資料
1. [!DNL Target]資料已透過SDID比對至Analytics資料，並已處理至[!DNL Analytics]報表儲存體。 然後就可以透過A4T報表在[!DNL Analytics]和[!DNL Target]中檢視[!DNL Analytics]資料。

使用triggerView()函式時的![at.js 2.0行為](assets/triggerview.png)

1. 在單頁應用程式中呼叫`adobe.target.triggerView()`
1. 從快取讀取檢視的目標內容

1. 目標內容會儘快出現，不會有忽隱忽現的預設內容

1. 通知要求已傳送至[!DNL Target] [!UICONTROL Profile Store]，以計算活動中的訪客數並增加量度
1. [!DNL Analytics]資料從SPA傳送到[!UICONTROL Data Collection]伺服器

1. [!DNL Target]資料從[!DNL Target]後端傳送至[!UICONTROL Data Collection]伺服器。 [!DNL Target]資料透過SDID與[!DNL Analytics]資料相符，並且已處理至[!DNL Analytics]報表儲存體。 然後就可以透過A4T報表在[!DNL Analytics]和[!DNL Target]中檢視[!DNL Analytics]資料。

## 其他資源

* [在單頁應用程式中實作at.js 2.0](implement-atjs-20-in-a-single-page-application.md)
* [使用適用於單頁應用程式的Adobe Target Visual Experience Composer (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
