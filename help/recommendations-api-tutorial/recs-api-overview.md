---
title: Adobe Recommendations API概觀
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations包含一組專屬的API，可讓您管理建議產品和／或內容的目錄；管理您的建議演算法和宣傳活動；並以JSON、HTML或XML物件提供建議，以便顯示在網頁、行動裝置、電子郵件、IOT和其他通道中。
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: c221f434ce9daec03dbb4d897343775b40b14462
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 1%

---


# Adobe Recommendations API概觀

與[!DNL Recommendations]相關的API包括[管理API](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html)，可讓您：

* 管理建議產品或內容的目錄
* 管理您的[!DNL Recommendations]演算法和活動

使用[!DNL Target] [傳送API](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html)搭配Recommendations，您也可以：

* 在JSON、HTML或XML物件中擷取建議，以便在網頁、行動裝置、電子郵件、物聯網(IOT)和其他通道中顯示。

## 教學課程說明

本教學課程將逐步帶領開發人員使用[!DNL Recommendations] API來設定和管理[!DNL Recommendations]型錄和自訂准則，以及使用傳送API來擷取建議內容，以進行實際操作。 在本教學課程結束時，您將能夠：

* 使用Recommendations API設定和管理實體
* 使用Recommendations API設定並管理自訂標準
* 瞭解如何搭配傳送API使用Recommendations以在非HTML裝置中使用建議結果

## 對象

本教學課程適用於Target API或Recommendations API新手的開發人員。

## 先決條件

使用Target管理API需要[Adobe驗證設定](../apis/configure-io-target-integration.md)。 在開始本教學課程之前，請務必先設定此設定。

## 資源

請注意下列必要資源，以瞭解本教學課程並順利遵循：

| 資源 | 詳細資料 |
| --- | --- |
| 郵遞員 | 取得您作業系統的[Postman應用程式](https://www.postman.com/downloads/)。 郵遞員基本功能是免費的，可建立帳戶。 Postman可讓API工作流程更輕鬆，而Adobe Target則提供數個Postman系列，以協助執行其API並瞭解其運作方式。 本教程的其餘部分假定您對郵遞員有工作知識。 如需協助，請參閱[郵遞員檔案](https://learning.getpostman.com/)。 |
| 參考 | 在本教學課程的其餘部分中，我們假定您熟悉以下資源：<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[鎖定Adobe I/O檔案](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API檔案](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[下一個「管理您的Recommendations目錄」>](manage-catalog.md)
