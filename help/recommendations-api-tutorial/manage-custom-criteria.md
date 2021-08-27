---
title: 如何管理自訂條件
description: 本教學課程的本部分會引導開發人員完成使用Adobe Target API來管理、建立、列出、編輯、取得和刪除Adobe Target Recommendations條件所需的步驟。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: ee63bd3e-200a-4c08-b364-9f17a479033b
source-git-commit: d1517f0763290eb61a9e4eef4f2eb215a9cdd667
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 1%

---

# 管理自訂條件

有時，[!DNL Recommendations]提供的演算法無法呈現您要促銷的特定項目。 在這種情況下，自訂條件可讓您為指定的關鍵項目或類別提供一組特定的建議項目。 您可以定義關鍵項目或類別與建議項目之間的對應，並將該對應匯入為自訂條件。 [自訂條件檔案](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en)中會說明此程式。 如本檔案所述，您可以透過[!DNL Target]使用者介面(UI)建立、編輯和刪除自訂條件。 不過，[!DNL Target]也提供一組自訂條件API，可讓您更詳細地管理自訂條件。

>[!IMPORTANT]
>
>自訂條件請遵循以下使用准則：
>
> 使用API為指定自訂條件執行所有作業（建立、編輯、刪除），或使用UI執行所有作業（建立、編輯、刪除）。 透過UI和API的組合管理自訂條件可能會導致資訊衝突或意外的結果。 例如，在UI中建立自訂條件，但透過API編輯條件時，即使在後端更新（透過API顯示）,UI中仍不會反映您的更新。

## 建立自訂條件

若要使用[建立自訂條件API](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom)建立自訂條件，語法為：

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>使用「建立自訂條件API」建立的自訂條件（如本練習所述）會顯示在UI中，並持續存在。 您將無法從UI編輯或刪除這些項目。 您可以透過API **編輯或刪除它們**，但無論如何，它們都會繼續顯示在[!DNL Target] UI中。 若要維護從UI編輯或刪除的選項，請根據檔案[使用UI建立自訂條件，而非使用建立自訂條件API。](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en)

您必須先閱讀上述警告，並熟悉如何建立後續無法從UI刪除的新自訂條件後，才能繼續進行本教學課程。

1. 為&#x200B;**建立自訂條件**&#x200B;驗證`TENANT_ID`和`API_KEY`參考先前建立的Postman環境變數。 請使用下圖進行比較。

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. 將&#x200B;**Body**&#x200B;新增為&#x200B;**raw** JSON，定義自訂條件CSV檔案的位置。 使用[建立自訂條件API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom)檔案中提供的範例作為範本，視需要提供您的`environmentId`和其他值。 在此範例中，我們使用LAST_PURCHASED作為索引鍵。

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. 傳送要求並觀察回應，其中包含您剛建立之自訂條件的詳細資訊。

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. 若要確認自訂條件已建立，請在Adobe Target內導覽至&#x200B;**[!UICONTROL Recommendations] > [!UICONTROL 條件]**&#x200B;並依名稱搜尋條件，或在下一個步驟中使用&#x200B;**清單自訂條件API**。

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

在這種情況下，我們有錯誤。 讓我們使用&#x200B;**清單自訂條件API**&#x200B;更仔細地檢查自訂條件，以調查錯誤。

## 列出自訂條件

若要擷取所有自訂條件的清單以及每個條件的詳細資訊，請使用[清單自訂條件API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom)。 語法為：

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. 如前所述，驗證`TENANT_ID`和`API_KEY`並傳送要求。 在回應中，請注意自訂條件ID，以及先前指出之錯誤訊息的相關詳細資訊。
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

在此情況下，會因為伺服器資訊不正確而發生錯誤，這表示[!DNL Target]無法存取包含自訂條件定義的CSV檔案。 現在來編輯自訂條件以修正此問題。

## 編輯自訂條件

若要變更自訂條件定義的詳細資訊，請使用[編輯自訂條件API](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom)。 語法為：

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 如前所述，驗證`TENANT_ID`和`API_KEY`。
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. 指定您要編輯之（單一）自訂條件的條件ID。
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. 在內文中，提供已更新的JSON及正確的伺服器資訊。 （在此步驟中，指定您可存取之伺服器的FTP存取權。）
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. 傳送要求並記下回應。
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

讓我們使用&#x200B;**取得自訂條件API**&#x200B;來確認更新後的自訂條件是否成功。

## 取得自訂條件

若要檢視特定自訂條件的自訂條件詳細資訊，請使用[取得自訂條件API](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom)。 語法為：

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 指定您要取得其詳細資料的自訂條件的條件ID。 傳送要求並檢閱回應。
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. 驗證成功。 （在本例中，請確認沒有其他FTP錯誤。）
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. （選用）確認更新在UI中反映正確。
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## 刪除自訂條件

使用先前提及的條件ID，使用[刪除自訂條件API](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom)刪除您的自訂條件。 語法為：

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. 指定要刪除之（單一）自訂條件的條件ID。 按一下「**傳送**」。
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. 確認已使用取得自訂條件來刪除條件。
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)
在此情況下，預期的404錯誤表示找不到已刪除的條件。

>[!NOTE]
>提醒您，即使條件已刪除，系統也不會從[!DNL Target] UI中移除，因為該條件是使用「建立自訂條件API」建立。

恭喜！ 您現在可以使用[!DNL Recommendations] API，建立、列出、編輯、刪除及取得自訂條件的詳細資訊。 在下一節中，您將使用[!DNL Target]傳送API來擷取建議。

[下堂課「使用伺服器端傳送API擷取Recommendations」>](fetch-recs-server-side-delivery-api.md)
