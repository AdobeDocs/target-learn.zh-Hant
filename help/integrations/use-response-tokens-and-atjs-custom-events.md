---
title: 如何使用回應Token和at.js自訂事件
description: 了解如何使用回應Token和at.js自訂事件，共用從Target到協力廠商系統的設定檔資訊。
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
source-git-commit: d1517f0763290eb61a9e4eef4f2eb215a9cdd667
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 3%

---

# 將回應代號和at.js自訂事件與Adobe Target搭配使用

回應Token和`at.js`自訂事件可讓您將設定檔資訊從[!DNL Target]共用至協力廠商系統。 [!DNL Target]訪客設定檔中的任何物件，包括自訂設定檔屬性、地理資訊、活動詳細資料和內建設定檔，都可以新增至[!DNL Target]回應中，您可以在此使用自訂JavaScript與協力廠商整合。

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## 如何使用回應Token和at.js自訂事件

1. 確定您需要[!DNL Target]中的資料
1. 開啟設定 — >回應Token畫面上的切換按鈕，以開啟您需要的資料的回應Token
1. 確定您需要使用哪個事件偵聽器
1. 撰寫必要的JavaScript，以監聽Adobe Target事件、讀取回應Token，並執行您整合所需的動作
1. 在「載入Target」動作後，使用Launch中的自訂程式碼動作部署事件接聽程式JavaScript，或將其新增至at.js的「設定 — >實作」畫面上的「資料庫頁尾」區段，然後儲存新的at.js檔案
1. QA並發佈您的整合

## 其他資源

* [使用Experience Cloud Debugger搭配Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [回應Token檔案](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [at.js自訂事件檔案](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/atjs-custom-events.html?lang=en)
* [使用 Adobe Target 中的資料提供者](use-data-providers-to-integrate-third-party-data.md)
