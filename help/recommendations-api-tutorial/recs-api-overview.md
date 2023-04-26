---
title: 什麼是Adobe Recommendations API?
description: 本教學課程將逐步引導開發人員實作實踐，使用Adobe Target Recommendations API來設定和管理Recommendations目錄和自訂條件，以及使用傳送API來擷取建議內容。
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
source-wordcount: '374'
ht-degree: 3%

---

# Adobe Recommendations API概述

與 [!DNL Recommendations] 包括 [管理API](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) 可讓您：

* 管理建議產品或內容的目錄
* 管理 [!DNL Recommendations] 演算法與活動

使用 [!DNL Target] [傳送API](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) 有了Recommendations，您也可以：

* 在JSON、HTML或XML物件中擷取建議，以便在網路、行動裝置、電子郵件、物聯網(IOT)和其他通道中顯示。

## 教學課程說明

本教學課程會逐步引導開發人員了解使用 [!DNL Recommendations] 要配置和管理的API [!DNL Recommendations] 目錄和自訂條件，以及使用傳送API來擷取建議內容。 在本教學課程結束前，您將能：

* 使用Recommendations API設定和管理實體
* 使用Recommendations API設定和管理自訂條件
* 了解如何搭配傳送API使用Recommendations，以在非HTML裝置中使用建議

## 對象

本教學課程適用於Target API或Recommendations API的新開發人員。

## 先決條件

使用Target管理API需要 [Adobe驗證設定](https://experienceleague.adobe.com/docs/target-dev/developer/api/configure-authentication.html){target="_blank"}. 開始本教學課程之前，請務必先完成此設定。

## 資源

請注意下列必要資源，這些資源是了解本教學課程並成功遵循的必要資源：

| 資源 | 詳細資料 |
| --- | --- |
| Postman | 取得 [Postman應用程式](https://www.postman.com/downloads/) 作業系統。 Postman Basic免費建立帳戶。 Postman雖然並非一般使用Adobe Target API的必要條件，但可讓API工作流程更輕鬆，而Adobe Target提供數個Postman集合，以協助執行其API並了解其運作方式。 本教學課程的其餘部分假設您具備Postman的工作知識。 如需協助，請參考 [Postman檔案](https://learning.getpostman.com/). |
| 參考 | 在本教學課程的其餘部分中，我們假設您熟悉以下資源：<UL><li>[Adobe I/OGithub](https://github.com/adobeio)</li><li>[TargetAdobe I/O檔案](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API檔案](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[下堂課「管理Recommendations目錄」>](https://experienceleague.adobe.com/docs/target-dev/developer/api/recommendations-api/manage-catalog.html){target="_blank"}
