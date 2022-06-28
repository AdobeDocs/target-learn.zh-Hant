---
title: 如何管理自定義標準
description: 本教程的這一部分將指導開發人員完成使用Adobe TargetAPI管理、建立、列出、編輯、獲取和刪除Adobe TargetRecommendations標準所需的步驟。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: ee63bd3e-200a-4c08-b364-9f17a479033b
source-git-commit: 0ecfde208b3e201de135512d5aab70192fc2b826
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 1%

---

# 管理自定義條件

有時，由 [!DNL Recommendations] 無法顯示要升級的特定項目。 在這種情況下，自定義條件提供了一種為給定關鍵項目或類別提供一組特定建議項目的方法。 您可以定義關鍵項或類別與建議項之間的映射，並將該映射作為自定義標準導入。 此過程在 [自定義條件文檔](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en)。 如該文檔中所述，您可以通過 [!DNL Target] 用戶介面(UI)。 但是， [!DNL Target] 還提供了一組自定義標準API，允許對自定義標準進行更詳細的管理。

>[!IMPORTANT]
>
>請遵循以下自定義標準的使用准則：
>
> 使用API對給定自定義條件執行所有操作（建立、編輯、刪除），或使用UI執行所有操作（建立、編輯、刪除）。 通過UI和API的組合管理自定義條件可能會導致資訊衝突或意外結果。 例如，在UI中建立自定義條件，但隨後通過API編輯它將不會反映您在UI中的更新，即使它將在後端進行更新，如通過API可見的那樣。

## 建立自定義條件

使用 [建立自定義條件API](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom)，語法為：

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>如本練習所述，使用「建立自定義標準API」建立的自定義標準將出現在UI中，這些標準將保留在UI中。 您將無法從UI中編輯或刪除它們。 您可以編輯或刪除它們 **通過API**&#x200B;但不管怎樣，它們都會繼續出現 [!DNL Target] UI。 要維護UI中的編輯或刪除選項，請使用UI建立自定義條件 [文檔](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en)，而不是使用「建立自定義條件API」。

只有在您閱讀了上面的警告後，才能繼續本教程，並且能夠輕鬆地建立新的自定義條件，這些條件隨後無法從UI中刪除。

1. 驗證 `TENANT_ID` 和 `API_KEY` 為 **建立自定義條件** 參考先前建立的Postman環境變數。 使用下面的影像進行比較。

   ![建立自定義條件1](assets/CreateCustomCriteria1.png)

2. 添加 **身體** 如 **生** 定義自定義條件CSV檔案位置的JSON。 使用中提供的示例 [建立自定義條件API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) 文檔作為模板，提供 `environmentId` 和其他必要的價值。 在此示例中，我們使用LAST_PRECHAILED作為鍵。

   ![建立自定義條件2](assets/CreateCustomCriteria2.png)

3. 發送請求並觀察響應，該響應包含您剛剛建立的自定義條件的詳細資訊。

   ![建立自定義條件3](assets/CreateCustomCriteria3.png)

4. 要驗證是否已建立自定義條件，請在Adobe Target內導航到 **[!UICONTROL Recommendations] > [!UICONTROL 標準]** 按名稱搜索條件，或使用 **列出自定義條件API** 的上界。

   ![建立自定義條件4](assets/CreateCustomCriteria4.png)

在這種情況下，我們有個錯誤。 讓我們使用 **列出自定義條件API**。

## 列出自定義條件

要檢索所有自定義條件的清單以及每個條件的詳細資訊，請使用 [列出自定義條件API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom)。 語法為：

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. 驗證 `TENANT_ID` 和 `API_KEY` 像以前一樣，發送請求。 在響應中，請注意自定義條件ID以及前面提到的錯誤消息的詳細資訊。
   ![清單自定義條件](assets/ListCustomCriteria.png)

在這種情況下，由於伺服器資訊不正確，因此出現錯誤 [!DNL Target] 無法訪問包含自定義條件定義的CSV檔案。 讓我們編輯自定義條件以更正此問題。

## 編輯自定義條件

要更改自定義條件定義的詳細資訊，請使用 [編輯自定義條件API](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom)。 語法為：

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 驗證 `TENANT_ID` 和 `API_KEY`的雙曲餘切值。
   ![編輯自定義條件1](assets/EditCustomCriteria1.png)

1. 指定要編輯的（單個）自定義條件的條件ID。
   ![編輯自定義條件2](assets/EditCustomCriteria2.png)

1. 在正文中，提供具有正確伺服器資訊的更新的JSON。 （對於此步驟，指定對可訪問的伺服器的FTP訪問。）
   ![編輯自定義條件3](assets/EditCustomCriteria3.png)

1. 發送請求並記錄響應。
   ![編輯自定義條件4](assets/EditCustomCriteria4.png)

讓我們使用 **獲取自定義條件API**。

## 獲取自定義條件

要查看特定自定義條件的自定義條件詳細資訊，請使用 [獲取自定義條件API](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom)。 語法為：

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 指定要獲取其詳細資訊的自定義條件的條件ID。 發送請求，並查看響應。
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. 驗證成功。 （在本例中，驗證是否再有FTP錯誤。）
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. （可選）驗證更新在UI中是否正確反映。
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## 刪除自定義條件

使用前面提到的條件ID，使用 [刪除自定義條件API](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom)。 語法為：

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 指定要刪除的（單個）自定義條件的條件ID。 按一下「**傳送**」。
   ![刪除自定義條件1](assets/DeleteCustomCriteria1.png)

1. 驗證是否已使用「獲取自定義條件」刪除了條件。
   ![刪除自定義條件2](assets/DeleteCustomCriteria2.png)
在這種情況下，預期的404錯誤表示找不到刪除的條件。

>[!NOTE]
>作為提醒，不會從 [!DNL Target] UI，即使它被刪除，因為它是使用「建立自定義條件API」建立的。

恭喜！ 現在，您可以使用 [!DNL Recommendations] API。 在下一節中，您將使用 [!DNL Target] 提供API以檢索建議。

[下一個「使用伺服器端交付API獲取Recommendations」 >](https://developer.adobe.com/target/before-administer/recs-api/fetch-recs-server-side-delivery-api/){target=_blank}
