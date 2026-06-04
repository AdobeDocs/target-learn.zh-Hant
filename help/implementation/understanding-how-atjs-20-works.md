---
title: at.js 2.0如何運作？
description: 瞭解at.js 2.0如何增強Adobe Target對單頁應用程式(SPA)的支援，並與其他Experience Cloud解決方案整合。
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
TQID: https://experienceleague.adobe.com/yi78hasak-rtlhpCG4-UnewWXAwMfPZJSpw9sFzRenU
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 412
ht-degree: 0%

---

# 瞭解Adobe Target的at.js 2.0如何運作

`at.js` 2.0增強了Adobe Target對單頁應用程式(SPA)的支援，並與其他Experience Cloud解決方案整合。 本影片和隨附的圖表說明各種元素的結合方式。

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## 架構圖

![at.js 2.0在頁面載入時的行為](assets/pageload.png)

1. 呼叫會傳回Experience Cloud ID (ECID)。 如果使用者已通過驗證，則另一個呼叫會同步客戶ID。

1. `at.js`資料庫會同步載入，並隱藏檔案本文（`at.js`也可以使用頁面上實作的選擇性預先隱藏程式碼片段來非同步載入）。

1. 提出頁面載入請求，包含所有已設定的引數、ECID、SDID和客戶ID。

1. 設定檔指令碼執行並加入[!UICONTROL 設定檔存放區]。 存放區會從[!UICONTROL 對象資料庫]要求合格對象（例如從[!DNL Analytics]、Audience Manager等共用的對象）。 [!UICONTROL 客戶屬性]會以批次程式傳送至[!UICONTROL 設定檔存放區]。
1. 根據URL、要求引數和設定檔資料，[!DNL Target]會決定可針對目前頁面和未來檢視傳回哪些活動和體驗給訪客

1. 目標內容會傳回至頁面，選擇性地包括其他個人化的設定檔值。

   目前頁面上目標內容會儘快出現，不會有忽隱忽現的預設內容。

   單頁應用程式未來檢視的目標內容會快取在瀏覽器中，因此可在觸發檢視時立即套用，不需額外的伺服器呼叫。 （請參閱下圖，瞭解`triggerView()`行為）。

1. 從頁面傳送至[!UICONTROL 資料收集]伺服器的[!DNL Analytics]資料
1. [!DNL Target]資料已透過SDID比對至Analytics資料，並已處理至[!DNL Analytics]報表儲存體。 然後就可以透過A4T報表在[!DNL Analytics]和[!DNL Target]中檢視[!DNL Analytics]資料。

使用triggerView()函式時的![at.js 2.0行為](assets/triggerview.png)

1. 在單頁應用程式中呼叫`adobe.target.triggerView()`
1. 從快取讀取檢視的目標內容

1. 目標內容會儘快出現，不會有忽隱忽現的預設內容

1. 通知要求已傳送至[!DNL Target] [!UICONTROL 設定檔存放區]，以計算活動中的訪客數和增加量度
1. [!DNL Analytics]資料從SPA傳送到[!UICONTROL 資料收集]伺服器

1. [!DNL Target]資料從[!DNL Target]後端傳送至[!UICONTROL 資料收集]伺服器。 [!DNL Target]資料透過SDID與[!DNL Analytics]資料相符，並且已處理至[!DNL Analytics]報表儲存體。 然後就可以透過A4T報表在[!DNL Analytics]和[!DNL Target]中檢視[!DNL Analytics]資料。

## 其他資源

* [在單頁應用程式中實作at.js 2.0](implement-atjs-20-in-a-single-page-application.md)
* [使用適用於單頁應用程式的Adobe Target視覺化體驗撰寫器(SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
