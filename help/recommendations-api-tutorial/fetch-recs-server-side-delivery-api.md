---
title: 如何使用傳送API擷取Recommendations
description: 本教學課程的本部分會引導開發人員完成使用Adobe Target傳送API擷取建議內容所需的步驟。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 553d1208-647f-479d-acc7-d7760469d642
source-git-commit: d1517f0763290eb61a9e4eef4f2eb215a9cdd667
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 2%

---

# 使用傳送API擷取[!DNL Recommendations]

Adobe Target和Adobe Target [!DNL Recommendations] API可用來傳送對網頁的回應，但也可用於非HTML型體驗，包括應用程式、螢幕、主控台、電子郵件、資訊站和其他顯示裝置。 換言之，當[!DNL Target]程式庫和JavaScript無法使用時，**[!DNL Target]傳送API**&#x200B;仍可讓我們存取完整的[!DNL Target]功能範圍，以提供個人化體驗。

>[!NOTE]
>
> 請求包含實際建議（建議產品或項目）的內容時，請使用[!DNL Target]傳送API。

若要擷取建議，請傳送包含適當內容資訊的Adobe Target傳送APIPOST呼叫，其中可能包括使用者ID(以便與設定檔專屬的建議（例如使用者最近檢視的項目）、相關mbox名稱、mbox參數、設定檔參數或其他屬性。 回應將包含建議的entity.ids（且可能包含其他實體資料），其格式為JSON或HTML，然後可在裝置中顯示。

Adobe Target的[傳送API](https://developers.adobetarget.com/api/delivery-api/)會公開標準[!DNL Target]請求提供的所有現有功能。

>[!NOTE]
>傳送API:
>* 可讓您以RESTful方式擷取位置和對象的體驗或選件。
>* 不需要驗證。
>* 僅POST。
>* 不會處理Cookie或重新導向呼叫。
>* 不需要或識別「使用者角色」。 它只會擷取內容或報告事件至[!DNL Target]邊緣伺服器。


若要使用傳送API來傳送[!DNL Target]體驗（包括建議），請遵循下列步驟：

1. 使用表單式撰寫器（非可視化體驗撰寫器）建立[!DNL Target]活動（A/B、XT、AP或[!DNL Recommendations]）。
2. 使用傳送API來取得您剛建立之[!DNL Target]活動所產生請求的回應。

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## 使用表單式體驗撰寫器建立建議

若要建立可與傳送API搭配使用的建議，請使用[表單式撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en)。

1. 首先，建立並儲存要在建議中使用的JSON型設計。 如需範例JSON，以及設定表單式活動時如何傳回JSON回應的背景資訊，請參閱[建立建議設計](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html?lang=en)上的檔案。 在此範例中，設計名為&#x200B;*Simple JSON.*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. 在[!DNL Target]中，導覽至&#x200B;**[!UICONTROL 活動] > [!UICONTROL 建立活動] > [!UICONTROL Recommendations]**，然後選取&#x200B;**[!UICONTROL 表單]**。

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. 選擇屬性，然後按一下&#x200B;**[!UICONTROL Next]**。
4. 定義您希望使用者接收建議回應的位置。 以下範例使用名為&#x200B;*api_charter*&#x200B;的位置。 選取您先前建立的JSON型設計，名為&#x200B;*簡單JSON。*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. 儲存並啟動建議。 會產生結果。 [結果準備就緒後](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html?lang=en)，您就可以使用傳送API來擷取它們。

## 使用傳送API

[傳送API](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API)的語法為：

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. 請注意，用戶端代碼為必要項目。 提醒您，您可以導覽至&#x200B;**[!UICONTROL Recommendations] > [!UICONTROL 設定]**，在Adobe Target中找到您的用戶端代碼。 記下「**[!UICONTROL 建議API Token]**」區段中的「**[!UICONTROL 用戶端代碼]**」值。
   ![client-code.png](assets/client-code.png)
1. 取得用戶端程式碼後，建立您的傳送API呼叫。 以下範例以[傳送API Postman集合](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)中提供的&#x200B;**[!UICONTROL Web批次Mbox傳送API呼叫]**&#x200B;開頭，進行相關修改。 例如：
   * 已從&#x200B;**Body**&#x200B;中移除&#x200B;**browser**&#x200B;和&#x200B;**address**&#x200B;物件，因為這些物件對於非HTML使用案例並非必要項目
   * *api_* charter在此範例中列為位置名稱
   * entity.id已指定，因為此建議以內容相似度為基礎，而內容相似度要求將目前項目索引鍵傳遞至[!DNL Target]。
      ![server-side-Delivery-API-call.](assets/server-side-delivery-api-call2.png)
pngRemember可正確設定查詢參數。例如，請務必指定 
`{{CLIENT_CODE}}`。<!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. 傳送要求。 這會針對&#x200B;*api_charter*&#x200B;位置執行，其上會執行作用中建議，並以您的JSON設計定義，並輸出建議實體的清單。
1. 根據JSON設計接收回應。
   ![server-side-create-recs-json-response2.](assets/server-side-create-recs-json-response2.png)
png回應包含索引鍵ID，以及建議實體的實體ID。

透過此方式使用具有[!DNL Recommendations]的傳送API，可讓您在非HTML裝置上向訪客顯示建議之前，先執行其他步驟。 例如，您可以取得傳送API的回應，在顯示最終結果之前，先從其他系統（例如CMS、PIM或電子商務平台）執行額外的即時查詢實體屬性詳細資訊（庫存、價格、評等等）。

使用本教學課程中概述的方法，您可以讓任何應用程式運用[!DNL Target]的回應，提供個人化建議！

## 範例實施

下列資源提供各種非HTML型實作的範例。 請記得，由於涉及的系統和裝置，每個實作都會是唯一的。

| 資源 | 詳細資料 |
| --- | --- |
| [Adobe Target Everywhere — 在IoT中實施伺服器端或](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit2019實驗，為採用Adobe Target伺服器端API的React應用程式提供實作體驗。 |
| [Adobe Target(在不使用AdobeSDK的行動應用程式中)](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | 本指南會說明如何在行動應用程式中設定Adobe Target，而不安裝AdobeSDK。 此解決方案使用Tealium SDK webview和Remote Commands模組，傳送和接收Adobe訪客API(Experience Cloud)和Adobe Target API的要求。 |
| [Adobe Target在行動應用程式中如何運作](https://experienceleague.adobe.com/docs/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html?lang=en) | [!DNL Target]如何與行動SDK搭配運作 |
| [設 [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] 定API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | 在Experience Platform Launch中設定[!DNL Target]擴充功能、將[!DNL Target]擴充功能新增至您的應用程式，以及實作[!DNL Target] API以請求活動、預先擷取選件及進入視覺預覽模式的步驟。 |
| [Adobe Target Node Client](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | 開放來源[!DNL Target] Node.js SDK v1.0 |
| [伺服器端概觀](https://experienceleague.adobe.com/docs/target/using/implement-target/server-side/api-and-sdk-overview.html?lang=en) | Adobe Target伺服器端傳送API、伺服器端批次傳送API、Node.js SDK和Adobe Target [!DNL Recommendations] API的相關資訊。 |
| [Adobe Campaign內容Recommendations（電子郵件）](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | 說明如何透過Adobe Campaign中的Adobe Target和Adobe I/O Runtime，運用電子郵件內容建議的部落格。 |

## 使用API管理[!DNL Recommendations]設定

大部分時候，建議都是在Adobe Target UI中設定，然後透過[!DNL Target] API使用或存取，原因如上節所述。 此UI-API協調是常見的。 不過，有時使用者可能會想透過API執行所有動作，包括設定及使用結果。 雖然很少見，但使用者可以完全透過API設定、執行&#x200B;*和*&#x200B;運用建議的結果。

我們在[前面的章節](manage-catalog.md)了解如何管理Adobe Target Recommendations實體並在伺服器端傳送。 同樣地，「Adobe I/O」可讓您管理條件、促銷活動、集合和設計範本，而無須登入Adobe Target。 所有[!DNL Recommendations] API的完整清單可在[此處](https://developers.adobetarget.com/api/recommendations/)找到，但此處是要參考的摘要。

| 資源 | 詳細資料 |
| --- | --- |
| [集合](https://developers.adobetarget.com/api/recommendations/#tag/Collections) | 列出、建立、取得、編輯和刪除集合。 |
| [條件](https://developers.adobetarget.com/api/recommendations/#tag/Criteria) | 列出並取得條件。 |
| [設計](https://developers.adobetarget.com/api/recommendations/#tag/Designs) | 列出、建立、取得、編輯、刪除及驗證設計。 |
| [實體](https://developers.adobetarget.com/api/recommendations/#tag/Entities) | 儲存、刪除和取得實體。 |
| [促銷活動](https://developers.adobetarget.com/api/recommendations/#tag/Promotions) | 列出、建立、取得、編輯和刪除促銷活動。 |
| [類別條件](https://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | 列出、建立、取得、編輯和刪除類別條件。 |
| [自訂條件](https://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | 列出、建立、取得、編輯和刪除自訂條件。 |
| [項目條件](https://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | 列出、建立、獲取、編輯和刪除項目條件。 |
| [人氣條件](https://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | 列出、建立、取得、編輯和刪除人氣標準。 |
| [設定檔屬性條件](https://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | 列出、建立、取得、編輯和刪除設定檔屬性條件。 |
| [最近的條件](https://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | 列出、建立、取得、編輯和刪除最近的條件。 |
| [序列條件](https://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | 列出、建立、取得、編輯和刪除序列條件。 |

## 參考檔案

* [Adobe Target API檔案](https://developers.adobetarget.com/api/#getting-started)
* [Adobe Target傳送API](https://developers.adobetarget.com/api/delivery-api/)
* [ [!DNL Recommendations] 與電子郵件整合](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html?lang=en)

## 摘要和審閱

恭喜！ 完成本教學課程後，您已學會如何：
* [使用Recommendations API管理目錄](manage-catalog.md)
* [使用Recommendations API管理自訂條件](manage-custom-criteria.md)
* [將傳送API與Recommendations搭配使用](fetch-recs-server-side-delivery-api.md)
