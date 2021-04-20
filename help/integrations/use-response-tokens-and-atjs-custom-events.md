---
title: 如何使用回應Token和at.js自訂事件
description: 瞭解如何使用回應Token和at.js自訂事件，將描述檔資訊從Target共用至協力廠商系統。
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 4%

---


# 搭配Adobe Target使用回應Token和at.js自訂事件

回應Token和`at.js`自訂事件可讓您將描述檔資訊從[!DNL Target]共用至協力廠商系統。 [!DNL Target]訪客描述檔中的任何物件，包括自訂描述檔屬性、地理資訊、活動詳細資訊和內建描述檔，都可新增至[!DNL Target]回應，您可使用自訂JavaScript與協力廠商整合。

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## 如何使用回應Token和at.js自訂事件

1. 確定您需要[!DNL Target]中的哪些資料
1. 在「設定->回應Token」畫面上切換，以開啟您所需資料的回應Token
1. 確定需要使用哪個事件偵聽器
1. 撰寫必要的JavaScript來監聽Adobe Target事件、讀取回應Token，並執行整合所需的動作
1. 在「載入目標」動作後，使用Launch中的自訂程式碼動作來部署事件接聽程式JavaScript，或將它新增至Setup->Implementation畫面上at.js的「程式庫頁尾」區段，並儲存新的at.js檔案
1. QA並發佈您的整合

## 其他資源

* [使用與Adobe Target的Experience Cloud Debugger](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [回應Token檔案](https://docs.adobe.com/help/en/target/using/administer/response-tokens.html)
* [At.js自訂事件檔案](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/atjs-custom-events.html)
* [使用 Adobe Target 中的資料提供者](use-data-providers-to-integrate-third-party-data.md)