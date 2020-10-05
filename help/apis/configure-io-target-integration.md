---
title: 設定Adobe Target API的驗證
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations包含一組專屬的API，可讓您管理建議產品和／或內容的目錄；管理您的建議演算法和宣傳活動；並以JSON、HTML或XML物件提供建議，以便顯示在網頁、行動裝置、電子郵件、IOT和其他通道中。
kt: null
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 7e57febf5f552d697260283a3f98f9b403663f28
workflow-type: tm+mt
source-wordcount: '1885'
ht-degree: 2%

---


# 設定Adobe Target API的驗證

Adobe Target管理API(包括管 [!DNL Recommendations] 理API)會透過驗證加以保護，以確保只有授權使用者才能使用這些API來存取Adobe Target。 使用 [Adobe Developer Console](https://console.adobe.io/) ，管理所有Adobe Experience Cloud解決方案的此驗證，包括 [!DNL Target]。

本課將逐步說明產生與Adobe Target API成功互動所需的驗證Token所需的初步步驟。 在下列章節中，您將：

1. 在Adobe Developer Console中建立專案（先前稱為整合）。
2. 將專案詳細資訊匯出至Postman。
3. 產生承載存取Token。
4. 測試承載存取Token。

## 先決條件

| 資源 | 詳細資料 |
| --- | --- |
| 郵遞員 | 為了順利完成這些步驟，請取得您作 [業系統的Postman應用程式](https://www.postman.com/downloads/) 。 郵遞員基本功能是免費的，可建立帳戶。 Postman可讓API工作流程更輕鬆，而Adobe Target則提供數個Postman系列，以協助執行其API並瞭解其運作方式。 本教程的其餘部分假定您對郵遞員有工作知識。 如需協助，請參閱郵 [遞員檔案](https://learning.getpostman.com/)。 |
| 參考 | 在本教學課程的其餘部分中，我們假定您熟悉以下資源：<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[鎖定Adobe I/O檔案](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API檔案](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

## 建立Adobe I/O專案

在本節中，您將存取Adobe Developer Console並建立專案 [!DNL Adobe Target]。 如需詳細資訊，請參閱專 [案的相關檔案](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects.md)。

<!--1. Generate your private key and public certificate, per the [documentation on authentication](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). //<!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below. // The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.-->

1. 在 [Adobe Admin Console](https://adminconsole.adobe.com/)，請確定您的Adobe使用者帳戶已獲得產品管理員和開發人員級 [別的存](https://helpx.adobe.com/enterprise/using/admin-roles.html) 取權 [](https://helpx.adobe.com/enterprise/using/manage-developers.html)[!DNL Target]。

2. 在 [Adobe Developer Console中](https://console.adobe.io/)，選取您要為其建立此整合的Experience Cloud組織。 （請注意，您可能只能存取單一Experience Cloud組織。）

   ![configure-io-target-createproject2.png](assets/configure-io-target-createproject2.png)

3. Click **[!UICONTROL Create new project]**.

   ![configure-io-target-createproject3.png](assets/configure-io-target-createproject3.png)

4. 按一 **[!UICONTROL 下「新增API]** 」，將REST API新增至您的專案，以存取Adobe服務和產品。

   ![新增API](assets/configure-io-target-createproject4.png)

5. 選 **[!DNL Adobe Target]** 擇您要整合的Adobe服務。 按一下顯 **[!UICONTROL 示的]** 「下一步」按鈕。

   ![configure-io-target-createproject5](assets/configure-io-target-createproject5.png)

6. 選擇一個選項，可將公用和私密金鑰與您為Target建立的服務帳戶整合建立關聯。 在本教學課程中，請選 **[!UICONTROL 擇選項1:生成密鑰對]** ，然後按一下 **[!UICONTROL 生成密鑰對]**。
   ![configure-io-target-createproject6](assets/configure-io-target-createproject6.png)

7. 注意結果！ 請依照指示記下自動下載的設定檔(`config`)，其中包含您的私密金鑰。 按&#x200B;**[!UICONTROL 「下一步」]**。
   ![configure-io-target-createproject7](assets/configure-io-target-createproject7.png)
8. 在檔案系統中，驗證的位 `config`置，該位置是在上一步中建立的壓縮配置檔案。 同樣地，此檔 `config` 案包含您的私密金鑰，您稍後將需要使用。 您檔案系統內的確切位置可能與此處顯示的位置不同。
   ![configure-io-target-createproject8](assets/configure-io-target-createproject8.png)
9. 回到Adobe Developer Console中，選取與 [您所使用之屬性對應的產品設定檔](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html)[!DNL Recommendations]。 （如果您不使用屬性，請選取「預設工作區」選項。） 按一 **[!UICONTROL 下「儲存已設定的API]**」。
   ![configure-io-target-createproject9](assets/configure-io-target-createproject9.png)

10. 按一 **[!UICONTROL 下建立整合]**。 您應該會收到一則暫時訊息，指出您的API已成功設定。

11. 最後，將專案重新命名為比原始檔案更有意義的名稱 `Project 1`。 若要這麼做，請使用如上所示的導覽路徑導覽至專案，按一下「 **[!UICONTROL Edit project]** 」（編輯專案）以存取**[!UICONTROL Edit Project] （編輯專案）模式，然後重新命名專案。

![configure-io-target-createproject11](assets/configure-io-target-createproject11.png)

>[!NOTE]
> 
>在本教學課程中，我們將專案命名為「Target整合」。 如果您預計不只針對Adobe Target使用專案，您可能會想據此命名專案。 例如，您可以選擇將其命名為「Adobe API」或「Experience Cloud API」，因為它可能與Adobe Experience Cloud中的其他解決方案搭配使用。

## 匯出專案詳細資訊

既然您有可用來存取的Adobe專案 [!DNL Target]，您必須確定傳送該專案的詳細資訊以及您的Adobe API要求。 若要與數個Adobe API互動，包括數個API，需要這些詳 [!DNL Target] 細資訊。 例如，整合詳細資訊包括管理API所需的授權和驗 [!DNL Target] 證資訊。 因此，要將API與Postman一起使用，您需要將這些詳細資訊導入Postman。

在Postman中指定專案詳細資訊有許多方法，但在本節中，我們運用一些預先建立的功能和系列。 首先（在本節中），您會將整合的詳細資訊匯出至郵遞員環境。 接下來（在下節），您將產生一個不記名存取Token，以授與您存取必要的Adobe資源。

>[!NOTE]
>
>如需適用於任何Experience Cloud解決方案的視訊指示，包括 [!DNL Target]，請參 [閱「搭配Experience Platform API使用郵遞員](https://docs.adobe.com/content/help/en/platform-learn/tutorials/apis/postman.html)」。 下列章節與API相 [!DNL Target] 關：
>
> 1. 將Adobe I/O整合詳細資訊匯出至郵遞員
> 2. 使用郵遞員產生存取Token

>
> 
這些步驟也提供如下。

1. 仍然在 [Adobe Developer Console中](https://console.adobe.io/)，導覽以檢視您新專案的 **[!UICONTROL 服務帳戶(JWT)憑證]** 。 使用左側導覽或「認證 **[!UICONTROL 」區段]** ，如所示。
   ![JWT1在](assets/configure-io-target-jwt1.png)**[!UICONTROL Credential詳細資訊中]**，請注意，您可以檢視您的 **Public key(s)**、 **Client ID**，以及與您的服務帳戶相關的其他資訊。
   ![JWT1a](assets/configure-io-target-jwt1a.png)
2. 按一下以導覽至 **[!UICONTROL Adobe Target]** API的相關資訊。 請使用左側導覽或「已連 **[!UICONTROL 線的產品與服務]** 」區段，如所示。
   ![JWT2](assets/configure-io-target-jwt2.png)
3. 按一 **[!UICONTROL 下「Download for Postman]** > **[!UICONTROL Service Account(JWT)]** 」，建立JSON檔案，以擷取Postman環境的驗證資訊。
   ![JWT3請](assets/configure-io-target-jwt3.png)注意您檔案系統中的JSON檔案。
   ![JWT3a](assets/configure-io-target-jwt3a.png)
4. 在Postman中，按一下齒輪圖示以管理您的環境，然後按一下「匯 **入** 」以匯入JSON檔案（環境）。
   ![JWT4](assets/configure-io-target-jwt4.png)
5. 選擇您的檔案，然後按一下「 **開啟**」。
   ![JWT5](assets/configure-io-target-jwt5.png)
6. 在「郵遞員 **管理環境** 」模式中，按一下新匯入環境的名稱以進行檢查。 (您的環境名稱可能與此處顯示的名稱不同。 視需要編輯名稱。 它不一定需要符合Adobe專案的名稱。)
   ![JWT6](assets/configure-io-target-jwt6.png)
7. 注意 `CLIENT_SECRET` 事項 `API_KEY` 和（以及其他變數）的值已預先填入，取自您在Adobe Developer Console中定義的整合。 (Postman變 `CLIENT_SECRET` 數應符合Developer Console中顯示的 `CLIENT SECRET` Adobe憑證，而 `API_KEY` Postman中也應符合Developer Console中 `CLIENT ID` 的憑證)。 相反，附註 `PRIVATE_KEY`、 `JWT_TOKEN`和 `ACCESS_TOKEN` 空白。 首先，我們提供值 `PRIVATE_KEY` 吧。
   ![JWT7](assets/configure-io-target-jwt7.png)

   >[!NOTE]
   >
   >**驚喜！**
   >
   >快來測驗！ 你記得你的私鑰在哪嗎？
   >沒錯，它就在之前從Adobe Developer Console `config` 下載的檔案中！

8. 從您的檔案系統開啟您 `config` 的檔案，然後開啟 `private` 金鑰檔案。
   ![JWT8](assets/configure-io-target-jwt8.png)
9. 選擇並複製密鑰檔案的整 `private` 個內容。
   ![JWT9](assets/configure-io-target-jwt9.png)
10. 在Postman中，將私密金鑰值貼入 **INITIAL VALUE****和CURRENT VALUE** 欄位。
   ![JWT10](assets/configure-io-target-jwt10.png)
11. 按一 **[!UICONTROL 下「更新]**」，然後關閉「環境」模式。


## 產生承載存取Token

在本節中，您會產生您的無記名存取Token，這是驗證您與Adobe Target API的互動時所需的。 若要產生您的無記名存取Token，您必須將您的整合詳細資訊（在前述章節中建立）傳送至 [Adobe Identity Management Service(IMS)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md)。 有幾種不同的方式可做到，但在本教學課程中，我們讓您針對IMS API建立定製的POST要求。 開玩笑的。 在本教學課程中，我們運用包含預先建立之IMS呼叫的Postman系列，讓程式變得直接而簡單。 匯入系列後，您可視需要重新使用，以產生新的Token，不僅適用於Adobe Target，也適用於其他Adobe API。

1. 導覽至 [Adobe Identity Management Service API範例呼叫](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)。
   ![token1](assets/configure-io-target-generatetoken1.png)
2. 按一下 **Adobe I/O存取Token產生Postman集合**。
   ![token2](assets/configure-io-target-generatetoken2.png)
3. 按一下「原始」 ****，然後將產生的JSON複製至剪貼簿，即可取得此系列的原始JSON。 （或者，您也可以將原始JSON儲存為。json檔案。）
   ![token3](assets/configure-io-target-generatetoken3.png)
4. 在Postman中，從剪貼簿貼上並送出原始JSON，以匯入系列。 （或者，您也可以上傳您儲存的。json檔案。） 按一下&#x200B;**「繼續」**。
   ![token4](assets/configure-io-target-generatetoken4.png)
5. 選取 **[!UICONTROL IMS:JWT在Adobe I/O存取Token Generation Postman集合中透過使用者Token]** 請求產生+驗證，請確定您的環境已選取，然後按一下 **Send** 以產生Token。

   ![token5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >此無記名存取Token的有效期為24小時。 當您需要產生新Token時，請再次傳送請求。

6. 再次開啟「管理環境」模型，並選擇您的環境。
   ![token6](assets/configure-io-target-jwt11.png)
7. 請注意， `ACCESS_TOKEN` 和 `JWT_TOKEN` 值現在已填入。
   ![token7](assets/configure-io-target-generatetoken7.png)

>[!NOTE]
>
>問：我是否必須使用Adobe I/O存取Token產生Postman集合來產生JSON網頁Token(JWT)和不記名存取Token?
>
>答：不！ Adobe I/O存取Token產生Postman收集是為了方便您在Postman中更輕鬆地產生JWT和不記名存取Token。 或者，您也可以使用Adobe Developer Console中的功能來手動產生不記名存取Token。

## 測試承載存取Token

在本練習中，您會傳送API要求，從您的帳戶擷取活動清單，以使用新的不記名存取Token [!DNL Target] 。 成功的回應表示您的Adobe專案和驗證如預期般運作，以便使用API。

1. 匯入 [Adobe Target管理API郵遞員集合](https://developers.adobetarget.com/api/#admin-postman-collection)。 依照所有提示進行，直到系列匯入Postman。
   ![testtoken1](assets/configure-io-target-testtoken0.png)
1. 展開系列，並記下「清 **[!UICONTROL 單」活動]** 。
   ![testtoken1](assets/configure-io-target-testtoken1.png)
1. 請注意，變數（例如） `{{access_token}}` 最初未解析。 您可以以幾種不同的方式來解決這個問題——例如，您可以定義名為新的系列變數 `{{access_token}}`—但在本教學課程中，您會改變API要求，以運用您先前使用的Postman環境。 這可讓環境繼續以單一、一致的方式整合所有Adobe API中常用的變數。
   ![testtoken2](assets/configure-io-target-testtoken2.png)
1. 鍵入以 `{{access_token}}` 取代 `{{ACCESS_TOKEN}}`。
   ![testtoken3](assets/configure-io-target-testtoken3.png)
1. 鍵入以 `{{api_key}}` 取代 `{{API_KEY}}`。
   ![testtoken4](assets/configure-io-target-testtoken4.png)
1. 鍵入以 `{{tenant}}` 取代 `{{TENANT_ID}}`。 尚未 `{{TENANT_ID}}` 確認附註。
   ![testtoken4](assets/configure-io-target-testtoken4a.png)
1. 開啟「管理環境」模組，並選取您的環境。
   ![JWT11](assets/configure-io-target-jwt11.png)
1. 鍵入以添加新環 `{{TENANT_ID}}` 境變數。 將您的租用戶ID值複製並貼至新 **環境變數的「初始值** 」和「目前值 **」欄**`TENANT_ID` 位中。
   ![testtoken5](assets/configure-io-target-testtoken5.png)
   >[!NOTE]
   >
   >租用戶ID與您的不同 [!DNL Target]`clientcode`。 當您登入時，URL中存在租用戶ID [!DNL Target]。 若要取得您的租用戶ID，請登入、 [!DNL Adobe Experience Cloud]開啟 [!DNL Target]並按一下 [!DNL Target] 資訊卡。 使用URL子網域中注明的租用戶ID值。
   >
   >例如，若您登入Adobe Target時的URL是
   ><https://mycompany.experiencecloud.adobe.com/...>
   >您的租用戶ID為「mycompany」。

1. 在確定您已選擇正確的環境後，傳送您的請求。 您應該會收到包含活動清單的回應。
   ![testtoken6](assets/configure-io-target-testtoken6.png)

恭喜！ 現在您已經驗證Adobe驗證，您可以用它來與Adobe Target API（以及其他Adobe API）互動。 例如，您可以使 [用Recommendations API](https://docs.adobe.com/content/help/en/target-learn/recommendations-api-tutorial/recs-api-overview.html) 來建立或管理建議。
