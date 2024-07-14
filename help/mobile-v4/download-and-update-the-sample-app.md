---
title: 下載並更新We.Travel範例應用程式
description: We.Travel範例應用程式已預先實作Adobe Mobile Services SDK v4。 您只需要更新該檔案，使其指向您自己的Experience Cloud組織和解決方案帳戶。
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 244bcf7a-b59b-4dd1-bd05-0a55ce7a7132
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# 下載並更新We.Travel範例應用程式

We.Travel範例應用程式已預先實作Adobe Mobile Services SDK v4。 您只需要更新它，讓它指向您自己的Experience Cloud組織和解決方案帳戶。

## 學習目標

在本課程結束時，您將能夠：

* 在Android Studio中下載並開啟We.Travel範例應用程式
* 驗證並更新[!DNL Target]的Mobile Services SDK設定

## 下載We.Travel應用程式

* 下載[sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* 解壓縮zip檔案
* 在Android Studio中開啟應用程式作為現有專案（忽略任何有關「無效的VCS根對應」的錯誤）
* 在模擬器中執行應用程式，以確認應用程式會建置，而且您可以看到主畫面
* 瀏覽應用程式，並確認您可以完成預訂程式（選取任何付款選項，然後按一下「繼續」以略過帳單畫面！）

  ![開啟應用程式](assets/wetravel_homeScreen.png)![確認畫面](assets/wetravel_confirmationScreen.png)

## 驗證並更新[!DNL Target]的Mobile Services SDK設定

根據檔案](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en)，已在We.Travel應用程式[中預先安裝Adobe Mobile Services SDK。 現在將更新安裝，以指向您自己的[!DNL Target]帳戶。

首先，在Mobile Services使用者介面中建立新的應用程式：

1. 登入[Adobe行動服務介面](https://mobilemarketing.adobe.com/)。
1. 移至[!UICONTROL Manage Apps]，然後按一下&#x200B;**[!UICONTROL Add]**&#x200B;以新增應用程式以用於此教學課程(**[!UICONTROL Manage Apps]** > **[!UICONTROL Add]**)。
1. 選擇包含非生產資料的Analytics報表套裝、為應用程式命名、選取&#x200B;**[!UICONTROL Standard]**&#x200B;型別並按一下&#x200B;**[!UICONTROL Save]**。
1. 新增應用程式後，請在[!UICONTROL SDK Target Options]區段的下一個畫面中新增您的[!DNL Target]使用者端代碼(您可以在[!DNL Target]介面的&#x200B;**[!UICONTROL Setup]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit Settings]** （在「下載`at.js`」按鈕旁）下找到您的使用者端代碼)。
1. [!UICONTROL Request Timeout]設定會決定應用程式在執行逾時指示前，等待[!DNL Target]伺服器回應的時間。 只要保留預設設定即可。
1. 啟用[!UICONTROL Visitor ID Service]並確定在下拉式清單中選取您的[!UICONTROL Organization]。
1. 按一下視窗右上方的&#x200B;**[!UICONTROL Save]** （不是[!UICONTROL Universal Links]、[!UICONTROL App Links]選項或[!UICONTROL Push Services]區段中的專案）以儲存變更。
1. 向下捲動至頁面底部的「應用程式SDK下載」區段，然後下載設定檔案：

   ![下載設定檔](assets/config_file.jpg)

1. 取代Android Studio專案資產資料夾中的`ADBMobileConfig.json`檔案（應用程式> src >主要>資產）。

1. 現在開啟`ADBMobileConfig.json`檔案，並確定它包含預期的變更，例如[!DNL Target]使用者端代碼和Analytics詳細資料：
   ![下載設定檔](assets/client_code.jpg)

如果您沒有看到您的設定，請確認您已按一下[!UICONTROL Mobile Services]介面中的正確&#x200B;**[!UICONTROL Save]**&#x200B;按鈕，並將檔案複製到正確的位置。

恭喜！您已使用[!DNL Target]帳戶詳細資料更新SDK！ 在下個課程中新增[!DNL Target]個請求後，我們會進一步驗證設定。

**[下一步：「新增Target請求」>](add-requests.md)**
