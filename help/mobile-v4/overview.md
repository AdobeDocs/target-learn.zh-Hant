---
title: Adobe Target與Android專用AdobeMobile Services SDK v4
description: Adobe TargetAdobeMobile Services SDK v4 for Android是已使用AdobeMobile Services SDK v4且想要開始與Adobe Target合作個人化應用程式體驗的Android開發人員的最佳起點。
role: 開發人員
level: 中級
topic: 行動、個人化
feature: 實作行動，概觀
doc-type: tutorial
kt: 3040
thumbnail: null
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---


# Adobe Target與AdobeMobile Services SDK v4 for Android —— 概觀

_Adobe Target與_ Android適用的AdobeMobile Services SDK v4是已使用AdobeMobile Services SDK v4且想要開始與Adobe Target個人化應用程式體驗的Android開發人員的最佳起點。

我們提供示範Android應用程式，讓您完成課程。 完成本教學課程後，您應準備好開始在您自己的Android應用程式中實作[!DNL Target]!

完成此教學課程之後，您將能:

* 驗證[AdobeMobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html)設定
* 實作下列類型的[!DNL Target]請求：
   * 預回遷[!DNL Target]內容
   * 在單一請求中批次多個[!DNL Target]位置(mbox)
   * 封鎖請求（在應用程式顯示前執行）
   * 非封鎖請求（在背景執行）
   * 即時（非快取）
   * 快取破壞重新擷取
* 將參數新增至要求以增強個人化
* 建立受眾和選件
* 個人化版面
* 推出具功能標幟的新功能

## 必要條件

在這些教訓中，我們假定您：

* 具有AdobeID和批准者級別的Adobe Target介面訪問權（請參見以下驗證步驟）
* 瞭解您的Adobe Target客戶代碼，以便向您自己的帳戶提出請求。 用戶端程式碼會顯示在Adobe Target介面的   「設定>實作>編輯at.js設定畫面」
* 存取並熟悉[Mobile Services使用者介面](https://mobilemarketing.adobe.com)
* 針對Android行動應用程式開發使用IDE。 本教學課程將[Android Studio](https://developer.android.com/studio/install)功能整合在各種步驟和螢幕擷取畫面中

如果您沒有Experience Cloud解決方案的必要存取權，請洽詢您的Experience Cloud管理員。

此外，您也應熟悉Java的Android開發。 您不需要是Java專家就能完成課程，但如果您能輕鬆閱讀並瞭解程式碼，您將可從中獲得更多。

### 驗證對Adobe Target的訪問

這一教訓需要Adobe Target。 在執行後續步驟之前，請執行下列動作，確保您可存取Adobe Target:

1. 登錄[Adobe Experience Cloud](https://experience.adobe.com/)
1. 在Experience Cloud主螢幕中，按一下[!DNL Target] :
   ![Experience Cloud首頁畫面](assets/aec_homeScreen_clickTarget.png)
1. 您應前往Adobe Target的「活動」清單，如下圖所示，您應看到您的使用者擁有「核准者」層級的存取權。 如果您無法存取[!DNL Target]或無法驗證核准者層級的存取權，請連絡您公司的Experience Cloud管理員，請申請此存取權，並在授與本教學課程後繼續本教學課程：

   ![AdobeUI](assets/targetUI_approver.png)

## 關於課程

在這些課程中，您將使用您自己的Adobe Target帳戶，將Adobe Target建置在名為「We.Travel」的示範旅遊應用程式中。 在教學課程結束時，您將根據使用者對應用程式的使用情況，向使用者傳遞個人化訊息！ 最終的個人化體驗如下所示：

![We.Travel應用程式最終版](assets/overview_final_result.jpg)

在We.Travel應用程式中進行實作後，您就可以在自己的行動應用程式中開始使用[!DNL Target]。

開始吧！

**[下一個：「下載並更新範例應用程式」>](download-and-update-the-sample-app.md)**
