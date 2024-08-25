---
title: 在Adobe Target中建立對象和選件
description: 在本課程中，我們會針對先前課程中實作的三個位置，在Adobe Target中建立對象和選件。 這些區段將在下一個課程中用於顯示個人化體驗。
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 4b153e4f-a979-49a8-8c26-f7ac95162a2f
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 1%

---

# 在Adobe Target中建立對象和選件

在本課程中，我們將進入[!DNL Target]介面，針對我們在先前課程中實作的三個位置建立對象和選件。

## 學習目標

在本課程結束時，您將能夠：

* 在 Adobe Target 中建立客群
* 在Adobe Target中建立優惠方案

更具體來說，在本課程中，我們將建立完成教學課程開頭定義的個人化使用案例所需的對象和選件。 我們希望使用「首頁」和「搜尋」畫面來協助應用程式使用者預訂行程，並使用「感謝您」畫面來根據使用者的目的地顯示一些相關促銷活動。 下表代表我們將在本課程中為每個位置建立的內容：

| 位置 | 客群 | 產品建議 |
| --- | --- | --- |
| wetravel_engage_home | 新行動應用程式使用者 | 選取您的來源和目的地以搜尋可用的巴士路線 |
| wetravel_engage_search | 新行動應用程式使用者 | 「使用篩選器縮小搜尋結果的範圍」 |
| wetravel_engage_home | 回訪行動應用程式使用者 | 「歡迎回來！ 結帳時使用促銷代碼BACK30，即可獲得10%的折扣。」 |
| wetravel_engage_search | 回訪行動應用程式使用者 | 預設內容 |
| wetravel_context_dest | 目的地：聖地亞哥 | &quot;DJ&quot; |
| wetravel_context_dest | 目的地：洛杉磯 | &quot;通用&quot; |

## 選取您的Workspace

如果您的公司使用「屬性」和「工作區」來建立個人化應用程式和網站的邊界，而且您已在上個課程中實作at_property引數，則在繼續本課程前，您應該先確定您位於正確的Workspace中。 如果您未使用「屬性」和「工作區」，請忽略此步驟。 選取您在上一個課程中使用的Workspace以複製at_property值：

![Workspace範例](assets/workspace.jpg)

## 建立對象

現在，讓我們建立受眾，以用於個人化應用程式。

### 為新使用者建立對象

Adobe Target Audiences用於識別特定的訪客群組。 然後可將選件鎖定為這些特定群組。 對於前兩個位置，我們將使用「新使用者」對象：

1. 按一下頂端導覽列中的&#x200B;**[!UICONTROL Audiences]**。
1. 按一下&#x200B;**[!UICONTROL Create Audience]**按鈕。
   ![建立新的使用者對象](assets/audience_new_mobile_app_users_1.jpg)

1. 輸入&#x200B;**[!UICONTROL New Mobile App Users]**&#x200B;作為對象名稱。
1. 選取&#x200B;**[!UICONTROL Add Rule]**。
1. 選取&#x200B;**[!UICONTROL Custom]**規則。
   ![建立新的使用者對象](assets/audience_new_mobile_app_users_2.jpg)

1. 選取&#x200B;**[!UICONTROL a.Launches]**。
1. 選取&#x200B;**[!UICONTROL is less than]**。
1. 輸入&#x200B;**5**。
1. 儲存新對象。
   ![建立新的使用者對象](assets/audience_new_mobile_app_users_3.jpg)

### 為回訪使用者建立受眾

請依照上述步驟，為再度訪問的使用者建立對象。

1. 將對象命名為&#x200B;_傳回行動應用程式使用者_。
1. 使用&#x200B;**[!UICONTROL a.Launches is greater than or equal to 5]**&#x200B;作為自訂規則。
1. 儲存新對象。

   ![建立回訪的使用者對象](assets/audience_returning_mobile_app_users.jpg)

>[!NOTE]
>
>在[!DNL Target]行動SDK中收集的所有生命週期量度和維度都會加上前置詞「a」（例如a.Launches），且可在下拉式選單的「自訂」選項中使用，也可用來建立對象。

### 為預訂聖地亞哥之旅的使用者建立受眾

接下來，我們將為We.Travel應用程式提供的部分目的地建立一些對象。 在上一課中，我們已將目的地作為location引數傳入wetravel_context_dest位置請求中。 下拉式選單的「自訂」選項中可使用該引數。

>[!NOTE]
>
>如果您預期會在「自訂」下拉式清單中看到的引數未出現在[!DNL Target]介面中，請仔細檢查請求中是否確實傳送了該引數。 如果您已驗證位於請求中，但尚未延遲載入至[!DNL Target]介面，您只需輸入引數名稱並按Enter鍵，即可繼續定義您的對象

1. 將對象命名為&#x200B;_目的地： San Diego_。
1. 使用此定義的自訂規則： _locationDest包含San Diego_。
1. 儲存新對象。

   ![建立「聖地亞哥」對象](assets/audience_locationDest_san_diego.jpg)

### 為預訂洛杉磯之旅的使用者建立受眾

1. 將對象命名為&#x200B;_目的地：洛杉磯_
1. 使用此定義的自訂規則： _locationDest包含Los Angeles_
1. 儲存新對象。

![建立「洛杉磯」對象](assets/audience_locationDest_los_angeles.jpg)

## 建立優惠方案

現在，讓我們建立選件以顯示這些訊息。 提醒您，選件是程式碼/內容的片段，會在[!DNL Target]回應中傳送。 它們通常在[!DNL Target]使用者介面中建立，但也可以透過API或使用與Adobe Experience Manager整合的體驗片段來建立。 在行動應用程式中，JSON選件很常見。 在本教學課程中，我們將使用HTML選件，其可用於將任何純文字內容（包括JSON）傳遞至應用程式。

### 為新使用者建立選件

首先，建立訊息的優惠方案給新使用者：

1. 按一下頂端導覽列中的&#x200B;**[!UICONTROL Offers]**。
1. 按一下 **[!UICONTROL Create]**。
1. 選取&#x200B;**[!UICONTROL HTML Offer]**。

   ![建立主選件](assets/offer_home_1.jpg)

1. 將優惠方案命名為&#x200B;_首頁：與新使用者互動_。
1. 輸入&#x200B;_選取Source和目的地以搜尋可用的匯流排_&#x200B;作為代碼。
1. 儲存新選件。

   ![建立首頁HTML選件](assets/offer_home_2.jpg)

### 為回訪使用者建立選件

現在，讓我們為回訪使用者建立一個選件（第二個選件將是預設內容，將不顯示任何內容）：

1. 將選件命名為&#x200B;_首頁：回訪使用者_。
1. 請輸入&#x200B;_歡迎回來！ 結帳時使用促銷代碼BACK30可獲得10%的折扣。_&#x200B;作為HTML代碼。
1. 儲存新選件。

   ![建立首頁HTML選件](assets/offer_home_returning_users.jpg)

### 建立San Diego選件

當「DJ」傳回ThankYou活動時，filterRecommendationBasedOnOffer()函式中的邏輯會顯示「Rock Night with DJ SAM」的橫幅：

1. 為San Diego的促銷活動命名&#x200B;__。
1. 輸入&#x200B;_DJ_&#x200B;作為HTML代碼。
1. 儲存新選件。

![建立「San Diego」選件](assets/offer_san_diego.jpg)

### 為前往洛杉磯的使用者建立優惠方案

當「Universal」傳回ThankYou活動時，filterRecommendationBasedOnOffer()函式中的邏輯會顯示「Universal Studios」的橫幅：

1. 為優惠方案命名&#x200B;_洛杉磯促銷活動_。
1. 輸入&#x200B;_Universal_&#x200B;作為HTML代碼。
1. 儲存新選件。

![建立「洛杉磯」優惠方案](assets/offer_los_angeles.jpg)

## 結論

現在我們有了「對象」和「選件」。 在下一個課程中，我們將建立將位置、對象和選件連結在一起的活動，以建立個人化體驗！

**[下一步：「個人化版面配置」>](personalize-layouts.md)**
