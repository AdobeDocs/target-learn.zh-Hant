---
title: 如何使用交付API獲取Recommendations
description: 本教程的這一部分指導開發人員完成使用Adobe Target交付API獲取建議內容所需的步驟。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 553d1208-647f-479d-acc7-d7760469d642
source-git-commit: 0ecfde208b3e201de135512d5aab70192fc2b826
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 1%

---

# 正在獲取 [!DNL Recommendations] 與交付API

Adobe Target和Adobe Target [!DNL Recommendations] API可用於傳遞對網頁的響應，但也可用於非基於HTML的體驗，包括應用、螢幕、控制台、電子郵件、資訊亭和其他顯示設備。 換句話說，當 [!DNL Target] 庫和JavaScript不能使用， **[!DNL Target]傳遞API** 仍然允許我們訪問 [!DNL Target] 提供個性化體驗的功能。

>[!NOTE]
>
> 當請求包含實際建議（推薦的產品或項目）的內容時，請使用 [!DNL Target] 傳遞API。

要檢索建議，請發送具有相應上下文資訊的Adobe Target交付APIPOST調用，該調用可能包括用戶ID（用於特定於概要檔案的建議，如用戶最近查看的項目）、相關的mbox名稱、mbox參數、配置檔案參數或其他屬性。 響應將包括推薦的entity.id（並可能包括其他實體資料），其格式為JSON或HTML，然後可以在設備中顯示。

的 [傳遞API](https://developer.adobe.com/target/implement/delivery-api/)Adobe Target的{target=_blank}公開了標準 [!DNL Target] 請求提供。

>[!NOTE]
>傳遞API:
>* 使您能夠以REST風格檢索位置和受眾的體驗或優惠。
>* 不需要身份驗證。
>* 僅開機自檢。
>* 不處理Cookie或重定向呼叫。
>* 不需要或識別「用戶角色」。 它只是將內容或報告事件提取到 [!DNL Target] 邊緣伺服器。


使用交付API交付 [!DNL Target] 經驗 — 包括建議 — 遵循以下步驟：

1. 建立 [!DNL Target] 活動(A/B、XT、AP或 [!DNL Recommendations])使用基於表單的作曲家（而不是視覺體驗作曲家）。
2. 使用「傳遞API」獲取由 [!DNL Target] 的子菜單。

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## 使用基於表單的經驗編寫器建立建議

要建立可與交付API一起使用的建議，請使用 [基於表單的作曲家](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en)。

1. 首先，建立並保存基於JSON的設計，以便在您的建議中使用。 有關JSON示例，以及配置基於表單的活動時如何返回JSON響應的背景資訊，請參閱上的文檔 [建立建議設計](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html?lang=en)。 在本示例中，該設計名為 *簡單JSON。*

   ![伺服器端建立 — recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. 在 [!DNL Target]，導航 **[!UICONTROL 活動] > [!UICONTROL 建立活動] > [!UICONTROL Recommendations]**，然後選擇 **[!UICONTROL 窗體]**。

   ![伺服器端create-recs.png](assets/server-side-create-recs.png)

3. 選擇屬性，然後按一下 **[!UICONTROL 下一個]**。
4. 定義希望用戶接收建議響應的位置。 下面的示例使用名為 *api_charter*。 選擇基於JSON的設計，以前建立，名為 *簡單JSON。*
   ![伺服器端create-recs-form.png](assets/server-side-create-recs-form1.png)
5. 保存並激活建議。 會產生結果。 [結果準備好後](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html?lang=en)，可以使用「傳遞API」來檢索它們。

## 使用交付API

的語法 [傳遞API](https://developer.adobe.com/target/implement/delivery-api/#tag/Delivery-API){target=_blank為：

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. 請注意，客戶端代碼是必填項。 作為提醒，您的客戶端代碼可導航至Adobe Target **[!UICONTROL Recommendations] > [!UICONTROL 設定]**。 注意 **[!UICONTROL 客戶端代碼]** 值 **[!UICONTROL 建議API令牌]** 的子菜單。
   ![客戶端代碼.png](assets/client-code.png)
1. 一旦您擁有了客戶端代碼，就構造您的交付API調用。 下面的示例以 **[!UICONTROL Web批處理Mboxs傳遞API調用]** 提供 [傳遞APIPostman集合](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)、進行相關修改。 例如：
   * 這樣 **瀏覽器** 和 **地址** 對象已從 **身體**，因為非HTML使用案例不需要這些
   * *api_charter* 列為此示例中的位置名稱
   * 已指定entity.id，因為此建議基於內容相似性，它要求將當前項項項傳遞到 [!DNL Target]。
      ![伺服器端傳遞 — API-call.png](assets/server-side-delivery-api-call2.png)
切記正確配置查詢參數。 例如，請務必指定 
`{{CLIENT_CODE}}` 必要時。 <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![客戶端代碼3](assets/client-code3.png)
1. 發送請求。 執行 *api_charter* 位置，該位置上運行活動的建議，它使用您的JSON設計定義，將輸出推薦實體清單。
1. 根據JSON設計接收響應。
   ![伺服器端建立 — recs-json-response2.png](assets/server-side-create-recs-json-response2.png)
響應包括密鑰ID以及建議實體的實體ID。

將Delivery API與 [!DNL Recommendations] 這樣，在向非HTML設備上的訪問者顯示建議之前，您就可以執行其他步驟。 例如，您可以利用Delivery API的響應，在顯示最終結果之前，從另一個系統（如CMS、PIM或電子商務平台）對實體屬性詳細資訊（庫存、價格、評級等）執行附加的即時查找。

使用本教程中概述的方法，您可以獲取任何應用程式以利用 [!DNL Target] 提供個性化推薦！

## 範例實施

以下資源提供了各種非HTML型實施的示例。 請記住，由於涉及的系統和設備，每個實施都是獨特的。

| 資源 | 詳細資料 |
| --- | --- |
| [Adobe Target各地 — 在IoT中實施伺服器端](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit2019 Lab，為利用Adobe Target伺服器端API的React應用程式提供實際操作體驗。 |
| [Adobe Target在沒有AdobeSDK的移動應用中](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | 本指南介紹如何在不安裝AdobeSDK的情況下在移動應用中設定Adobe Target。 此解決方案使用Tealium SDK網頁視圖和遠程命令模組向Adobe訪問者API(Experience Cloud)和Adobe TargetAPI發送和接收請求。 |
| [Adobe Target如何在移動應用中工作](https://experienceleague.adobe.com/docs/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html?lang=en) | 如何 [!DNL Target] 與移動SDK一起使用 |
| [配置 [!DNL Target] Experience Platform Launch延伸與實施 [!DNL Target] API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | 配置 [!DNL Target] Experience Platform Launch中的擴展，添加 [!DNL Target] 應用的擴展和實施 [!DNL Target] 請求活動、預回遷優惠和進入可視預覽模式的API。 |
| [Adobe Target節點客戶端](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | 開源 [!DNL Target] Node.js SDK v1.0 |
| [伺服器端概述](https://experienceleague.adobe.com/docs/target/using/implement-target/server-side/api-and-sdk-overview.html?lang=en) | 有關Adobe Target伺服器端交付API、伺服器端批處理交付API、Node.js SDK和Adobe Target的資訊 [!DNL Recommendations] API。 |
| [Adobe Campaign電子郵件內容Recommendations](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | 描述如何通過Adobe Target和Adobe I/O Runtime在Adobe Campaign利用電子郵件中的內容建議的部落格。 |

## 管理 [!DNL Recommendations] 使用API設定

大多數時候，建議在Adobe TargetUI中配置，然後使用或通過 [!DNL Target] API，原因如上節所述。 此UI-API協調是通用的。 但是，有時用戶可能希望通過API執行所有操作，包括設定和結果的使用。 雖然不常見，但用戶絕對可以配置，執行， *和* 完全使用API來利用建議的結果。

我們在 [早期部分](https://developer.adobe.com/target/before-administer/recs-api/manage-catalog/){target=_blank}如何管理Adobe TargetRecommendations實體並將其提供到伺服器端。 同樣，Adobe I/O允許您管理標準、促銷、收藏和設計模板，而無需登錄Adobe Target。 完整清單 [!DNL Recommendations] 可能找到API [這裡](https://developers.adobetarget.com/api/recommendations/)，但是這裡有一個摘要供參考。

| 資源 | 詳細資料 |
| --- | --- |
| [集合](https://developers.adobetarget.com/api/recommendations/#tag/Collections) | 列出、建立、獲取、編輯和刪除集合。 |
| [條件](https://developers.adobetarget.com/api/recommendations/#tag/Criteria) | 列出並獲取條件。 |
| [設計](https://developers.adobetarget.com/api/recommendations/#tag/Designs) | 列出、建立、獲取、編輯、刪除和驗證設計。 |
| [實體](https://developers.adobetarget.com/api/recommendations/#tag/Entities) | 保存、刪除和獲取實體。 |
| [促銷](https://developers.adobetarget.com/api/recommendations/#tag/Promotions) | 列出、建立、獲取、編輯和刪除促銷。 |
| [類別標準](https://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | 列出、建立、獲取、編輯和刪除類別條件。 |
| [自定義條件](https://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | 列出、建立、獲取、編輯和刪除自定義條件。 |
| [物料條件](https://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | 列出、建立、獲取、編輯和刪除項目條件。 |
| [受歡迎度標準](https://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | 列出、建立、獲取、編輯和刪除流行標準。 |
| [配置檔案屬性條件](https://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | 列出、建立、獲取、編輯和刪除配置檔案屬性條件。 |
| [最近的條件](https://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | 列出、建立、獲取、編輯和刪除最近的條件。 |
| [序列標準](https://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | 列出、建立、獲取、編輯和刪除序列條件。 |

## 參考文檔

* [Adobe Target管理API文檔](https://developer.adobe.com/target/administer/admin-api/){target=_blank}
* [Adobe Target交付API](https://developer.adobe.com/target/implement/delivery-api/){target=_blank}
* [將 [!DNL Recommendations] 與電子郵件整合](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## 摘要和審閱

恭喜！ 完成本教程後，您已學習了如何：
* [使用RecommendationsAPI管理目錄](https://developer.adobe.com/target/before-administer/recs-api/manage-catalog/){target=_blank}
* [使用RecommendationsAPI管理自定義條件](https://developer.adobe.com/target/before-administer/recs-api/manage-custom-criteria/){target=_blank}
* [將交付API與Recommendations](https://developer.adobe.com/target/before-administer/recs-api/fetch-recs-server-side-delivery-api/){target=_blank}
