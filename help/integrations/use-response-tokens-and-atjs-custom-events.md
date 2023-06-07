---
title: 如何使用回應Token和at.js自訂事件
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
source-wordcount: '225'
ht-degree: 3%

---

# 將回應代號和at.js自訂事件與Adobe Target搭配使用

回應權杖和 `at.js` 自訂事件可讓您分享設定檔資訊，從 [!DNL Target] 至協力廠商系統。 中的任何物件 [!DNL Target] 訪客設定檔，包括自訂設定檔屬性、地理資訊、活動詳細資訊，以及內建設定檔，可新增至 [!DNL Target] 回應，您可在其中使用自訂JavaScript來與協力廠商整合。

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## 如何使用回應Token和at.js自訂事件

1. 決定您需要從哪些資料 [!DNL Target]
1. 在設定 — >回應Token畫面中翻轉切換按鈕，開啟所需資料的回應Token
1. 決定您需要使用的事件接聽程式
1. 撰寫監聽Adobe Target事件所需的JavaScript、讀取回應Token，並執行整合所需的工作
1. 在「載入Target」動作之後，使用Launch中的自訂程式碼動作來部署事件接聽程式JavaScript，或將其新增至at.js的「設定」 — >「實作」畫面上的「資料庫頁尾」區段，並儲存新的at.js檔案
1. QA並發佈您的整合

## 其他資源

* [搭配Adobe Target使用Experience Cloud Debugger](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [回應Token檔案](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [使用 Adobe Target 中的資料提供者](use-data-providers-to-integrate-third-party-data.md)
