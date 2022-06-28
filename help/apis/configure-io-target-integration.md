---
title: 如何配置Adobe TargetAPI的身份驗證
description: 本教程指導開發人員完成生成與Adobe TargetAPI成功交互所需的驗證令牌所需的步驟。 按照以下步驟使用Adobe Developer控制台生成和test使用目標API所需的承載訪問令牌。
role: Developer, Admin, Architect
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Administration & Configuration
doc-type: tutorial
kt: null
author: Judy Kim
exl-id: 8a1e93e4-67b2-4942-a8da-fc0f2cbb2df2
source-git-commit: cee2618bb92284da1f82d108a0aff0d39340a15b
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 3%

---

# 配置Adobe TargetAPI的身份驗證

Adobe Target管理API，包括 [!DNL Recommendations] 管理員API通過身份驗證進行保護，以確保只有授權用戶才使用它們訪問Adobe Target。 使用 [Adobe Developer控制台](https://console.adobe.io/) 為所有Adobe Experience Cloud解決方案管理此身份驗證 [!DNL Target]。

本課將介紹生成與Adobe TargetAPI成功交互所需的驗證令牌所需的初步步驟。 在以下各節中，您將：

1. 在Adobe Developer控制台中建立項目（以前稱為整合）。
2. 將項目詳細資訊導出到Postman。
3. 生成承載訪問令牌。
4. Test承載訪問令牌。

## 先決條件

| 資源 | 詳細資料 |
| --- | --- |
| Postman | 要成功完成這些步驟，請 [Postman應用](https://www.postman.com/downloads/) 作業系統。 Postman基本賬戶是免費的。 雖然一般不需要Adobe TargetAPI，但Postman使API工作流更加容易，而Adobe Target提供了幾個Postman集合，以幫助執行其API並瞭解它們如何操作。 本教程的其餘部分假定您對Postman有工作知識。 有關幫助，請參考 [Postman文檔](https://learning.getpostman.com/)。 |
| 引用 | 在本教程的其餘部分中，假定您熟悉以下資源：<UL><li>[Adobe I/O吉圖布](https://github.com/adobeio)</li><li>[目標Adobe I/O文檔](https://developers.adobetarget.com/api/#introduction)</li><li>[RecommendationsAPI文檔](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

## 建立Adobe I/O項目

在本節中，您將訪問Adobe Developer控制台並為 [!DNL Adobe Target]。 有關詳細資訊，請參考 [項目文檔](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects.md)。

<!--1. Generate your private key and public certificate, per the [documentation on authentication](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). //<!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below. // The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.-->

1. 在 [Adobe Admin Console](https://adminconsole.adobe.com/)，確保已授予您的Adobe用戶帳戶 [產品管理](https://helpx.adobe.com/enterprise/using/admin-roles.html) 和 [開發人員](https://helpx.adobe.com/enterprise/using/manage-developers.html) 級別訪問 [!DNL Target]。

2. 在 [Adobe Developer控制台](https://console.adobe.io/)，選擇要為其建立此整合的Experience Cloud組織。 (請注意，您可能只能訪問單個Experience Cloud組織。)

   ![configure-io-target-createproject2.png](assets/configure-io-target-createproject2.png)

3. 按一下 **[!UICONTROL 建立新項目]**。

   ![configure-io-target-createproject3.png](assets/configure-io-target-createproject3.png)

4. 按一下 **[!UICONTROL 添加API]** 將REST API添加到項目中以訪問Adobe服務和產品。

   ![添加API](assets/configure-io-target-createproject4.png)

5. 選擇 **[!DNL Adobe Target]** 作為要整合的Adobe服務。 按一下 **[!UICONTROL 下一個]** 按鈕。

   ![configure-io-target-createproject5](assets/configure-io-target-createproject5.png)

6. 選擇一個選項，用於將公共密鑰和私鑰與您為目標建立的服務帳戶整合相關聯。 對於本教程，請選擇 **[!UICONTROL 選項1:生成密鑰對]** 按一下 **[!UICONTROL 生成鍵對]**。
   ![configure-io-target-createproject6](assets/configure-io-target-createproject6.png)

7. 注意結果！ 按照說明，記下自動下載的配置檔案(`config`)，其中包含您的私鑰。 按&#x200B;**[!UICONTROL 「下一步」]**。
   ![configure-io-target-createproject7](assets/configure-io-target-createproject7.png)
8. 在檔案系統中，驗證 `config`，是在上一步中建立的壓縮配置檔案。 這個 `config` 檔案包含您以後需要的私鑰。 檔案系統中的確切位置可能與此處所示的位置不同。
   ![configure-io-target-createproject8](assets/configure-io-target-createproject8.png)
9. 返回Adobe Developer控制台，選擇 [產品配置檔案](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html) 與所使用的屬性相對應 [!DNL Recommendations]。 (如果不使用屬性，請選擇「預設工作區」(Default Workspace)選項。) 按一下 **[!UICONTROL 保存已配置的API]**。
   ![configure-io-target-createproject9](assets/configure-io-target-createproject9.png)

10. 按一下 **[!UICONTROL 建立整合]**。 您應收到一條臨時消息，表明您的API已成功配置。

11. 最後，將項目更名為比原始項目更有意義的名稱 `Project 1`。 要執行此操作，請使用如所示的導航路徑導航到項目，按一下 **[!UICONTROL 編輯項目]** 訪問**[!UICONTROL 編輯項目] 模式，並更名項目。

![configure-io-target-createproject11](assets/configure-io-target-createproject11.png)

>[!NOTE]
> 
>在本教程中，我們將項目命名為「目標整合」。 如果您期望將項目用於不僅是Adobe Target，您可能需要相應地命名它。 例如，您可能會選擇將其命名為「AdobeAPI」或「Experience CloudAPI」，因為它可能與Adobe Experience Cloud的其他解決方案一起使用。

## 導出項目詳細資訊

現在，您有了一個Adobe項目，可用於訪問 [!DNL Target]，您需要確保發送該項目的詳細資訊以及AdobeAPI請求。 需要這些詳細資訊才能與多個AdobeAPI進行交互，包括幾個 [!DNL Target] API。 例如，整合詳細資訊包括 [!DNL Target] 管理API 因此，要將API與Postman一起使用，您需要將這些詳細資訊輸入Postman。

有多種方法可以指定您在Postman的項目的詳細資訊，但在本節中，我們將利用一些預構建的功能和集合。 首先（在本節中），您將將整合的詳細資訊導出到Postman環境。 接下來（在下節中），您將生成一個承載訪問令牌，以授予您對必要的Adobe資源的訪問權限。

>[!NOTE]
>
>有關適用於任何Experience Cloud解決方案的視頻說明，包括 [!DNL Target]，請參閱 [將Postman與Experience PlatformAPI一起使用](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=en)。 以下各節與 [!DNL Target] API:
>
> 1. 將Adobe I/O整合詳細資訊導出到Postman
> 2. 使用Postman生成訪問令牌

>
> 下面還提供了這些步驟。

1. 仍在 [Adobe Developer控制台](https://console.adobe.io/)，導航到查看新項目 **[!UICONTROL 服務帳戶(JWT)]** 憑據。 使用左導航或 **[!UICONTROL 憑據]** 的下界。
   ![JWT1](assets/configure-io-target-jwt1.png)
在 **[!UICONTROL 憑據詳細資訊]**，請注意，您可以查看 **公鑰**。 **客戶端ID**以及與服務帳戶相關的其他資訊。
   ![JWT1a](assets/configure-io-target-jwt1a.png)
2. 按一下以導航至有關 **[!UICONTROL Adobe Target]** API。 使用左導航或 **[!UICONTROL 連接的產品和服務]** 的下界。
   ![JWT2](assets/configure-io-target-jwt2.png)
3. 按一下 **[!UICONTROL 下載Postman]** > **[!UICONTROL 服務帳戶(JWT)]** 建立捕獲Postman環境的驗證資訊的JSON檔案。
   ![JWT3](assets/configure-io-target-jwt3.png)
記下檔案系統中的JSON檔案。
   ![JWT3a](assets/configure-io-target-jwt3a.png)
4. 在Postman，按一下「齒輪」表徵圖以管理您的環境，然後按一下 **導入** 導入JSON檔案（環境）。
   ![JWT4](assets/configure-io-target-jwt4.png)
5. 選擇檔案並按一下 **開啟**。
   ![JWT5](assets/configure-io-target-jwt5.png)
6. 在Postman **管理環境** 模式，按一下新導入環境的名稱以對其進行檢查。 (您的環境名稱可能與此處顯示的名稱不同。 根據需要編輯名稱。 它不一定需要與Adobe項目的名稱匹配。)
   ![JWT6](assets/configure-io-target-jwt6.png)
7. 注釋 `CLIENT_SECRET` 和 `API_KEY` （以及其他變數）的值已預填充，取自在Adobe Developer控制台中定義的整合。 (Postman `CLIENT_SECRET` 變數應匹配 `CLIENT SECRET` Adobe開發人員控制台中顯示的憑據， `API_KEY` Postman也應該 `CLIENT ID` )的正文。 相比之下，注意 `PRIVATE_KEY`。 `JWT_TOKEN`, `ACCESS_TOKEN` 為空。 讓我們從提供 `PRIVATE_KEY` 值。
   ![JWT7](assets/configure-io-target-jwt7.png)

   >[!NOTE]
   >
   >**驚喜！**
   >
   >小測驗！ 你記得你的私鑰在哪嗎？
   >沒錯，在 `config` 檔案已從Adobe Developer控制台下載！

8. 從檔案系統開啟 `config` 檔案，然後開啟 `private` 鍵檔案。
   ![JWT8](assets/configure-io-target-jwt8.png)
9. 選擇並複製 `private` 鍵檔案。
   ![JWT9](assets/configure-io-target-jwt9.png)
10. 在Postman，將您的私鑰值貼上到 **初始值** 和 **當前值** 的子菜單。
   ![JWT10](assets/configure-io-target-jwt10.png)
11. 按一下 **[!UICONTROL 更新]**，並關閉「環境」模式。


## 生成承載訪問令牌

在本節中，您將生成持有者訪問令牌，該令牌是驗證您與Adobe TargetAPI的交互所必需的。 要生成持有者訪問令牌，您需要將整合詳細資訊（在前面各節中建立）發送到 [AdobeIdentity Management社](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md)。 有幾種不同的方法可以做到這一點，但在本教程中，我們讓您為IMS API構建一個定製的POST請求。 開玩笑的。 在本教程中，我們利用一個包含預構建的IMS調用的Postman集合，使該過程直接且簡單。 一旦導入集合，您可以在需要時重新使用它，以便不僅為Adobe Target生成新令牌，而且為其他AdobeAPI生成新令牌。

1. 導航到 [AdobeIdentity Management服務API示例調用](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)。
   ![令牌1](assets/configure-io-target-generatetoken1.png)
2. 按一下 **Adobe I/O訪問令牌生成Postman集合**。
   ![令牌2](assets/configure-io-target-generatetoken2.png)
3. 通過按一下獲取此集合的原始JSON **原始**，然後將生成的JSON複製到剪貼簿。 （或者，可以將原始JSON另存為.json檔案。）
   ![令牌3](assets/configure-io-target-generatetoken3.png)
4. 在Postman，通過貼上和從剪貼簿提交原始JSON來導入集合。 （或者，您也可以上載您保存的.json檔案。） 按一下&#x200B;**「繼續」**。
   ![令牌4](assets/configure-io-target-generatetoken4.png)
5. 選擇 **[!UICONTROL IMS:JWT通過用戶令牌生成+驗證]** 在Adobe I/O訪問令牌生成Postman集合中請求，確保已選擇您的環境，然後按一下 **發送** 來生成標籤。

   ![令牌5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >此持有者訪問令牌將有效24小時。 只要需要生成新令牌，請再次發送請求。

6. 再次開啟「管理環境」模式，然後選擇您的環境。
   ![令牌6](assets/configure-io-target-jwt11.png)
7. 注意 `ACCESS_TOKEN` 和 `JWT_TOKEN` 值現在已填充。
   ![令牌7](assets/configure-io-target-generatetoken7.png)

>[!NOTE]
>
>問：我是否必須使用Adobe I/O訪問令牌生成Postman集合來生成JSON Web令牌(JWT)和持牌訪問令牌？
>
>答：不！ Adobe I/O訪問令牌生成Postman集合可方便地在Postman更容易地生成JWT和持有者訪問令牌。 或者，您可以使用Adobe Developer控制台中的功能手動生成承載訪問令牌。

## Test承載訪問令牌

在本練習中，您將通過發送API請求來使用新的持有者訪問令牌，該請求從您的 [!DNL Target] 帳戶。 成功響應表示Adobe項目和身份驗證正按預期運行，以便使用API。

1. 導入 [Adobe Target管理APIPostman集合](https://developers.adobetarget.com/api/#admin-postman-collection)。 按照所有提示操作，直到集合在Postman導入。
   ![測試令牌1](assets/configure-io-target-testtoken0.png)
1. 展開收藏，並注意 **[!UICONTROL 列出活動]** 請求。
   ![測試令牌1](assets/configure-io-target-testtoken1.png)
1. 請注意，變數，如 `{{access_token}}` 未解析。 可以用多種不同的方法解決此問題，例如，可以定義一個名為 `{{access_token}}` — 但在本教程中，您將更改API請求以利用您以前使用的Postman環境。 這將使Adobe能夠繼續作為跨環境API通用的所有變數的單一一致整合。
   ![測試令牌2](assets/configure-io-target-testtoken2.png)
1. 要替換的類型 `{{access_token}}` 與 `{{ACCESS_TOKEN}}`。
   ![測試令牌3](assets/configure-io-target-testtoken3.png)
1. 要替換的類型 `{{api_key}}` 與 `{{API_KEY}}`。
   ![測試令牌4](assets/configure-io-target-testtoken4.png)
1. 要替換的類型 `{{tenant}}` 與 `{{TENANT_ID}}`。 注釋 `{{TENANT_ID}}` 尚未識別。
   ![測試令牌4](assets/configure-io-target-testtoken4a.png)
1. 開啟「管理環境」模式，然後選擇您的環境。
   ![JWT11](assets/configure-io-target-jwt11.png)
1. 鍵入以添加新 `{{TENANT_ID}}` 環境變數。 將租戶ID值複製並貼上到 **初始值** 和 **當前值** 的 `TENANT_ID` 環境變數。

   ![測試令牌5](assets/configure-io-target-testtoken5.png)

   >[!NOTE]
   >
   >租戶ID與您的 [!DNL Target] `clientcode`。 登錄到時，URL中存在租戶ID [!DNL Target]。 要獲取您的租戶ID，請登錄到 [!DNL Adobe Experience Cloud]開啟 [!DNL Target]，然後按一下 [!DNL Target] 卡。 使用URL子域中注明的租戶ID值。
   >
   >例如，如果登錄Adobe Target時的URL是
   >
   >`<https://mycompany.experiencecloud.adobe.com/...>`
   >
   >你的租戶ID是&quot;mycompany&quot;

1. 在確保選擇了正確的環境後，發送您的請求。 您應收到包含活動清單的響應。
   ![測試令牌6](assets/configure-io-target-testtoken6.png)

恭喜！ 現在您已驗證了Adobe驗證，您可以使用它與Adobe TargetAPI(以及其他AdobeAPI)進行交互。 例如， [使用RecommendationsAPI](https://developer.adobe.com/target/before-administer/recs-api/){target=&quot;_blank&quot;}以建立或管理建議。
