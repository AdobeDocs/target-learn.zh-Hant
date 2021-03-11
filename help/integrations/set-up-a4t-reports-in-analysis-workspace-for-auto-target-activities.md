---
title: 如何在Analysis Workspace為自動定位活動設定A4T報表
description: 如何在Analysis Workspace設定A4T報表，以便在執行Auto-Target活動時取得預期結果
kt: null
audience: business user
doc-type: tutorial
activity: use, setup
feature: Analytics for Target(A4T)、Auto-Target
topic: Analytics for Target(A4T)、Auto-Target
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: bb3b6e65f8c21c180b46b635268c220d882787cb
workflow-type: tm+mt
source-wordcount: '2235'
ht-degree: 1%

---


# 如何在Analysis Workspace為[!DNL Auto-Target]活動設定A4T報告

[!DNL Auto-Target]活動的Analytics for Target(A4T)整合使用Adobe Target的整合機器學習(ML)演算法，根據每位訪客的描述檔、行為和上下文選擇最佳體驗，同時使用Adobe Analytics目標量度。

雖然Adobe AnalyticsAnalysis Workspace有豐富的分析功能，但由於實驗活動（手動A/B和自動分配）和個人化活動([!DNL Auto-Target])之間的差異，需要對預設&#x200B;**[!UICONTROL Analytics for Target]**&#x200B;面板進行一些修改，以正確解譯[!DNL Auto-Target]活動。

本文將逐步介紹分析Workspace中[!DNL Auto-Target]活動的建議修改，這些修改基於以下主要概念：

* **[!UICONTROL Control與Targeted]**&#x200B;維度可用來區分控制體驗與[!DNL Auto-Target]整合ML演算法所提供體驗。
* 在檢視「體驗」層級的效能劃分時，瀏覽應當用作標準化度量。 此外，[Adobe Analytics的預設計數方法可能包括使用者實際未看見活動內容](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics)的瀏覽，但此預設行為可透過使用適當範圍的區段來修改（詳細資料如下）。
* Adobe Target的ML模型在其培訓階段使用瀏覽回顧範圍歸因（也稱為指定歸因模型上的「瀏覽回顧視窗」），在劃分目標量度時最好使用相同的（非預設）歸因模型。

## 在工作區中為[!DNL Auto-Target]面板建立A4T

若要建立[!DNL Auto-Target]報表的A4T，請從工作區中的「Analytics for Target」面板開始（如下所示），或從自由表格開始。 然後進行下列選擇：

1. **[!UICONTROL 控制體驗]**:您可以選擇任何經驗；不過，我們稍後會覆寫此選項。請注意，對於[!DNL Auto-Target]活動，控制體驗實際上是一種控制策略，其對象為a)在所有體驗中隨機提供，或b)提供單一體驗(此選項是在Adobe Target的活動建立時選擇)。 即使您選擇(b)—您的[!DNL Auto-Target]活動將特定體驗指定為控制項——您仍應遵循本文中概述的方法，來分析[!DNL Auto-Target]活動的A4T。
1. **[!UICONTROL 標準化量度]**:選擇瀏覽。
1. **[!UICONTROL 成功度量]**:雖然您可以選取要報告的任何量度，但您通常應檢視在Adobe Target建立活動期間針對最佳化所選擇之量度的報表。

![圖1.](assets/Figure1.png)
*png圖1:活動的Analytics for Target面板設 [!DNL Auto-Target] 定。*

>[!NOTE]
>
>若要為Auto-Target活動設定Analytics的Target面板，請選擇任何控制體驗，選擇「瀏覽」作為標準化度量，並選擇與建立Target活動期間選擇用於最佳化的相同目標度量。

## 使用「控制項與目標」維度，比較Adobe Target的整合ML模型與您的控制項

預設的A4T面板是專為傳統（手動）A/B測試或自動分配活動而設計，其目標是比較個別體驗與控制體驗的效能。 但是，在[!DNL Auto-Target]活動中，一級比較應是在控制&#x200B;*策略*&#x200B;和目標&#x200B;*策略*&#x200B;之間（換言之，確定[!DNL Auto-Target]整合ML模型對控制策略的整體效能的提升度）。

若要執行此比較，請使用&#x200B;**[!UICONTROL 「控制與定位」(Analytics for Target)]**&#x200B;維度。 拖放以取代預設A4T報表中的&#x200B;**[!UICONTROL Target Experiences]**&#x200B;維度。

請注意，此取代會使A4T面板上的預設提升度和可信度計算失效。 為避免混淆，您可從預設面板移除這些量度，並保留下列報表：

![圖2.](assets/Figure2.png)
*png圖2:建議的活動基準 [!DNL Auto-Target] 報告。此報告已設定成將「目標」流量（由整合ML模型提供）與您的「控制」流量*&#x200B;進行比較

>[!NOTE]
>
>目前，自動定位的A4T報表的「控制」與「目標」維度無法使用「提升度」與「信賴度」數字。 在新增支援之前，您可下載[信賴計算器](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en)，以手動方式計算提升度和信賴度。

## 瞭解量度的體驗層級劃分

若要進一步瞭解整合ML模型的執行方式，您可以檢查&#x200B;**[!UICONTROL 控制與定位]**&#x200B;維度的體驗層級劃分。 在工作區中，將&#x200B;**[!UICONTROL Target Experiences]**&#x200B;維度拖曳至您的報表上，然後分別劃分控制項和目標維度。

![圖3.](assets/Figure3.png)
*png圖3:依Target體驗劃分目標維度*

此處顯示產生報表的範例。

![圖4.](assets/Figure4.png)
*png圖4:具有體驗 [!DNL Auto-Target] 層級劃分的標準報表。請注意，您的目標量度可能不同，而您的控制策略可能有單一體驗。*

>[!TIP]
>
>在工作區中，按一下齒輪圖示可隱藏「轉換率」欄中的「百分比」，以協助您專注於體驗轉換率。 請注意，轉換率隨後會格式化為小數，但會依此解譯為百分比。

## 為什麼「瀏覽」是[!DNL Auto-Target]活動的正確標準化度量

分析[!DNL Auto-Target]活動時，請一律選擇「瀏覽」作為預設標準化度量。 [!DNL Auto-Target] 個人化會為訪客選取每次瀏覽一次的體驗(正式為每次Adobe Target作業一次)，這表示向使用者顯示的體驗可在每次瀏覽時變更。因此，如果我們使用獨特訪客作為標準化度量，那麼單一使用者最終可能會看到多個體驗（跨不同瀏覽），這會導致混淆轉換率。

一個簡單的示例演示了這一點：請考慮兩個訪客進入只有兩個體驗之促銷活動的情形。 第一個訪客瀏覽兩次。 他們會在第一次瀏覽時指派至體驗A，但在第二次瀏覽時指派至體驗B（因為他們的描述檔狀態在第二次瀏覽時會變更）。 第二次瀏覽後，訪客會下單進行轉換。 轉換歸因於最近顯示的體驗（體驗B）。 第二個訪客也瀏覽了兩次，而且兩次都顯示體驗B，但從未轉換。

讓我們比較訪客層級和瀏覽層級報表：

| 體驗 | 獨特訪客 | 瀏覽次數 | 轉換 | 訪客規範。 康夫。 比率 | 瀏覽規範。 康夫。 比率 |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 3 | - | 0% | 0% |
| B | 2 | 3 | 3 | 50% | 33.3% |
| 總計 | 2 | 4 | 1 | 50% | 25% |
*表1:比較訪客標準化和瀏覽標準化報表的範例，其中決策與瀏覽（而非訪客，如同一般A/B測試）有關。在此案例中，訪客標準化量度會令人混淆。*

如表格所示，訪客層級的數字明顯不一致。 儘管有兩個獨特訪客總數，但這並非每個體驗的個別獨特訪客總和。 雖然訪客層級的轉換率不一定是錯的，但當您比較個別體驗時，瀏覽層級的轉換率可以說更有意義。 從形式上講，分析單位（「瀏覽」）與決策粘性單位相同，這表示對度量的體驗層級劃分進行總和和比較是有意義的。

## 進階：非預設瀏覽計數方法

Adobe Analytics對Target活動的瀏覽的預設計數方法可能包括使用者未與Target活動互動的瀏覽。 這是由於Target活動指派在Analytics訪客內容中的持續存在方式所致。 因此，對Target活動的瀏覽次數有時會被誇大，導致轉換率降低。

如果您想要報告使用者實際與「自動定位」活動互動的瀏覽（透過活動的登入、顯示／瀏覽事件或轉換），您可以：

1. 建立特定區段，其中包含有關Target活動的點擊，然後
1. 使用此區段篩選「瀏覽」度量。

### 若要建立正確的區段：

1. 在「工作區」工具列中，選取「**[!UICONTROL 元件>建立區段]**」選項。
1. 輸入區段的&#x200B;**[!UICONTROL 標題]**。 在下列範例中，區段名稱為[!DNL "Hit with specific Auto-Target activity"]。
1. 將&#x200B;**[!UICONTROL Target活動]**&#x200B;維度拖曳至區段&#x200B;**[!UICONTROL 定義]**&#x200B;區段。
1. 使用&#x200B;**[!UICONTROL equals]**&#x200B;運算子。
1. 搜尋您的特定Target活動。
1. 選擇齒輪表徵圖，然後選擇&#x200B;**[!UICONTROL Attribution model > Instance]**，如下圖所示。
1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

![圖5.](assets/Figure5.png)
*png圖5:使用此處顯示的區段等區段，以篩選A4T報表中的「瀏覽」度 [!DNL Auto-Target] 量*

建立區段後，我們可使用它來篩選「瀏覽」度量，以便僅包含使用者與「目標」活動互動的瀏覽。

### 若要使用此區段篩選瀏覽：

1. 從元件工具列拖曳新建立的區段，將滑鼠指標暫留在&#x200B;**[!UICONTROL 瀏覽]**&#x200B;量度標籤的底端，直到出現藍色的&#x200B;**[!UICONTROL 依]**&#x200B;篩選提示。
1. 釋放區段。 篩選器將套用至該量度。

最終面板將顯示如下。

![圖6.](assets/Figure6.png)
*png圖6:報表面板，其中「特定自動定位活動的點擊」區段已套用至「訪客」  量度。這可確保只有使用者實際與相關Target活動互動的瀏覽才會納入報表。*

## 進階：目標量度的瀏覽範圍歸因

A4T整合可讓[!DNL Auto-Target]的ML模型使用與用於在Adobe Analytics產生效能報告&#x200B;*的相同轉換事件資料*&#x200B;訓練&#x200B;*。*&#x200B;然而，在培訓ML模型時，在解釋此資料時必須採用若干假設，與Adobe Analytics報告階段所作之預設假設不同。

尤其是，Adobe Target的ML模型使用瀏覽範圍歸因模型。 也就是說，他們假設轉換必須發生在與活動內容顯示相同的瀏覽中，以便將轉換「歸因」於ML模型所做的決策。 這是Target保證及時培訓其模型的必要條件；Target在將轉換(Adobe Analytics報表的預設歸因視窗)納入其模型的訓練資料之前，無法等待30天。

因此，Target模型（在培訓期間）使用的歸因與查詢資料（在報告產生期間）使用的預設歸因之間的差異，可能會導致不一致。 ML模型甚至可能表現不佳，但實際上問題在于歸因。

>[!TIP]
>
>如果ML模型針對與您在報表中檢視之量度不同的量度進行最佳化，則模型的效能可能不如預期！ 若要避免這種情況，請確定報表上的目標量度使用與Target ML模型使用的相同歸因。

若要檢視與Adobe TargetML模型使用相同歸因方法的目標量度，請遵循下列步驟：

1. 將滑鼠指標暫留在目標量度的齒輪圖示上：
   ![gearicon.png](assets/gearicon.png)
1. 從產生的功能表，捲動至&#x200B;**[!UICONTROL 資料設定]**。
1. 選擇&#x200B;**[!UICONTROL 使用非預設歸因模型]**（如果尚未選取）:
   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)
1. 按一下&#x200B;**[!UICONTROL 編輯]**。
1. 選擇&#x200B;**[!UICONTROL Model]**:**[!UICONTROL 參與率]**&#x200B;和&#x200B;**[!UICONTROL 回顧視窗]**:**[!UICONTROL 瀏覽]**。
   ![ParticitionbyVisit.png](assets/ParticipationbyVisit.png)
1. 按一下&#x200B;**[!UICONTROL 「套用」]**。

這些步驟可確保您的報表將目標度量歸因於體驗的顯示，如果目標度量事件在顯示體驗的同一次瀏覽中隨時發生&#x200B;*（「參與率」）。*

## 最終步驟：瀏覽範圍歸因與篩選瀏覽標準化的轉換率

在前幾節中對「瀏覽」和「目標」量度所做的修改後，您對[!DNL Auto-Target]報表面板的預設A4T所做的最終修改，是建立正確比率的轉換率，即目標量度與適當篩選的「瀏覽」量度的轉換率。

若要這麼做，請使用下列步驟建立計算量度：

1. 在「工作區」工具列中選取「**[!UICONTROL 元件>建立量度]**」選項。
1. 輸入量度的&#x200B;**[!UICONTROL 標題]**。 例如，「活動XXX的瀏覽更正轉換率」。
1. 選擇&#x200B;**[!UICONTROL 格式]** =百分比和&#x200B;**[!UICONTROL 小數位數]** = 2。
1. 將您活動的相關目標量度（例如「活動轉換」）拖曳至定義中，然後使用此目標量度上的齒輪圖示，將歸因模型調整為（參與率|瀏覽），如前所述。
1. 從&#x200B;**[!UICONTROL 定義]**&#x200B;區段的右上角選擇&#x200B;**[!UICONTROL 添加>容器]**。
1. 在兩個容器之間選取除法(altar)運算子。
1. 針對此特定[!DNL Auto-Target]活動，拖曳您先前建立的區段——在本文中命名為「Hit with specific [!DNL Auto-Target] activity」。
1. 將&#x200B;**[!UICONTROL 瀏覽]**&#x200B;量度拖曳至區段容器。
1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

此處顯示完整的計算量度定義。

![圖7.](assets/Figure7.png)
*png圖7:瀏覽和歸因修正的模型轉換率度量定義。(請注意，此量度取決於您的目標量度和活動。 換言之，此量度定義無法跨活動重複使用。)*

>[!IMPORTANT]
>
>來自A4T面板的「轉換率」量度不會連結至表格中的轉換事件或標準化量度。 當您進行本文中建議的修改時，轉換率不會適應變更。 因此，如果您對轉換事件歸因和標準化度量中的一個（或兩者）進行修改，則您必須記住最後一個步驟，才能修改轉換率，如上所示。

## 摘要：[!DNL Auto-Target]報告的最終工作區範例面板

將上述所有步驟結合為單一面板，下圖顯示[!DNL Auto-Target] A4T活動建議報表的完整檢視。 此報告與Target機器學習模型用來最佳化目標量度的報告相同，並整合了本文中討論的所有細微差別和建議。 此報告也最接近傳統Target報告導向[!DNL Auto-Target]活動所使用的計數方法。

![圖8.](assets/Figure8.png)
*png圖8:Adobe Analytics工作區中 [!DNL Auto-Target] 的最終A4T報表，其中結合本檔案上一節所述之量度定義的所有調整。*
