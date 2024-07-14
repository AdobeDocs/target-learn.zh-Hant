---
title: 什麼是Adobe Recommendations API？
description: 本教學課程會逐步引導開發人員使用Adobe Target Recommendations API來設定和管理Recommendations目錄和自訂條件，以及使用傳送API來擷取建議內容。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
source-git-commit: 542ff406fc24df54a2f1b007422492341ea46507
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 2%

---

# Adobe Recommendations API概觀

與[!DNL Recommendations]相關的API包含[管理員API](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en)，可讓您：

* 管理建議產品或內容的目錄
* 管理您的[!DNL Recommendations]演演算法和活動

透過Recommendations使用[!DNL Target] [傳遞API](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en)，您也可以：

* 擷取JSON、HTML或XML物件中的建議，以便這些建議可在網頁、行動裝置、電子郵件、物聯網(IOT)和其他管道中顯示。

## 教學課程說明

此教學課程會逐步引導開發人員使用[!DNL Recommendations] API來設定和管理[!DNL Recommendations]目錄和自訂條件，以及使用傳送API來擷取建議內容。 在本教學課程結束時，您將能夠：

* 使用Recommendations API設定和管理實體
* 使用Recommendations API設定和管理自訂條件
* 瞭解如何搭配傳送API使用Recommendations，以在非HTML裝置中使用建議結果

## 對象

本教學課程適用於不熟悉Target API或Recommendations API的開發人員。

## 先決條件

使用Target管理員API需要[Adobe驗證設定](https://experienceleague.adobe.com/docs/target-dev/developer/api/configure-authentication.html){target="_blank"}。 在開始本教學課程之前，請確定您已設定此專案。

## 資源

請注意下列資源，這些資源是瞭解本教學課程並成功遵循本教學課程所必需的：

| 資源 | 詳細資料 |
| --- | --- |
| Postman | 取得您作業系統的[Postman應用程式](https://www.postman.com/downloads/)。 Postman basic可免費建立帳戶。 雖然在一般情況下使用Adobe Target API不需要使用，但Postman可簡化API工作流程，而Adobe Target提供多個Postman集合來協助執行其API並瞭解其運作方式。 本教學課程的其餘部分假設您具備Postman的工作知識。 如需協助，請參考[Postman檔案](https://learning.getpostman.com/)。 |
| 參考 | 在本教學課程的其餘部分中，假設您已熟悉下列資源：<UL><li>[Adobe I/O的Github](https://github.com/adobeio)</li><li>[目標Adobe I/O檔案](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API檔案](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[下堂課「管理您的Recommendations目錄」>](https://experienceleague.adobe.com/docs/target-dev/developer/api/recommendations-api/manage-catalog.html){target="_blank"}
