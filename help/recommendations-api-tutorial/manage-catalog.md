---
title: 如何使用API管理Recommendations目錄
description: 本教學課程的本部分會引導開發人員完成使用Adobe Target API來建立、更新、儲存、取得和刪除您Recommendations目錄中的實體所需的步驟。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 8060b69b-e8e5-4fe7-895f-742410d8ed45
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 2%

---

# 使用API管理[!DNL Recommendations]目錄

此時，您已學習如何使用JWT驗證流程產生存取權杖，以搭配Adobe I/O使用Adobe Target Admin API。

您可以使用[Recommendations API](https://developers.adobetarget.com/api/recommendations/)來新增、更新或刪除建議目錄中的項目。 和其他Adobe Target Admin API一樣，[!DNL Recommendations] API需要驗證。

>[!TIP]
>
>傳送&#x200B;**[!UICONTROL IMS:每當您需要重新整理存取權杖以進行驗證時，JWT會透過使用者權杖]**&#x200B;產生+驗證請求，因為它會在24小時後到期。 如需指示，請參閱[設定AdobeAPI驗證](../apis/configure-io-target-integration.md) 。

![JWT3ff](assets/configure-io-target-jwt3ff.png)

>[!NOTE]
>
>繼續操作之前，請獲取[Recommendations Postman集合](https://developers.adobetarget.com/api/recommendations/#section/Postman)。

## 使用儲存實體API建立和更新項目

若要使用API填入您的[!DNL Recommendations]產品資料庫，而非使用CSV產品摘要或在產品頁面上引發的[!DNL Target]請求，請使用[儲存實體API](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities)。 此請求會新增或更新單一[!DNL Target]環境中的項目。 語法為：

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

例如，「保存實體」(Save Entities)可用於在滿足某些閾值（如庫存閾值或價格閾值）時更新項目，以便標籤這些項目並防止建議它們。

1. 導覽至&#x200B;**[!DNL Target]> [!UICONTROL Setup] > [!UICONTROL Hosts] > [!UICONTROL Environments]** ，以取得您要新增或更新項目的[!DNL Target]環境ID。

   ![SaveEntities1](assets/SaveEntities01.png)

2. 驗證`TENANT_ID`和`API_KEY`參考先前建立的Postman環境變數。 請使用下圖進行比較。 如有需要，請修改API請求中的標題和路徑，以符合下圖中的標題和路徑。

   ![SaveEntities3](assets/SaveEntities03.png)

3. 在&#x200B;**Body**&#x200B;中，將JSON輸入為&#x200B;**raw**&#x200B;程式碼。 別忘了使用`environment`變數指定環境ID。 （在以下範例中，環境ID為6781。）

   ![SaveEntities4.png](assets/SaveEntities04.png)

   >!![NOTE]
   以下示例JSON，它將entity.id kit2001與烤麵包機烤箱產品的相關實體值添加到環境6781中。

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

4. 按一下「**傳送**」。您應會收到下列回應。

   ![SaveEntities5.png](assets/SaveEntities05.png)

JSON物件可縮放以傳送多個產品。 例如，此JSON會指定兩個實體。

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

1. 現在輪到你了！ 使用&#x200B;**儲存實體** API將下列項目新增至目錄。 請從上方的範例JSON開始。 （您需要擴充JSON以包含其他實體。）

   ![SaveEntities6.png](assets/SaveEntities06.png)

哇，看來最後兩件都不屬於。 我們將使用&#x200B;**Get Entity** API來檢查這些實體，並視需要使用&#x200B;**Delete Entities** API刪除這些實體。

## 使用取得實體API取得項目詳細資訊

若要擷取現有項目的詳細資訊，請使用[取得實體API](https://developers.adobetarget.com/api/recommendations/#operation/getEntity)。 語法為：

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

一次只能為單一實體擷取實體詳細資料。 您可以使用「取得實體」來確認目錄中已如預期進行更新，或以其他方式稽核目錄內容。

1. 在API請求中，使用變數`entityId`指定實體ID。 以下示例將返回其entityId=kit2004的實體的詳細資訊。

   ![GetEntity1](assets/GetEntity1.png)

2. 驗證`TENANT_ID`和`API_KEY`參考先前建立的Postman環境變數。 請使用下圖進行比較。 如有需要，請修改API請求中的標題和路徑，以符合下圖中的標題和路徑。

   ![GetEntity2](assets/GetEntity2.png)

3. 傳送要求。

   ![GetEntity3](assets/GetEntity3.png)
如果您收到錯誤訊息，指出找不到實體（如上例所示），請確認您是否將請求提交至正確的 [!DNL Target] 環境。

   >[!NOTE]
   如果未明確指定任何環境，則「獲取實體」將嘗試僅從[預設環境](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=en)獲取實體。 如果您想從預設環境以外的任何環境提取，必須指定環境ID。

4. 如有必要，請新增`environmentId`參數，然後重新傳送要求。

   ![GetEntity4](assets/GetEntity4.png)

5. 發送另一個&#x200B;**Get Entity**&#x200B;請求，這次檢查其entityId=kit2005的實體。

   ![GetEntity5](assets/GetEntity5.png)

假設您決定需要從目錄中移除這些實體。 讓我們使用&#x200B;**Delete Entities** API。

## 使用刪除實體API刪除項目

若要從目錄中移除項目，請使用[刪除實體API](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities)。 語法為：

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
此API會刪除由您指定ID所參考的實體。
如果未提供實體ID，則指定環境中的所有實體都會被刪除。 如果未指定環境ID，則會從所有環境中刪除實體。 小心使用！

1. 導覽至&#x200B;**[!DNL Target]> [!UICONTROL Setup] > [!UICONTROL Hosts] > [!UICONTROL Environments]** ，以取得您要刪除項目的[!DNL Target] Environment ID。

   ![DeleteEntities1](assets/SaveEntities01.png)

2. 在API請求中，使用語法`&ids=[comma-delimited-entity-ids]`（查詢參數），指定您要刪除之實體的實體ID。 刪除多個實體時，請使用逗號分隔ID。

   ![DeleteEntities2](assets/DeleteEntities2.png)

3. 使用`&environment=[environmentId]`語法指定環境ID，否則將刪除所有環境中的實體。

   ![DeleteEntities3](assets/DeleteEntities3.png)

4. 驗證`TENANT_ID`和`API_KEY`參考先前建立的Postman環境變數。 請使用下圖進行比較。 如有需要，請修改API請求中的標題和路徑，以符合下圖中的標題和路徑。

   ![DeleteEntities4](assets/DeleteEntities4.png)

5. 傳送要求。

   ![DeleteEntities5](assets/DeleteEntities5.png)

6. 使用&#x200B;**Get Entity**&#x200B;驗證結果，此時應該表示找不到已刪除的實體。

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

恭喜！ 您現在可以使用[!DNL Recommendations] API來建立、更新、刪除和取得目錄中實體的詳細資訊。 在下一節中，您將學習如何管理自訂條件。

[下堂課「管理自訂條件」>](manage-custom-criteria.md)
