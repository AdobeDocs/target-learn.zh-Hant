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
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '217'
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

* [搭配Adobe Target使用Experience Cloud Debugger](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [回應Token檔案](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [使用 Adobe Target 中的資料提供者](use-data-providers-to-integrate-third-party-data.md)
