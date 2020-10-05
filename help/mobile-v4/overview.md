---
title: Adobe Target搭配Adobe Mobile Services SDK v4 for Android
description: Adobe Target搭配Adobe Mobile Services SDK v4 for Android是已使用Adobe Mobile Services SDK v4且想要開始使用Adobe Target個人化應用程式體驗的Android開發人員的最佳起點。
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: d6cedd55dcc9c08d2d2ca5709e15fe5ea9fab8b8
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---


# Adobe Target搭配Adobe Mobile Services SDK v4 for Android —— 概觀

_Adobe Target搭配Adobe Mobile Services SDK v4 for Android_ ，是已使用Adobe Mobile Services SDK v4且想要開始使用Adobe Target個人化應用程式體驗的Android開發人員的最佳起點。

我們提供示範Android應用程式，讓您完成課程。 完成本教學課程後，您應準備好開始在您自己的Android應 [!DNL Target] 用程式中實作！

完成此教學課程之後，您將能:

* 驗證 [Adobe Mobile Services SDK設定](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html)
* 實作下列類型的 [!DNL Target] 請求：
   * 內容預取 [!DNL Target]
   * 在單一請 [!DNL Target] 求中批次多個位置(mbox)
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

* 擁有Adobe Id和核准者層級的Adobe Target介面存取權（請參閱下方的驗證步驟）
* 瞭解您的Adobe Target用戶端代碼，以便向您自己的帳戶提出要求。 「用戶端程式碼」會顯示在「設定>實作>編輯at.js設定」畫面的Adobe Target介面中
* 存取並熟悉 [Mobile Services使用者介面](https://mobilemarketing.adobe.com)
* 針對Android行動應用程式開發使用IDE。 本教學課程以 [Android Studio](https://developer.android.com/studio/install) ，為各個步驟和螢幕擷取

如果您沒有Experience Cloud解決方案的必要存取權，請洽詢您的Experience Cloud管理員。

此外，您也應熟悉Java的Android開發。 您不需要是Java專家就能完成課程，但如果您能輕鬆閱讀並瞭解程式碼，您將可從中獲得更多。

### 驗證Adobe Target的存取權

本課程需要存取Adobe Target。 在執行後續步驟之前，請執行下列動作，以確保您擁有Adobe Target的存取權：

1. 登入 [Adobe Experience Cloud](https://experience.adobe.com/)
1. 從Experience Cloud首頁畫面，按一下 [!DNL Target]:
   ![Experience Cloud首頁畫面](assets/aec_homeScreen_clickTarget.png)
1. 您應前往Adobe Target中的「活動」清單，如下圖所示，您應該會看到您的使用者擁有「核准者」層級的存取權。 如果您無法存取或 [!DNL Target] 無法驗證核准者層級的存取權，請連絡您公司的其中一位Experience Cloud管理員，請申請此存取權，並在授予本教學課程後繼續本教學課程：

   ![Adobe UI](assets/targetUI_approver.png)

## 關於課程

在這些課程中，您將使用您自己的Adobe Target帳戶，將Adobe Target實作至名為「We.Travel」的示範旅行應用程式。 在教學課程結束時，您將根據使用者對應用程式的使用情況，向使用者傳遞個人化訊息！ 最終的個人化體驗如下所示：

![We.Travel應用程式最終版](assets/overview_final_result.jpg)

在We.Travel應用程式中進行實作後，您就可以開始在自己的行動應 [!DNL Target] 用程式中使用。

開始吧！

**[下一個：「下載並更新範例應用程式」>](download-and-update-the-sample-app.md)**
