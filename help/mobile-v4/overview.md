---
title: Adobe Target與適用於Android的Adobe Mobile Services SDK v4
description: 已使用Adobe Target Mobile Services SDK v4且想要開始使用Android提供個人化應用程式體驗的Android開發人員，最佳起點就是透過Adobe Mobile Services SDK v4AdobeAdobe Target。
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile, Overview
doc-type: tutorial
kt: 3040
exl-id: 20f8ed4f-a86d-4c5e-9296-71a93724caa3
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---

# Adobe Target與適用於Android的Adobe Mobile Services SDK v4 — 概觀

已使用Adobe Target Mobile Services SDK v4且想要開始使用Android提供個人化應用程式體驗的Android開發人員，_具有Adobe Mobile Services SDK v4 for Adobe_&#x200B;的Adobe Target是最佳起點。

提供的示範Android應用程式作用是協助您完成課程。 完成本教學課程後，您應該已準備好開始在自己的Android應用程式中實施[!DNL Target]！

完成此教學課程之後，您將能:

* 驗證[Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=zh-Hant)安裝程式
* 實作下列[!DNL Target]要求型別：
   * 預先擷取[!DNL Target]內容
   * 在單一請求中批次處理多個[!DNL Target]位置(mbox)
   * 封鎖請求（在應用程式顯示前執行）
   * 非封鎖請求（在背景執行）
   * 即時（非快取）
   * 防快取重新擷取
* 將引數新增至增強型個人化的請求
* 建立對象和選件
* 個人化版面
* 推出具有功能標幟的新功能

## 必備條件

在這些課程中，假設您：

* 擁有Adobe Target介面的AdobeID和核准者層級存取權（請參閱下列驗證步驟）
* 知道您的Adobe Target使用者端代碼，以便向自己的帳戶提出請求。 使用者端代碼會顯示在的Adobe Target介面中，   「設定>實作>編輯at.js設定」畫面
* 可以存取並熟悉[Mobile Services使用者介面](https://mobilemarketing.adobe.com/)
* 擁有用於Android行動應用程式開發的IDE。 本教學課程在各個步驟和熒幕擷取畫面中提供[Android Studio](https://developer.android.com/studio/install)

如果您沒有Experience Cloud解決方案所需的存取權，請聯絡您的Experience Cloud管理員。

此外，您也應熟悉使用Java的Android開發流程。 您不需要成為Java專家就能完成這些課程，但如果您熟悉且瞭解程式碼，將能從中學到更多。

### 驗證Adobe Target的存取權

本課程需要存取Adobe Target。 在繼續接下來的步驟之前，請執行以下操作來確保您有權存取Adobe Target：

1. 登入[Adobe Experience Cloud](https://experience.adobe.com/)
1. 在Experience Cloud主畫面中，按一下「[!DNL Target]」：
   ![Experience Cloud主畫面](assets/aec_homeScreen_clickTarget.png)
1. 您應該會前往Adobe Target中的「活動」清單（如下圖所示），且您應該會看到使用者擁有核准者層級的存取權。 如果您無法存取[!DNL Target]或無法驗證核准者層級的存取權，請連絡貴公司的其中一個Experience Cloud管理員，要求此存取權，並在授與教學課程後繼續進行：

   ![Adobe的UI](assets/targetUI_approver.png)

## 關於課程

在這些課程中，您將使用自己的Adobe Target帳戶，將Adobe Target實施至名為「We.Travel」的示範旅遊應用程式中。 在教學課程結束時，您將根據使用者使用應用程式的情形，提供個人化訊息給使用者！ 最終的個人化體驗將如下所示：

![We.Travel應用程式最終版](assets/overview_final_result.jpg)

逐步完成We.Travel應用程式中的實作後，您就能在自己的行動應用程式中開始使用[!DNL Target]。

讓我們開始吧！

**[下一步：「下載並更新範例應用程式」>](download-and-update-the-sample-app.md)**
