---
title: 什麼是Adobe RecommendationsAPI?
description: 本教程指導開發人員通過實際操作練習，使用Adobe TargetRecommendationsAPI配置和管理Recommendations目錄和自定義標準，以及使用交付API檢索建議內容。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
source-git-commit: cee2618bb92284da1f82d108a0aff0d39340a15b
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 3%

---

# Adobe RecommendationsAPI概述

與 [!DNL Recommendations] 包括 [管理API](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) 允許您：

* 管理推薦產品或內容目錄
* 管理 [!DNL Recommendations] 算法和活動

使用 [!DNL Target] [傳遞API](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) 在Recommendations，你也可以：

* 在JSON、HTML或XML對象中檢索建議，以便它們可以在Web、移動、電子郵件、物聯網(IOT)和其他渠道中顯示。

## 教程說明

本教程將指導開發人員使用 [!DNL Recommendations] 要配置和管理的API [!DNL Recommendations] 目錄和自定義標準，以及使用交付API檢索建議內容。 在本教程結束時，您將能夠：

* 使用RecommendationsAPI配置和管理實體
* 使用RecommendationsAPI配置和管理自定義標準
* 瞭解如何將Recommendations與交付API一起使用以在非HTML設備中使用建議結果

## 對象

本教程適用於新加入目標API或RecommendationsAPI的開發人員。

## 先決條件

使用目標管理API需要 [Adobe驗證設定](https://developer.adobe.com/target/before-administer/configure-authentication/){target=&quot;_blank&quot;}。 在開始本教程之前，請確保已配置了此功能。

## 資源

請注意以下資源，這些資源是理解本教程並成功遵循本教程所必需的：

| 資源 | 詳細資料 |
| --- | --- |
| Postman | 獲取 [Postman應用](https://www.postman.com/downloads/) 作業系統。 Postman基本賬戶是免費的。 雖然一般不需要Adobe TargetAPI，但Postman使API工作流更加容易，而Adobe Target提供了幾個Postman集合，以幫助執行其API並瞭解它們如何操作。 本教程的其餘部分假定您對Postman有工作知識。 有關幫助，請參考 [Postman文檔](https://learning.getpostman.com/)。 |
| 引用 | 在本教程的其餘部分中，假定您熟悉以下資源：<UL><li>[Adobe I/O吉圖布](https://github.com/adobeio)</li><li>[目標Adobe I/O文檔](https://developers.adobetarget.com/api/#introduction)</li><li>[RecommendationsAPI文檔](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[下一個「管理Recommendations目錄」 >](https://developer.adobe.com/target/before-administer/recs-api/manage-catalog/){target=&quot;_blank&quot;
