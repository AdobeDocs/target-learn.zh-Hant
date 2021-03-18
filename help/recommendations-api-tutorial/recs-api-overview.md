---
title: 什麼是Adobe RecommendationsAPI?
description: 本教學課程將帶領開發人員進行實際操作，使用Adobe TargetRecommendationsAPI來設定和管理Recommendations型錄和自訂准則，以及使用傳送API來擷取建議內容。
role: 開發人員
level: 中級
topic: 個人化、管理、整合、開發
feature: API/SDK,Recommendations，管理與設定，概觀
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 1%

---


# Adobe RecommendationsAPI概觀

與[!DNL Recommendations]相關的API包括[管理API](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html)，可讓您：

* 管理建議產品或內容的目錄
* 管理您的[!DNL Recommendations]演算法和活動

使用[!DNL Target] [傳送API](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html)搭配Recommendations，您也可以：

* 在JSON、HTML或XML物件中擷取建議，以便在網頁、行動裝置、電子郵件、物聯網(IOT)和其他通道中顯示。

## 教學課程說明

本教學課程將逐步帶領開發人員使用[!DNL Recommendations] API來設定和管理[!DNL Recommendations]型錄和自訂准則，以及使用傳送API來擷取建議內容，以進行實際操作。 在本教學課程結束時，您將能夠：

* 使用RecommendationsAPI設定和管理實體
* 使用RecommendationsAPI設定和管理自訂准則
* 瞭解如何搭配傳送API使用Recommendations，在非HTML裝置中使用建議結果

## 對象

本教學課程適用於Target API或RecommendationsAPI新手的開發人員。

## 先決條件

使用Target管理API需要[Adobe驗證設定](../apis/configure-io-target-integration.md)。 在開始本教學課程之前，請務必先設定此設定。

## 資源

請注意下列必要資源，以瞭解本教學課程並順利遵循：

| 資源 | 詳細資料 |
| --- | --- |
| 郵遞員 | 取得您作業系統的[Postman應用程式](https://www.postman.com/downloads/)。 郵遞員基本功能是免費的，可建立帳戶。 雖然一般而言，Adobe TargetAPI並非必要項目，但Postman讓API工作流程更輕鬆，而Adobe Target則提供數個Postman系列，以協助執行其API並瞭解其運作方式。 本教程的其餘部分假定您對郵遞員有工作知識。 如需協助，請參閱[郵遞員檔案](https://learning.getpostman.com/)。 |
| 參考 | 在本教學課程的其餘部分中，我們假定您熟悉以下資源：<UL><li>[Adobe I/O吉圖布](https://github.com/adobeio)</li><li>[TargetAdobe I/O檔案](https://developers.adobetarget.com/api/#introduction)</li><li>[RecommendationsAPI檔案](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[下一個「管理您的Recommendations目錄」 >](manage-catalog.md)
