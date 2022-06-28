---
title: 如何使用API管理Recommendations目錄
description: 本教程的這一部分將指導開發人員完成使用Adobe TargetAPI建立、更新、保存、獲取和刪除Recommendations目錄中的實體所需的步驟。
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 8060b69b-e8e5-4fe7-895f-742410d8ed45
source-git-commit: cee2618bb92284da1f82d108a0aff0d39340a15b
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 2%

---

# 管理 [!DNL Recommendations] 使用API的目錄

此時，您已學會了如何使用JWT驗證流生成訪問令牌，以使用帶Adobe I/O的Adobe Target管理API。

您可以使用 [RecommendationsAPI](https://developers.adobetarget.com/api/recommendations/) 添加、更新或刪除建議目錄中的項目。 與其他Adobe Target管理API一樣， [!DNL Recommendations] API需要驗證。

>[!TIP]
>
>發送 **[!UICONTROL IMS:JWT通過用戶令牌生成+驗證]** 在需要刷新訪問令牌以進行身份驗證時請求，因為該令牌在24小時後過期。 請參閱 [配置AdobeAPI身份驗證](https://developer.adobe.com/target/before-administer/configure-authentication/){target=&quot;_blank&quot;}以獲取說明。

![JWT3ff](assets/configure-io-target-jwt3ff.png)

>[!NOTE]
>
>在繼續之前，獲取 [RecommendationsPostman系列](https://developers.adobetarget.com/api/recommendations/#section/Postman)。

## 使用「保存實體API」建立和更新項目

填充 [!DNL Recommendations] 使用API而不是CSV產品源的產品資料庫或 [!DNL Target] 請求在產品頁面上觸發，使用 [保存實體API](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities)。 此請求在單個中添加或更新項目 [!DNL Target] 環境。 語法為：

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

例如，當滿足某些閾值（如庫存或價格的閾值）時，「保存實體」可用於更新物料，以標籤這些物料並防止它們被推薦。

1. 導航到 **[!DNL Target]> [!UICONTROL 設定] > [!UICONTROL 主機] > [!UICONTROL 環境]** 獲取 [!DNL Target] 要添加或更新項目的環境ID。

   ![保存實體1](assets/SaveEntities01.png)

2. 驗證 `TENANT_ID` 和 `API_KEY` 參考先前建立的Postman環境變數。 使用下面的影像進行比較。 如有必要，請修改API請求中的標頭和路徑，以匹配下面映像中的標頭和路徑。

   ![保存實體3](assets/SaveEntities03.png)

3. 將JSON輸入為 **生** 代碼 **身體**。 不要忘記使用 `environment` 變數。 （在下面的示例中，環境ID為6781。）

   ![保存實體4.png](assets/SaveEntities04.png)

   >!![NOTE]
   下面是示例JSON，它將entity.id kit2001與烤麵包機烤箱產品的關聯實體值添加到環境6781中。

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

4. 按一下「**傳送**」。您應收到以下響應。

   ![保存實體5.png](assets/SaveEntities05.png)

JSON對象可縮放以發送多個產品。 例如，此JSON指定兩個實體。

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

1. 現在輪到你了！ 使用 **保存實體** API，將以下項添加到目錄。 使用上面的示例JSON作為起點。 （您需要擴展JSON以包括其他實體。）

   ![保存實體6.png](assets/SaveEntities06.png)

哇，看來最後兩件都不屬於。 讓我們使用 **獲取實體** API，如果需要，使用 **刪除實體** API。

## 使用獲取實體API獲取項詳細資訊

要檢索現有項的詳細資訊，請使用 [獲取實體API](https://developers.adobetarget.com/api/recommendations/#operation/getEntity)。 語法為：

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

一次只能為單個實體檢索實體詳細資訊。 您可以使用「獲取實體」來確認在目錄中按預期進行了更新，或以其他方式審核目錄的內容。

1. 在API請求中，使用變數指定實體ID `entityId`。 以下示例將返回其entityId=kit2004的實體的詳細資訊。

   ![GetEntity1](assets/GetEntity1.png)

2. 驗證 `TENANT_ID` 和 `API_KEY` 參考先前建立的Postman環境變數。 使用下面的影像進行比較。 如有必要，請修改API請求中的標頭和路徑，以匹配下面映像中的標頭和路徑。

   ![GetEntity2](assets/GetEntity2.png)

3. 發送請求。

   ![GetEntity3](assets/GetEntity3.png)
如果您收到錯誤，指出未找到實體，請驗證您是否將請求提交到正確的 [!DNL Target] 環境。

   >[!NOTE]
   如果未明確指定環境，則「獲取實體」會嘗試從 [預設環境](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=en) 只是。 如果要從預設環境以外的任何環境中提取，必須指定環境ID。

4. 如有必要，請添加 `environmentId` 參數，然後重新發送請求。

   ![GetEntity4](assets/GetEntity4.png)

5. 發送其他 **獲取實體** 請求，此時檢查其entityId=kit2005的實體。

   ![獲取實體5](assets/GetEntity5.png)

假設您決定需要從目錄中刪除這些實體。 讓我們使用 **刪除實體** API。

## 使用刪除實體API刪除項

要從目錄中刪除項目，請使用 [刪除實體API](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities)。 語法為：

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
此API刪除由您指定的ID引用的實體。
如果未提供實體ID，則刪除給定環境中的所有實體。 如果未提供環境ID，則將從所有環境中刪除實體。 小心使用！

1. 導航到 **[!DNL Target]> [!UICONTROL 設定] > [!UICONTROL 主機] > [!UICONTROL 環境]** 獲取 [!DNL Target] 要從中刪除項的環境ID。

   ![刪除實體1](assets/SaveEntities01.png)

2. 在API請求中，使用語法指定要刪除的實體的實體ID `&ids=[comma-delimited-entity-ids]` （查詢參數）。 刪除多個實體時，請使用逗號分隔ID。

   ![刪除實體2](assets/DeleteEntities2.png)

3. 使用語法指定環境ID `&environment=[environmentId]`否則，將刪除所有環境中的實體。

   ![刪除實體3](assets/DeleteEntities3.png)

4. 驗證 `TENANT_ID` 和 `API_KEY` 參考先前建立的Postman環境變數。 使用下面的影像進行比較。 如有必要，請修改API請求中的標頭和路徑，以匹配下面映像中的標頭和路徑。

   ![刪除實體4](assets/DeleteEntities4.png)

5. 發送請求。

   ![刪除實體5](assets/DeleteEntities5.png)

6. 使用 **獲取實體**，現在應表示找不到已刪除的實體。

   ![刪除實體6](assets/DeleteEntities6.png)

   ![刪除實體6](assets/DeleteEntities7.png)

恭喜！ 您現在可以使用 [!DNL Recommendations] 建立、更新、刪除和獲取目錄中實體的詳細資訊的API。 在下一節中，您將學習如何管理自定義條件。

[下一個「管理自定義條件」 >](https://developer.adobe.com/target/before-administer/recs-api/manage-custom-criteria/){target=&quot;_blank&quot;
