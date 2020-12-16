---
title: 管理自訂條件
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
source-wordcount: '959'
ht-degree: 1%

---


# 管理自訂條件

有時，[!DNL Recommendations]提供的演算法無法呈現您要促銷的特定項目。 在這種情況下，自訂條件可讓您針對特定關鍵項目或類別提供一組特定建議項目。 您可以定義關鍵項目或類別與建議項目之間的映射，並將該映射匯入為自訂標準。 此過程在[自訂標準文檔](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html)中有說明。 如該檔案所述，您可透過[!DNL Target]使用者介面(UI)建立、編輯和刪除自訂准則。 不過，[!DNL Target]也提供一組自訂准則API，可讓您更詳細地管理自訂准則。

>[!IMPORTANT]
>
>請依照此自訂准則的使用方針：
>
> 使用API針對特定自訂准則執行所有動作（建立、編輯、刪除），或使用UI執行所有動作（建立、編輯、刪除）。 透過UI和API的組合管理自訂准則可能會導致資訊衝突或意外結果。 例如，在UI中建立自訂准則，但透過API進行編輯，將不會反映您在UI中的更新，即使它會在後端更新，如透過API所見。

## 建立自訂條件

若要使用[建立自訂准則API](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom)建立自訂准則，語法為：

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>如本練習所述，使用「建立自訂准則API」建立的自訂准則會顯示在UI中，並持續存在。 您將無法從UI中編輯或刪除這些項目。 您可以透過API **編輯或刪除它們，但無論如何，它們都會繼續出現在** UI中。 [!DNL Target]若要維持從UI編輯或刪除的選項，請依照檔案[的UI建立自訂准則，而非使用「建立自訂准則API」。](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html)

請等到您閱讀上述警告並樂於建立無法從UI刪除的新自訂准則後，再繼續本教學課程。

1. 驗證`TENANT_ID`和`API_KEY`的&#x200B;**建立自定義條件**&#x200B;引用先前建立的郵遞員環境變數。 請使用下列影像進行比較。

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. 將&#x200B;**Body**&#x200B;新增為&#x200B;**raw** JSON，以定義自訂准則CSV檔案的位置。 使用[建立自訂准則API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom)檔案中提供的範例做為範本，視需要提供您的`environmentId`和其他值。 在此範例中，我們使用LAST_PURCHASED作為索引鍵。

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. 傳送請求並觀察回應，回應中包含您剛建立之自訂准則的詳細資訊。

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. 若要確認已建立自訂准則，請在Adobe Target中導覽至&#x200B;**[!UICONTROL Recommendations] > [!UICONTROL Criteria]**，並依名稱搜尋准則，或在下一步驟中使用&#x200B;**清單自訂准則API**。

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

在這種情況下，我們有個錯誤。 讓我們使用&#x200B;**清單自訂准則API**&#x200B;更仔細地檢查自訂准則，以調查錯誤。

## 清單自訂條件

若要擷取所有自訂准則的清單以及每個准則的詳細資訊，請使用[清單自訂准則API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom)。 語法為：

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. 如前所述，驗證`TENANT_ID`和`API_KEY`，並傳送請求。 在回應中，請注意自訂准則ID，以及前面已指出的錯誤訊息的詳細資訊。
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

在此情況下，發生錯誤的原因是伺服器資訊不正確，這表示[!DNL Target]無法訪問包含自定義標準定義的CSV檔案。 讓我們編輯自訂條件以修正此問題。

## 編輯自訂條件

若要變更自訂准則定義的詳細資訊，請使用[編輯自訂准則API](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom)。 語法為：

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 如前所述，檢驗`TENANT_ID`和`API_KEY`。
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. 指定要編輯的（單一）自訂准則的准則ID。
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. 在「內文」中，提供已更新的JSON及正確的伺服器資訊。 （對於此步驟，指定您可存取之伺服器的FTP存取權。）
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. 傳送請求並記下回應。
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

讓我們使用&#x200B;**取得自訂准則API**&#x200B;來驗證更新的自訂准則是否成功。

## 取得自訂條件

若要檢視特定自訂准則的自訂准則詳細資訊，請使用[取得自訂准則API](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom)。 語法為：

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 指定您要取得其詳細資訊的自訂准則的准則ID。 傳送請求，並檢閱回應。
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. 確認成功。 （在本例中，請確認沒有其他FTP錯誤。）
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. （可選）驗證更新是否正確反映在UI中。
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## 刪除自訂條件

使用前面注明的標準ID，使用[刪除自訂標準API](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom)刪除自訂標準。 語法為：

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 指定要刪除的（單一）自訂准則的准則ID。 按一下「**傳送**」。
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. 使用「取得自訂准則」確認已刪除准則。
   ![DeleteCustomCriteria2在](assets/DeleteCustomCriteria2.png)
此情況下，預期的404錯誤表示找不到已刪除的條件。

>[!NOTE]
>提醒您，即使刪除了[!DNL Target] UI，該准則仍不會從中移除，因為它是使用「建立自訂准則API」建立的。

恭喜！ 您現在可以使用[!DNL Recommendations] API，建立、列出、編輯、刪除及取得自訂准則的詳細資訊。 在下一節中，您將使用[!DNL Target]傳送API來擷取建議。

[下一個「使用伺服器端傳送API擷取建議」>](fetch-recs-server-side-delivery-api.md)
