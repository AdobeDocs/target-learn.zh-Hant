---
title: 如何使用回應代號和at.js自訂事件
description: 瞭解如何使用回應Token和at.js自訂事件，共用從Target到協力廠商系統的設定檔資訊。
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
TQID: https://experienceleague.adobe.com/gJfFi9mC3iKY8pEdvE1Tuk7Mk2rUOdTKtv67vXQwkO8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 230
ht-degree: 3%

---

# 將回應代號和at.js自訂事件與Adobe Target搭配使用

回應Token和`at.js`自訂事件可讓您從[!DNL Target]將設定檔資訊分享至協力廠商系統。 [!DNL Target]訪客設定檔中的任何物件，包括自訂設定檔屬性、地理資訊、活動詳細資料和內建設定檔，都可以新增至[!DNL Target]回應，讓您可以使用自訂JavaScript與協力廠商整合。

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## 如何使用回應代號和at.js自訂事件

1. 決定您需要從[!DNL Target]取得哪些資料
1. 在設定 — >回應Token畫面中切換按鈕，以開啟所需資料的回應Token
1. 決定您需要使用的事件監聽器
1. 撰寫監聽Adobe Target事件、讀取回應Token以及執行整合所需操作所需的JavaScript
1. 在「載入Target」動作之後，使用Launch中的自訂程式碼動作來部署事件接聽程式JavaScript，或將其新增至at.js的「設定」 — >「實作」畫面上的「資料庫頁尾」區段，並儲存新的at.js檔案
1. QA並發佈您的整合

## 其他資源

* [將Experience Cloud Debugger與Adobe Target搭配使用](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [回應Token檔案](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hant)
* [使用 Adobe Target 中的資料提供者](use-data-providers-to-integrate-third-party-data.md)
