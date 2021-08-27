---
title: 下載並更新We.Travel範例應用程式
description: 'We.Travel範例應用程式已透過AdobeMobile Services SDK v4預先實作。 您只需要更新它，使其指向您自己的Experience Cloud組織和解決方案帳戶。   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
thumbnail: null
exl-id: 244bcf7a-b59b-4dd1-bd05-0a55ce7a7132
source-git-commit: ee58c7c85708722cf040cd9b039a2855dd390a16
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# 下載並更新We.Travel範例應用程式

We.Travel範例應用程式已透過AdobeMobile Services SDK v4預先實作。 您只需要更新它，就能指向您自己的Experience Cloud組織和解決方案帳戶。

## 學習目標

在本課程結束時，您將能夠：

* 下載並開啟Android Studio中的We.Travel範例應用程式
* 驗證並更新[!DNL Target]的Mobile Services SDK設定

## 下載We.Travel應用程式

* 下載[sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* 解壓縮zip檔案
* 在Android Studio中以現有專案的形式開啟應用程式（忽略「VCS根映射無效」的任何錯誤）
* 在模擬器中執行應用程式，確認應用程式已建置，且您可以看見主畫面
* 瀏覽應用程式，確認您可以完成預訂流程（選取任何付款選項，然後按一下「繼續」，略過計費畫面！）

   ![開啟appConfirmation](assets/wetravel_homeScreen.png)![畫面](assets/wetravel_confirmationScreen.png)

## 驗證並更新[!DNL Target]的Mobile Services SDK設定

AdobeMobile Services SDK已根據檔案](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en)預先安裝在We.Travel應用程式[中。 現在您將更新安裝，以指向您自己的[!DNL Target]帳戶。

首先，在Mobile Services使用者介面中建立新應用程式：

1. 登入[AdobeMobile Services介面](https://mobilemarketing.adobe.com/)。
1. 前往[!UICONTROL 管理應用程式]，然後按一下&#x200B;**[!UICONTROL 新增]**&#x200B;以新增要與本教學課程搭配使用的新應用程式（**[!UICONTROL 管理應用程式]** > **[!UICONTROL 新增]**）。
1. 選擇含有非生產資料的Analytics報表套裝，為應用程式命名，選取&#x200B;**[!UICONTROL Standard]**&#x200B;類型，然後按一下&#x200B;**[!UICONTROL 儲存]**。
1. 新增應用程式後，請在[!UICONTROL SDK目標選項]區段的下一個畫面中新增您的[!DNL Target]用戶端代碼（您可以在&#x200B;**[!UICONTROL Setup]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit Settings]**&#x200B;介面中「下載`at.js`」按鈕旁的[!DNL Target]介面中找到您的用戶端代碼）。
1. [!UICONTROL 請求逾時]設定決定在執行逾時指示前，應用程式等待[!DNL Target]伺服器回應的時間。 只需保留預設設定即可。
1. 啟用[!UICONTROL 訪客ID服務]，並確認下拉式清單中已選取您的[!UICONTROL 組織]。
1. 按一下視窗右上方的&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存您的變更（而非[!UICONTROL 通用連結]、[!UICONTROL 應用程式連結]選項或[!UICONTROL 推送服務]區段中的變更）。
1. 捲動至頁面底部的「應用程式SDK下載」區段，然後下載設定檔案：

   ![下載設定檔案](assets/config_file.jpg)

1. 取代Android Studio專案資產資料夾中的`ADBMobileConfig.json`檔案（應用程式> src >主要>資產）。

1. 現在開啟`ADBMobileConfig.json`檔案，並確認其包含預期的變更，例如您的[!DNL Target]用戶端代碼和您的Analytics詳細資料：
   ![下載設定檔案](assets/client_code.jpg)

如果您沒有看到設定，請確認您已按一下[!UICONTROL Mobile Services]介面中的右&#x200B;**[!UICONTROL Save]**&#x200B;按鈕，並將檔案複製到正確的位置。

恭喜！ 您已使用[!DNL Target]帳戶詳細資訊更新SDK! 在下堂課新增[!DNL Target]請求後，我們將對設定進行額外驗證。

**[下一個：&quot;添加目標請求&quot; >](add-requests.md)**
