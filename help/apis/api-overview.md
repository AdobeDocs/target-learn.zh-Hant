---
title: Adobe Target API概觀
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations包含一組專屬的API，可讓您管理建議產品和／或內容的目錄； 管理您的建議演算法和宣傳活動； 並以JSON、HTML或XML物件提供建議，以便顯示在網頁、行動裝置、電子郵件、IOT和其他通道中。
kt: null
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: b66dbae616c9559f5d1b7bbedf2d9b383840973b
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---


# Adobe Target API概觀

Adobe Target API可依類型分組。

| API 類型 | 它可讓您 | 下載連結 |
| --- | --- | --- |
| 管理 | 建立、修改和刪除活動、觀眾、選件和其他物件(包括 [!DNL Recommendations] 實體、准則、設計等)。 API [!DNL Recommendations] 是一種管理API。) | <UL><li>[Target Admin API Postman Collection](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Recommendations API Postman Collection](https://developers.adobetarget.com/api/recommendations/#section/Postman)</li></ul> |
| 傳送 | 從中擷取最佳化和個人化的 [!DNL Target] 內容，以便傳送給使用者。 | [Target Delivery API Postman Collection](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection) |
| 報表 | 匯出活動結果和其他報告結果。 | 報表API包含在 [Target Admin API Postman集合中](https://developers.adobetarget.com/api/#admin-postman-collection)。 |
| 描述檔 | 擷取並修改儲存在Adobe Target中的使用者設定檔。 | [Target描述檔API Postman Collection](https://developers.adobetarget.com/api/#profiles) |

請注意管理 **API** (包括 [!DNL Recommendations] API)與傳送API（可讓您設定Adobe Target的各個方面）之 ****&#x200B;間的區別，傳送API可讓您擷取內容。 管理API需要驗證，而傳送API則不需要。

若要使用Adobe Target管理API，您首先需要使用Adobe I/O來設定驗證。

[下一個「配置身份驗證」 >](configure-io-target-integration.md)
