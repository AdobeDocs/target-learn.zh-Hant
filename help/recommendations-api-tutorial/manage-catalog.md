---
title: 使用API管理您的Recommendations目錄
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
source-wordcount: '931'
ht-degree: 1%

---


# 使用API管理[!DNL Recommendations]目錄

目前，您已學習如何使用JWT驗證流程產生存取Token，以搭配Adobe I/O使用Adobe Target管理API。

您可以使用[Recommendations API](https://developers.adobetarget.com/api/recommendations/)來新增、更新或刪除建議目錄中的項目。 和其他Adobe Target管理API一樣，[!DNL Recommendations] API需要驗證。

>[!TIP]
>
>傳送&#x200B;**[!UICONTROL IMS:JWT只要您需要重新整理存取Token以進行驗證，就會透過使用者Token]**&#x200B;產生+驗證請求，因為它會在24小時後過期。 如需指示，請參閱[設定Adobe API驗證](../apis/configure-io-target-integration.md)。

![JWT3ff](assets/configure-io-target-jwt3ff.png)

>[!NOTE]
>
>繼續之前，請先取得[Recommendations Postman系列](https://developers.adobetarget.com/api/recommendations/#section/Postman)。

## 使用「儲存實體API」建立和更新項目

若要使用API填入[!DNL Recommendations]產品資料庫，而不是使用CSV產品饋送或[!DNL Target]要求在產品頁面上引發，請使用[儲存實體API](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities)。 此請求會在單一[!DNL Target]環境中新增或更新項目。 語法為：

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

例如，「儲存實體」可用於在符合特定臨界值（例如庫存或價格臨界值）時更新項目，以標籤這些項目並防止建議它們。

1. 導覽至「**[!DNL Target]> [!UICONTROL Setup] > [!UICONTROL Hosts] > [!UICONTROL Environments]**」，以取得您要新增或更新項目的[!DNL Target] Environment ID。

   ![SaveEntitys1](assets/SaveEntities01.png)

2. 驗證`TENANT_ID`和`API_KEY`是否引用先前建立的Postman環境變數。 請使用下列影像進行比較。 如有必要，請修改API請求中的標題和路徑，以符合下圖中的標題和路徑。

   ![SaveEntities3](assets/SaveEntities03.png)

3. 在&#x200B;**Body**&#x200B;中，將您的JSON輸入為&#x200B;**raw**&#x200B;程式碼。 不要忘記使用`environment`變數來指定您的環境ID。 （在以下範例中，環境ID為6781。）

   ![SaveEntities4.png](assets/SaveEntities04.png)

   >!![NOTE]
   以下是範例JSON，將entity.id kit2001與烤箱產品的相關實體值新增至環境6781。

   ```
      {
      "entities": [{
              "name": "Toaster Oven",
              "id": "kit2001",
              "environment": 6781,
              "categories": [
                  "housewares:appliances"
              ],
              "attributes": {
                  "inventory": 77,
                  "margin": 23,
                  "message": "crashing helicopter",
                  "pageUrl": "www.foobar.foo.com/helicopter.html",
                  "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                  "value": 19.2
              }
          }]
      }
   ```

4. 按一下「**傳送**」。您應收到下列回應。

   ![SaveEntities5.png](assets/SaveEntities05.png)

JSON物件可縮放以傳送多個產品。 例如，此JSON指定兩個實體。

```
    {
        "entities": [{
                "name": "Toaster Oven",
                "id": "kit2001",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 89,
                    "margin": 11,
                    "message": "Toaster Oven",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 102.5
                }
            },
            {
                "name": "Blender",
                "id": "kit2002",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 36,
                    "margin": 5,
                    "message": "Blender",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 54.5
                }
            }
        ]
    }
```

1. 現在該你了！ 使用&#x200B;**儲存實體** API，將下列項目新增至目錄。 以上範例JSON為起點。 （您需要擴充JSON以包含其他實體。）

   ![SaveEntities6.png](assets/SaveEntities06.png)

哇，看來最後兩件東西不屬於。 讓我們使用&#x200B;**Get Entity** API來檢查這些項目，並視需要使用&#x200B;**Delete Entities** API來刪除這些項目。

## 使用Get Entity API取得項目詳細資訊

若要擷取現有項目的詳細資料，請使用[取得實體API](https://developers.adobetarget.com/api/recommendations/#operation/getEntity)。 語法為：

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

一次只能檢索單個圖元的實體詳細資訊。 您可以使用「取得實體」來確認目錄中的更新是否如預期般進行，或以其他方式審核目錄內容。

1. 在API請求中，使用變數`entityId`指定實體ID。 下列範例將傳回其entityId=kit2004之實體的詳細資料。

   ![GetEntity1](assets/GetEntity1.png)

2. 驗證`TENANT_ID`和`API_KEY`是否引用先前建立的Postman環境變數。 請使用下列影像進行比較。 如有必要，請修改API請求中的標題和路徑，以符合下圖中的標題和路徑。

   ![GetEntity2](assets/GetEntity2.png)

3. 傳送請求。

   ![GetEntity3](assets/GetEntity3.png)
如果您收到錯誤，指出找不到實體，如上例所示，請確認您是否將請求送出至正確的 [!DNL Target] 環境。

   >[!NOTE]
   如果未明確指定任何環境，則「獲取實體」僅會嘗試從[預設環境](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html#section_4F8539B07C0C45E886E8525C344D5FB0)獲取實體。 如果要從預設環境以外的任何環境提取，必須指定環境ID。

4. 如有必要，請新增`environmentId`參數，然後重新傳送請求。

   ![GetEntity4](assets/GetEntity4.png)

5. 傳送另一個&#x200B;**Get Entity**&#x200B;請求，此時檢查entityId=kit2005的實體。

   ![GetEntity5](assets/GetEntity5.png)

假設您決定必須從目錄中移除這些實體。 讓我們使用&#x200B;**刪除實體** API。

## 使用刪除實體API刪除項目

若要從目錄中移除項目，請使用[刪除實體API](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities)。 語法為：

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
此API會刪除您指定之ID所參照的實體。
如果未提供實體ID，則會刪除指定環境中的所有實體。 如果未提供環境ID，則會從所有環境中刪除實體。 小心使用！

1. 導覽至「**[!DNL Target]> [!UICONTROL Setup] > [!UICONTROL Hosts] > [!UICONTROL Environments]**」，以取得您要從中刪除項目的[!DNL Target] Environment ID。

   ![DeleteEntitys1](assets/SaveEntities01.png)

2. 在API請求中，使用語法`&ids=[comma-delimited-entity-ids]`（查詢參數），指定您要刪除之實體的實體ID。 刪除多個實體時，請使用逗號分隔ID。

   ![DeleteEntities2](assets/DeleteEntities2.png)

3. 使用語法`&environment=[environmentId]`指定環境ID，否則將刪除所有環境中的實體。

   ![DeleteEntities3](assets/DeleteEntities3.png)

4. 驗證`TENANT_ID`和`API_KEY`是否引用先前建立的Postman環境變數。 請使用下列影像進行比較。 如有必要，請修改API請求中的標題和路徑，以符合下圖中的標題和路徑。

   ![DeleteEntities4](assets/DeleteEntities4.png)

5. 傳送請求。

   ![DeleteEntitys5](assets/DeleteEntities5.png)

6. 使用&#x200B;**Get Entity**&#x200B;驗證結果，此時應指出找不到已刪除的實體。

   ![DeleteEntitys6](assets/DeleteEntities6.png)

   ![DeleteEntitys6](assets/DeleteEntities7.png)

恭喜！ 您現在可以使用[!DNL Recommendations] API來建立、更新、刪除和取得目錄中實體的詳細資訊。 在下一節，您將學習如何管理自訂准則。

[下一個「管理自訂條件」>](manage-custom-criteria.md)
