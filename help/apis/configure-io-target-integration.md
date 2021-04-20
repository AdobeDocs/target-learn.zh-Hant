---
title: 如何配置Adobe TargetAPI的驗證
description: 本教學課程將引導開發人員完成產生與Adobe TargetAPI成功互動所需驗證Token的必要步驟。 請依照下列步驟，使用Adobe開發人員主控台產生並測試使用Target API所需的承載存取Token。
role: Developer, Administrator, Architect
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Administration & Configuration
doc-type: tutorial
kt: null
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: 2c371ea17ce38928bcf3655a0d604a69e29963a0
workflow-type: tm+mt
source-wordcount: '1896'
ht-degree: 2%

---


# 設定Adobe TargetAPI的驗證

Adobe Target管理API（包括[!DNL Recommendations]管理API）會透過驗證加以保護，以確保只有經過授權的使用者才能使用這些API來存取Adobe Target。 使用[Adobe開發人員控制台](https://console.adobe.io/)管理所有Adobe Experience Cloud解決方案的此驗證，包括[!DNL Target]。

本課將逐步說明產生與Adobe TargetAPI成功互動所需的驗證Token所需的初步步驟。 在下列章節中，您將：

1. 在Adobe開發人員主控台中建立專案（先前稱為整合）。
2. 將專案詳細資訊匯出至Postman。
3. 產生承載存取Token。
4. 測試承載存取Token。

## 先決條件

| 資源 | 詳細資料 |
| --- | --- |
| 郵遞員 | 為了成功完成這些步驟，請為您的作業系統獲取[Postman應用程式](https://www.postman.com/downloads/)。 郵遞員基本功能是免費的，可建立帳戶。 雖然一般而言，Adobe TargetAPI並非必要項目，但Postman讓API工作流程更輕鬆，而Adobe Target則提供數個Postman系列，以協助執行其API並瞭解其運作方式。 本教程的其餘部分假定您對郵遞員有工作知識。 如需協助，請參閱[郵遞員檔案](https://learning.getpostman.com/)。 |
| 參考 | 在本教學課程的其餘部分中，我們假定您熟悉以下資源：<UL><li>[Adobe I/O吉圖布](https://github.com/adobeio)</li><li>[TargetAdobe I/O檔案](https://developers.adobetarget.com/api/#introduction)</li><li>[RecommendationsAPI檔案](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

## 建立Adobe I/O專案

在本節中，您將訪問Adobe開發人員控制台並為[!DNL Adobe Target]建立項目。 有關詳細資訊，請參考有關項目](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects.md)的[文檔。

<!--1. Generate your private key and public certificate, per the [documentation on authentication](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). //<!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below. // The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.-->

1. 在[Adobe Admin Console](https://adminconsole.adobe.com/)中，確保您的Adobe用戶帳戶已獲得[產品管理員](https://helpx.adobe.com/enterprise/using/admin-roles.html)和[開發人員](https://helpx.adobe.com/enterprise/using/manage-developers.html)級別訪問[!DNL Target]的權限。

2. 在[Adobe開發人員控制台](https://console.adobe.io/)中，選擇要為其建立此整合的Experience Cloud組織。 (請注意，您可能只能存取單一Experience Cloud組織。)

   ![configure-io-target-createproject2.png](assets/configure-io-target-createproject2.png)

3. 按一下&#x200B;**[!UICONTROL 建立新項目]**。

   ![configure-io-target-createproject3.png](assets/configure-io-target-createproject3.png)

4. 按一下「新增API ]**」，將REST API新增至您的專案，以存取Adobe服務和產品。**[!UICONTROL 

   ![新增API](assets/configure-io-target-createproject4.png)

5. 選擇&#x200B;**[!DNL Adobe Target]**&#x200B;作為要與整合的Adobe服務。 按一下顯示的&#x200B;**[!UICONTROL Next]**&#x200B;按鈕。

   ![configure-io-target-createproject5](assets/configure-io-target-createproject5.png)

6. 選擇一個選項，可將公用和私密金鑰與您為Target建立的服務帳戶整合建立關聯。 在本教程中，選擇&#x200B;**[!UICONTROL 選項1:生成密鑰對]**&#x200B;並按一下「生成密鑰對&#x200B;**[!UICONTROL 」。]**
   ![configure-io-target-createproject6](assets/configure-io-target-createproject6.png)

7. 注意結果！ 請依照指示記下包含您的私密金鑰的自動下載組態檔(`config`)。 按&#x200B;**[!UICONTROL 「下一步」]**。
   ![configure-io-target-createproject7](assets/configure-io-target-createproject7.png)
8. 在檔案系統中，驗證`config`的位置，該位置是在上一步中建立的壓縮配置檔案。 同樣地，此`config`檔案包含您的私密金鑰，您稍後將需要該私密金鑰。 您檔案系統內的確切位置可能與此處顯示的位置不同。
   ![configure-io-target-createproject8](assets/configure-io-target-createproject8.png)
9. 回到Adobe開發人員主控台中，選取與您使用[!DNL Recommendations]的屬性對應的[產品設定檔](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html)。 （如果您不使用屬性，請選取「預設工作區」選項。） 按一下「保存配置的API ]**」。**[!UICONTROL 
   ![configure-io-target-createproject9](assets/configure-io-target-createproject9.png)

10. 按一下「建立整合」。 ****&#x200B;您應該會收到一則暫時訊息，指出您的API已成功設定。

11. 最後，將專案重新命名為比原始`Project 1`更有意義的名稱。 若要這麼做，請使用如上所示的導覽路徑導覽至專案，按一下「編輯專案&#x200B;]**」以存取**[!UICONTROL 「編輯專案]」模式，並重新命名專案。**[!UICONTROL 

![configure-io-target-createproject11](assets/configure-io-target-createproject11.png)

>[!NOTE]
> 
>在本教學課程中，我們將專案命名為「Target整合」。 如果您預計不只針對Adobe Target使用專案，您可能會想據此命名專案。 例如，您可以選擇將其命名為&quot;AdobeAPI&quot;或&quot;Experience CloudAPI&quot;，因為它可能與Adobe Experience Cloud的其他解決方案搭配使用。

## 匯出專案詳細資訊

既然您有Adobe專案可用來存取[!DNL Target]，您必須確定傳送該專案的詳細資料以及您的AdobeAPI要求。 若要與數個AdobeAPI互動，包括數個[!DNL Target] API，需要這些詳細資訊。 例如，整合詳細資訊包括[!DNL Target]管理API所需的授權和驗證資訊。 因此，要將API與Postman一起使用，您需要將這些詳細資訊導入Postman。

在Postman中指定專案詳細資訊有許多方法，但在本節中，我們運用一些預先建立的功能和系列。 首先（在本節中），您會將整合的詳細資訊匯出至郵遞員環境。 接下來（在下節），您將產生一個承載存取Token，以授與您對必要Adobe資源的存取權。

>[!NOTE]
>
>如需適用於任何Experience Cloud解決方案（包括[!DNL Target]）的視訊指示，請參閱[搭配Experience PlatformAPI使用郵遞員](https://docs.adobe.com/content/help/en/platform-learn/tutorials/apis/postman.html)。 以下章節與[!DNL Target] API相關：
>
> 1. 將Adobe I/O整合詳細資訊導出到郵遞員
> 2. 使用郵遞員產生存取Token

>
> 
這些步驟也提供如下。

1. 在[Adobe開發人員控制台](https://console.adobe.io/)中，導航以查看新項目的&#x200B;**[!UICONTROL 服務帳戶(JWT)]**&#x200B;憑據。 使用左側導覽或&#x200B;**[!UICONTROL 憑證]**區段，如所示。
   ![JWT1在](assets/configure-io-target-jwt1.png)
 **[!UICONTROL Credential詳細資訊中]**，請注意，您可以檢視您的 **Public key(s)**、 **Client ID**，以及與您的服務帳戶相關的其他資訊。
   ![JWT1a](assets/configure-io-target-jwt1a.png)
2. 按一下以導航至&#x200B;**[!UICONTROL Adobe Target]** API的相關資訊。 使用左側導覽或&#x200B;**[!UICONTROL Connected products and services]**區段，如所示。
   ![JWT2](assets/configure-io-target-jwt2.png)
3. 按一下「下載郵遞員&#x200B;]**>**[!UICONTROL &#x200B;服務帳戶(JWT)]**」以建立JSON檔案，擷取您對郵遞員環境的驗證資訊。**[!UICONTROL 
   ![JWT3請](assets/configure-io-target-jwt3.png)
注意您檔案系統中的JSON檔案。
   ![JWT3a](assets/configure-io-target-jwt3a.png)
4. 在Postman中，按一下齒輪圖示來管理您的環境，然後按一下&#x200B;**匯入**以匯入JSON檔案（環境）。
   ![JWT4](assets/configure-io-target-jwt4.png)
5. 選擇您的檔案，然後按一下&#x200B;**開啟**。
   ![JWT5](assets/configure-io-target-jwt5.png)
6. 在郵遞員&#x200B;**管理環境**模式中，按一下新導入環境的名稱以檢查它。 (您的環境名稱可能與此處顯示的名稱不同。 視需要編輯名稱。 它不一定需要與Adobe專案的名稱相符。)
   ![JWT6](assets/configure-io-target-jwt6.png)
7. 附註`CLIENT_SECRET`和`API_KEY`（連同其他變數）的值已預先填入，取自您的整合，如Adobe開發人員主控台所定義。 (Postman `CLIENT_SECRET`變數應符合「開發人員主控台」中顯示的`CLIENT SECRET`Adobe憑證，而Postman中的`API_KEY`也應符合「開發人員主控台」中的`CLIENT ID`。) 相反，附註`PRIVATE_KEY`、`JWT_TOKEN`和`ACCESS_TOKEN`為空白。 讓我們從提供`PRIVATE_KEY`值開始。
   ![JWT7](assets/configure-io-target-jwt7.png)

   >[!NOTE]
   >
   >**驚喜！**
   >
   >快來測驗！ 你記得你的私鑰在哪嗎？
   >沒錯，它位於之前從Adobe開發人員主控台下載的`config`檔案中！

8. 從檔案系統中開啟`config`檔案，然後開啟`private`密鑰檔案。
   ![JWT8](assets/configure-io-target-jwt8.png)
9. 選擇並複製`private`密鑰檔案的整個內容。
   ![JWT9](assets/configure-io-target-jwt9.png)
10. 在Postman中，將私密金鑰值貼入&#x200B;**INITIAL VALUE**&#x200B;和&#x200B;**CURRENT VALUE**欄位。
   ![JWT10](assets/configure-io-target-jwt10.png)
11. 按一下&#x200B;**[!UICONTROL 更新]** ，然後關閉「環境」模式。


## 產生承載存取Token

在本節中，您會產生您的無記名存取Token，這是驗證您與Adobe TargetAPI的互動所需的。 若要產生您的無記名存取Token，您必須將您的整合詳細資訊（在前述章節中建立）傳送至[AdobeIdentity Management服務(IMS)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md)。 有幾種不同的方式可做到，但在本教學課程中，我們讓您針對IMS API建立定制POST要求。 開玩笑的。 在本教學課程中，我們運用包含預先建立之IMS呼叫的Postman系列，讓程式變得直接而簡單。 匯入系列後，您可視需要重新使用，以產生新的Token，不僅適用於Adobe Target，也適用於其他AdobeAPI。

1. 導覽至[AdobeIdentity Management服務API範例呼叫](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)。
   ![token1](assets/configure-io-target-generatetoken1.png)
2. 按一下&#x200B;**Adobe I/O存取Token產生Postman系列**。
   ![token2](assets/configure-io-target-generatetoken2.png)
3. 按一下&#x200B;**Raw**，然後將產生的JSON複製至剪貼簿，即可取得此系列的原始JSON。 （或者，您也可以將原始JSON儲存為。json檔案。）
   ![token3](assets/configure-io-target-generatetoken3.png)
4. 在Postman中，從剪貼簿貼上並送出原始JSON，以匯入系列。 （或者，您也可以上傳您儲存的。json檔案。） 按一下&#x200B;**「繼續」**。
   ![token4](assets/configure-io-target-generatetoken4.png)
5. 選擇&#x200B;**[!UICONTROL IMS:JWT在Adobe I/O存取Token產生Postman系列中透過使用者Token]**&#x200B;請求產生+驗證，請確定您的環境已選取，然後按一下&#x200B;**Send**&#x200B;以產生Token。

   ![token5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >此無記名存取Token的有效期為24小時。 當您需要產生新Token時，請再次傳送請求。

6. 再次開啟「管理環境」模型，並選擇您的環境。
   ![token6](assets/configure-io-target-jwt11.png)
7. 請注意，`ACCESS_TOKEN`和`JWT_TOKEN`值現在已填入。
   ![token7](assets/configure-io-target-generatetoken7.png)

>[!NOTE]
>
>問：我是否必須使用Adobe I/O存取Token產生Postman系列來產生JSON網頁Token(JWT)和不記名存取Token?
>
>答：不！ Adobe I/O存取Token產生Postman集合是為了方便在Postman中更輕鬆地產生JWT和承載存取Token。 或者，您也可以使用Adobe開發人員主控台中的功能，手動產生承載存取Token。

## 測試承載存取Token

在本練習中，您會傳送從[!DNL Target]帳戶擷取活動清單的API要求，以使用新的持牌者存取Token。 成功的回應表示您的Adobe專案和驗證正如預期般運作，以便使用API。

1. 匯入[Adobe Target管理API郵遞員集合](https://developers.adobetarget.com/api/#admin-postman-collection)。 依照所有提示進行，直到系列匯入Postman。
   ![testtoken1](assets/configure-io-target-testtoken0.png)
1. 展開系列，並記下&#x200B;**[!UICONTROL 清單活動]**請求。
   ![testtoken1](assets/configure-io-target-testtoken1.png)
1. 請注意，`{{access_token}}`等變數最初未解析。 您可以以幾種不同的方式解決此問題——例如，您可以定義名為`{{access_token}}`的新系列變數——但在本教學課程中，您會改變API要求，以運用您先前使用的Postman環境。 這可讓環境繼續以單一、一致的方式整合所有AdobeAPI中常用的變數。
   ![testtoken2](assets/configure-io-target-testtoken2.png)
1. 鍵入以`{{ACCESS_TOKEN}}`替換`{{access_token}}`。
   ![testtoken3](assets/configure-io-target-testtoken3.png)
1. 鍵入以`{{API_KEY}}`替換`{{api_key}}`。
   ![testtoken4](assets/configure-io-target-testtoken4.png)
1. 鍵入以`{{TENANT_ID}}`替換`{{tenant}}`。 注意`{{TENANT_ID}}`尚未識別。
   ![testtoken4](assets/configure-io-target-testtoken4a.png)
1. 開啟「管理環境」模組，並選取您的環境。
   ![JWT11](assets/configure-io-target-jwt11.png)
1. 鍵入以添加新的`{{TENANT_ID}}`環境變數。 將您的租用戶ID值複製並貼至新`TENANT_ID`環境變數的&#x200B;**INITIAL VALUE**&#x200B;和&#x200B;**CURRENT VALUE**&#x200B;欄位。

   ![testtoken5](assets/configure-io-target-testtoken5.png)

   >[!NOTE]
   >
   >租用戶ID與您的[!DNL Target] `clientcode`不同。 當您登入[!DNL Target]時，URL中會存在租用戶ID。 若要取得您的租用戶ID，請登入[!DNL Adobe Experience Cloud]，開啟[!DNL Target]，然後按一下[!DNL Target]卡。 使用URL子網域中注明的租用戶ID值。
   >
   >例如，若您登入Adobe Target時的URL是
   >
   >`<https://mycompany.experiencecloud.adobe.com/...>`
   >
   >您的租用戶ID為「mycompany」。

1. 在確定您已選擇正確的環境後，傳送您的請求。 您應該會收到包含活動清單的回應。
   ![testtoken6](assets/configure-io-target-testtoken6.png)

恭喜！ 現在您已驗證Adobe驗證，您可以用它來與Adobe TargetAPI(以及其他AdobeAPI)互動。 例如，您可以[使用RecommendationsAPI](https://docs.adobe.com/content/help/en/target-learn/recommendations-api-tutorial/recs-api-overview.html)來建立或管理建議。
