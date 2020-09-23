---
title: 使用傳送API擷取建議
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
source-wordcount: '1473'
ht-degree: 0%

---


# 使用 [!DNL Recommendations] 傳送API擷取

Adobe Target和Adobe Target [!DNL Recommendations] API可用來傳遞網頁回應，但也可用於非HTML型的體驗，包括應用程式、螢幕、控制台、電子郵件、資訊站和其他顯示裝置。 換言之，當無法 [!DNL Target] 使用程式庫和JavaScript時， **[!DNL Target]Delivery API** (傳送API [!DNL Target] )仍可讓我們存取各種功能，以提供個人化的體驗。

>[!NOTE]
>
> 請求包含實際建議（建議產品或項目）的內容時，請使用 [!DNL Target] 傳送API。

若要擷取建議，請傳送含有適當內容資訊的Adobe Target傳送API POST呼叫，其中可能包含使用者ID（以用於特定描述檔的建議，例如使用者最近檢視的項目）、相關mbox名稱、mbox參數、描述檔參數或其他屬性。 回應將包含JSON或HTML格式的建議entity.ids（且可能包含其他實體資料），然後會顯示在裝置中。

Adobe Target [的Delivery API](https://developers.adobetarget.com/api/delivery-api/) ，可公開標準要求提供的所有現 [!DNL Target] 有功能。

>[!NOTE]
>傳送API:
>* 可讓您以REST風格擷取位置和對象的體驗或選件。
>* 不需要驗證。
>* 僅開機自檢。
>* 不處理Cookie或重新導向呼叫。
>* 不需要或識別「使用者角色」。 它只會擷取內容或報告事件至 [!DNL Target] 邊緣伺服器。


若要使用傳送API來傳送體驗( [!DNL Target] 包括建議)，請遵循下列步驟：

1. 使用 [!DNL Target] 表單式撰寫器（非視覺體驗撰寫器）建立活動( [!DNL Recommendations]A/B、XT、AP或)。
2. 使用「傳送API」來取得您剛建立之活動所產生 [!DNL Target] 之請求的回應。

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## 使用表單型體驗撰寫器建立建議

若要建立可與傳送API搭配使用的建議，請使用表 [格式撰寫器](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)。

1. 首先，建立並儲存要用於建議的JSON架構設計。 如需範例JSON，加上設定表單型活動時如何傳回JSON回應的背景資訊，請參閱建立建議設 [計的檔案](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html)。 在此範例中，設計名為 *Simple JSON。*

   ![server-side-create-recs-json-design-png](assets/server-side-create-recs-json-design.png)

2. 在中 [!DNL Target]，導航至「建立活 **[!UICONTROL 動]」> 「活動[!UICONTROL 」，然]後選擇「表******&#x200B;單建議」。

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. 選取屬性，然後按一下「下 **[!UICONTROL 一步]**」。
4. 定義您希望使用者接收建議回應的位置。 以下範例使用名為 *api_charter的位置*。 選取您以JSON為基礎的設計，先前建立，名為 *Simple JSON。*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. 儲存並啟動建議。 它將產生結果。 [結果準備就緒後](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html)，您就可以使用傳送API來擷取結果。

## 使用傳送API

The syntax for the [Delivery API](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API) is:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. 請注意，用戶端代碼是必要的。 提醒您，您的用戶端程式碼可在Adobe Target中導覽至「 **[!UICONTROL Recommendations]>設[!UICONTROL 定」]**。 請注意「 **[!UICONTROL 建議API Token]** 」區段 **[!UICONTROL 中的「用戶端代碼]** 」值。
   ![client-code.png](assets/client-code.png)
1. 在您取得用戶端程式碼後，建構您的傳送API呼叫。 下列範例從「傳送 **[!UICONTROL API郵遞人」系列中提供的「網頁批次Mbox傳送API呼叫」開]**[](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)始，進行相關修改。 例如:
   * 瀏 **覽器和** 地址物件已從 **Body中移除******，因為非HTML使用案例不需要這些物件
   * *api_charter* 在此範例中列為位置名稱
   * entity.id已指定，因為此建議是以內容相似性為基礎，而內容相似性需要傳遞目前的項目索引鍵 [!DNL Target]。
      ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)Remember可正確設定查詢參數。 例如，請務必指定`{{CLIENT_CODE}}` 必要。 <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. 傳送請求。 此動作會針對 *api_charter* location執行，該位置上會執行作用中建議，且會以您的JSON設計定義，並輸出建議實體的清單。
1. 根據JSON設計接收回應。
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)回應包含索引鍵ID以及建議實體的實體ID。

以此方式使用 [!DNL Recommendations] 傳送API，可讓您在非HTML裝置上向訪客顯示建議之前，先執行其他步驟。 例如，您可以利用「傳送API」的回應，從其他系統（例如CMS、PIM或電子商務平台）執行額外的即時實體屬性詳細資訊查閱（庫存、價格、評分等），然後再顯示最終結果。

使用本教學課程中概述的方法，您可以取得任何應用程式，以運用回應來 [!DNL Target] 提供個人化建議！

## 範例實施

下列資源提供各種非HTML重點實作的範例。 請記住，由於涉及的系統和裝置，每個實作都是獨一無二的。

| 資源 | 詳細資料 |
| --- | --- |
| [在AEM中使用REST風格的API](https://helpx.adobe.com/experience-manager/using/restful-services.html) | 如何建立和部署Adobe Experience Manager OSGi套件，以取用來自協力廠商REST風格的網站服務的資料。 |
| [Adobe Target Everywhere —— 在IoT中實作伺服器端](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit 2019 Lab，為運用Adobe Target伺服器端API的React應用程式提供實際操作體驗。 |
| [Adobe Target在不使用Adobe SDK的行動應用程式中](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | 本指南說明如何在行動應用程式中設定Adobe Target，而不需安裝Adobe SDK。 此解決方案使用Tealium SDK網頁檢視和遠端指令模組，傳送和接收要求至Adobe Visitor API(Experience Cloud)和Adobe Target API。 |
| [Adobe Target在行動應用程式中的運作方式](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | 如何 [!DNL Target] 與Mobile SDK搭配使用 |
| [設定 [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | 在Experience Platform Launch中設定 [!DNL Target] 擴充功能、將擴充功能新增至應用程式，以及實作 [!DNL Target][!DNL Target] API以請求活動、預回遷選件和進入視覺預覽模式的步驟。 |
| [Adobe Target節點用戶端](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | 開放來源 [!DNL Target] 的Node.js SDK v1.0 |
| [伺服器端概觀](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | Adobe Target伺服器端傳送API、伺服器端批次傳送API、Node.js SDK和Adobe Target [!DNL Recommendations] API的相關資訊。 |
| [電子郵件中的Adobe Campaign內容建議](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | 說明如何在Adobe Campaign中透過Adobe Target和Adobe I/O Runtime運用電子郵件中的內容建議的部落格。 |

## 使用API [!DNL Recommendations] 管理設定

大部分時候，建議是在Adobe Target UI中設定，然後透過 [!DNL Target] API使用或存取，原因如上節所述。 此UI-API協調是常見的。 不過，有時使用者可能會想要透過API執行所有動作，包括設定以及結果的使用。 雖然不常見，但使用者完全可以使用API來設 *定、執行* ，並運用建議的結果。

我們在前面的 [章節中](manage-catalog.md) ，學習了如何管理Adobe Target Recommendations實體並在伺服器端提供。 同樣地，Adobe I/O可讓您管理標準、促銷、系列和設計範本，而不需登入Adobe Target。 所有API的完整清 [!DNL Recommendations] 單可在此 [處找到](http://developers.adobetarget.com/api/recommendations/)，但以下是摘要供參考。

| 資源 | 詳細資料 |
| --- | --- |
| [集合](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | 列出、建立、取得、編輯和刪除系列。 |
| [標準](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | 列出並取得標準。 |
| [設計](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | 列出、建立、取得、編輯、刪除和驗證設計。 |
| [實體](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | 儲存、刪除及取得實體。 |
| [促銷活動](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | 列出、建立、取得、編輯和刪除促銷活動。 |
| [類別條件](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | 列出、建立、取得、編輯和刪除類別標準。 |
| [自訂條件](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | 列出、建立、取得、編輯和刪除自訂准則。 |
| [項目標準](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | 列出、建立、取得、編輯和刪除項目標準。 |
| [人氣標準](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | 列出、建立、取得、編輯和刪除人氣標準。 |
| [描述檔屬性條件](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | 列出、建立、取得、編輯和刪除描述檔屬性條件。 |
| [最近的條件](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | 列出、建立、取得、編輯和刪除最新標準。 |
| [序列條件](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | 列出、建立、取得、編輯和刪除序列標準。 |

## 參考檔案

* [Adobe Target API檔案](https://developers.adobetarget.com/api/#getting-started)
* [Adobe Target傳送API](https://developers.adobetarget.com/api/delivery-api/)
* [與電子 [!DNL Recommendations] 郵件整合](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## 摘要和審查

恭喜！ 在完成本教學課程後，您已學習如何：
* [使用Recommendations API管理您的目錄](manage-catalog.md)
* [使用Recommendations API管理自訂條件](manage-custom-criteria.md)
* [搭配Recommendations使用傳送API](fetch-recs-server-side-delivery-api.md)
