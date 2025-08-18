---
title: 如何在 [!DNL Analysis Workspace] 中為 [!DNL Auto-Target] 個活動設定A4T報告
description: 如何在 [!DNL Analysis Workspace] 中設定A4T報告，以便在執行[!UICONTROL Auto-Target]活動時取得預期結果？
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=zh-Hant#premium newtab=true" tooltip="檢視Target Premium包含的內容。"
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
thumbnail: null
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 78e5b5f7fa8f4c1a08c06c6d2b0e1a5242cd464c
workflow-type: tm+mt
source-wordcount: '2430'
ht-degree: 1%

---

# 在[!DNL Analysis Workspace]中為[!DNL Auto-Target]個活動設定A4T報告

>[!IMPORTANT]
>
>針對[!UICONTROL Auto-Target]活動，您必須檢查[!DNL Analytics Workspace]中的報告，並手動建立A4T面板。

[!UICONTROL Analytics for Target]活動的[!DNL Auto-Target] (A4T)整合使用[!DNL Adobe Target]整體機器學習(ML)演演算法，依據訪客的設定檔、行為和內容來選擇每位訪客的最佳體驗，所有這一切都使用[!DNL Adobe Analytics]目標量度。

雖然[!DNL Adobe Analytics] [!DNL Analysis Workspace]中提供了豐富的分析功能，但由於實驗活動（手動&#x200B;**[!UICONTROL Analytics for Target]**&#x200B;和[!DNL Auto-Target]）和個人化活動([!UICONTROL A/B Test])之間的差異，預設[!UICONTROL Auto-Allocate]面板需要一些修改才能正確解譯[!UICONTROL [!UICONTROL Auto-Target]]活動。

此教學課程會逐步引導您瞭解分析[!UICONTROL Auto-Target]中[!DNL Analysis Workspace]個活動的建議修改，這些修改是以下列重要概念為基礎：

* **[!UICONTROL Control vs Targeted]**&#x200B;維度可用來區分[!UICONTROL Control]個體驗與[!UICONTROL Auto-Target]組合ML演演算法所提供的體驗。
* 檢視體驗層級的效能劃分時，瀏覽應作為標準化量度使用。 此外，[Adobe Analytics的預設計數方法可能包含使用者實際上未看到活動內容的造訪](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=zh-Hant#metrics){target=_blank}，但此預設行為可以使用適當範圍的區段來修改（詳細資訊如下）。
* [!DNL Adobe Target] ML模型在其訓練階段會使用造訪回顧範圍歸因（在指定的歸因模型上也稱為「造訪回顧期間」），且在劃分目標量度時應使用相同的（非預設）歸因模型。

## 在[!UICONTROL Auto-Target]中建立[!DNL Analysis Workspace]面板的A4T

若要為[!UICONTROL Auto-Target]報告建立A4T，請從&#x200B;**[!UICONTROL Analytics for Target]**&#x200B;中的[!DNL Analysis Workspace]面板開始（如下所示），或以自由表格開始。 然後進行下列選取：

1. **[!UICONTROL Control Experience]**：您可以選擇任何體驗；不過，您稍後會覆寫此選項。 請注意，對於[!UICONTROL Auto-Target]個活動，控制體驗其實是控制策略，其目的為a)在所有體驗中隨機提供，或b)提供單一體驗（此選項是在[!DNL Adobe Target]中建立活動時做出的）。 即使您已選擇選項(b)，您的[!UICONTROL Auto-Target]活動仍會指定特定體驗作為控制。 您仍然應該遵循本教學課程中概述的方法，分析[!UICONTROL Auto-Target]活動的A4T。
2. **[!UICONTROL Normalizing Metric]**：選取[!UICONTROL Visits]。
3. **[!UICONTROL Success Metrics]**：雖然您可以選取要報告的任何量度，但您通常應該檢視在[!DNL Target]中活動建立期間為最佳化所選取之相同量度的報告。

   ![[!UICONTROL Analytics for Target]活動的[!UICONTROL Auto-Target]面板設定。](assets/Figure1.png)

   *圖1： [!UICONTROL Analytics for Target]活動的[!UICONTROL Auto-Target]面板設定。*

>[!TIP]
>
>若要設定[!UICONTROL Analytics for Target]活動的[!UICONTROL Auto-Target]面板，請選擇任何控制體驗，選擇[!UICONTROL Visits]作為標準化量度，並選擇在[!DNL Target]活動建立期間為最佳化選擇的相同目標量度。

## 使用[!UICONTROL Control vs.Targeted]維度來比較[!DNL Target]組合ML模型與您的控制項

預設A4T面板是針對傳統（手動） [!UICONTROL A/B Test]或[!UICONTROL Auto-Allocate]活動而設計，其目標是比較個別體驗與控制體驗的效能。 但在[!UICONTROL Auto-Target]活動中，第一順序比較應該是在控制&#x200B;*策略*&#x200B;與目標的&#x200B;*策略*&#x200B;之間。 換言之，決定[!UICONTROL Auto-Target]整體ML模型相對於控制策略的整體效能提升度。

若要執行這項比較，請使用&#x200B;**[!UICONTROL Control vs Targeted (Analytics for Target)]**&#x200B;維度。 拖放以取代預設A4T報表中的&#x200B;**[!UICONTROL Target Experiences]**&#x200B;維度。

請注意，此取代會使A4T面板上的預設[!UICONTROL Lift and Confidence]計算失效。 為避免混淆，您可以從預設面板中移除這些量度，並留下下列報表：

![[!UICONTROL Experiences by Activity Conversions]中的[!DNL Analysis Workspace]](assets/Figure2.png)面板

*圖2： [!DNL Auto-Target]活動的建議基準線報告。 此報告已設定為比較目標流量（由整體ML模型提供）與您的控制流量。*

>[!NOTE]
>
>目前，[!UICONTROL Lift and Confidence]的A4T報告的[!UICONTROL Control vs Targeted]個維度無法使用[!UICONTROL Auto-Target]個數字。 在新增支援之前，可藉由下載[!UICONTROL Lift and Confidence]可信度計算器[來手動計算](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=zh-Hant)。

## 新增量度的體驗層級劃分

若要進一步瞭解insight如何執行整體ML模型，您可以檢查&#x200B;**[!UICONTROL Control vs Targeted]**&#x200B;維度的體驗層級劃分。 在[!DNL Analysis Workspace]中，將&#x200B;**[!UICONTROL Target Experiences]**&#x200B;維度拖曳至您的報表，然後分別劃分每個控制項和目標維度。

![[!UICONTROL Experiences by Activity Conversions]中的[!DNL Analysis Workspace]](assets/Figure3.png)面板

*圖3：依目標體驗劃分目標維度*

產生的報表範例顯示於此處。

![[!UICONTROL Experiences by Activity Conversions]中的[!DNL Analysis Workspace]](assets/Figure4.png)面板

*圖4：具有體驗層級劃分的標準[!UICONTROL Auto-Target]報告。 請注意，您的目標量度可能不同，而您的控制策略可能有單一體驗。*

>[!TIP]
>
>在[!DNL Analysis Workspace]中，按一下齒輪圖示以隱藏[!UICONTROL Conversion Rate]欄中的百分比，以協助將焦點保持在體驗轉換率上。 轉換率隨後將格式化為小數，但會據此將其解譯為百分比。

## 為什麼&quot;[!UICONTROL Visits]&quot;是[!UICONTROL Auto-Target]活動的正確標準化量度

分析[!UICONTROL Auto-Target]活動時，請一律選擇[!UICONTROL Visits]作為預設標準化量度。 [!UICONTROL Auto-Target]個人化會在每次造訪時為訪客選取一次體驗（正式地說，每個[!DNL Target]工作階段選取一次），這表示向訪客顯示的體驗可在每次造訪時變更。 因此，如果您使用[!UICONTROL Unique Visitors]作為標準化量度，單一使用者最終可能會看到多個體驗（跨不同造訪）的事實會導致轉換率混亂。

一個簡單的範例將示範這一點：假設有兩個訪客進入一個只有兩個體驗的行銷活動。 第一個訪客造訪兩次。 他們會在第一次造訪時指派給體驗A，但在第二次造訪時指派給體驗B （因為其設定檔狀態在第二次造訪時變更）。 在第二次造訪後，訪客會下訂單進行轉換。 此轉換可歸因於最近顯示的體驗（體驗B）。 第二個訪客也會造訪兩次，且兩次都會顯示體驗B，但絕不會轉換。

讓我們比較訪客層級和造訪層級報表：

| 體驗 | 獨特訪客 | 瀏覽次數 | 轉換 | 訪客標準化轉換率 | 造訪標準化轉換率 |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33.3% |
| 總計 | 2 | 4 | 1 | 50% | 25% |

*表1：比較訪客標準化和造訪標準化的報表範例，適用於決策對造訪有粘性的案例（而非訪客，如同一般A/B測試）。 此情境中的訪客標準化量度令人困惑。*

如表格所示，訪客層級數字明顯不一致。 雖然不重複訪客總數有兩位，但這不是每個體驗的個別不重複訪客的總和。 雖然訪客層級的轉換率未必錯誤，但在比較個別體驗時，造訪層級的轉換率可能更有意義。 在形式上，分析單位（「造訪」）與決定粘著度單位相同，這表示可新增並比較量度的體驗層級劃分。

## 篩選活動的實際造訪

[!DNL Adobe Analytics]活動造訪的[!DNL Target]預設計數方法可能包含使用者未與[!DNL Target]活動互動的造訪。 這是因為[!DNL Target]活動指派持續存在於[!DNL Analytics]訪客內容中的方式。 因此，[!DNL Target]活動的造訪次數有時會膨脹，導致轉換率降低。

如果您偏好報告使用者實際與[!UICONTROL Auto-Target]活動互動的造訪（透過進入活動、顯示或造訪事件，或轉換），您可以：

1. 建立特定區段，包含來自相關[!DNL Target]活動的點選，然後
1. 使用此區段篩選[!UICONTROL Visits]量度。

**若要建立區段：**

1. 選取&#x200B;**[!UICONTROL Components > Create Segment]**&#x200B;工具列中的[!DNL Analysis Workspace]選項。
2. 指定區段的&#x200B;**[!UICONTROL Title]**。 在下列範例中，區段名為[!DNL "Hit with specific Auto-Target activity"]。
3. 將&#x200B;**[!UICONTROL Target Activities]**&#x200B;維度拖曳至區段&#x200B;**[!UICONTROL Definition]**&#x200B;區段。
4. 使用&#x200B;**[!UICONTROL equals]**&#x200B;運運算元。
5. 搜尋您的特定[!DNL Target]活動。
6. 按一下齒輪圖示，然後選取&#x200B;**[!UICONTROL Attribution model > Instance]**，如下圖所示。
7. 按一下 **[!UICONTROL Save]**。

![中的[!DNL Analysis Workspace]](assets/Figure5.png)區段

*圖5：使用如這裡所示的區段來篩選[!UICONTROL Visits]報告[!UICONTROL Auto-Target]的A4T中的*&#x200B;量度

建立區段後，請使用該區段來篩選[!UICONTROL Visits]量度，因此[!UICONTROL Visits]量度僅包含使用者與[!DNL Target]活動互動的造訪。

**若要使用此區段來篩選[!UICONTROL Visits]：**

1. 從元件工具列拖曳新建立的區段，並將滑鼠游標暫留在&#x200B;**[!UICONTROL Visits]**&#x200B;量度標籤的基底上，直到出現藍色&#x200B;**[!UICONTROL Filter by]**&#x200B;提示為止。
2. 發行區段。 篩選器會套用至該量度。

最終面板顯示如下：

![[!UICONTROL Experiences by Activity Conversions]中的[!DNL Analysis Workspace]](assets/Figure6.png)面板

*圖6：套用到[!UICONTROL Visits]量度且「具有特定自動鎖定目標活動的點選」區段的報告面板。 此區段可確保報表中只包含使用者實際與相關[!DNL Target]活動互動的造訪。*

## 確保目標量度和歸因符合最佳化標準

A4T整合允許[!UICONTROL Auto-Target] ML模型使用與&#x200B;*用於*&#x200B;產生效能報表[!DNL Adobe Analytics]的相同轉換事件資料&#x200B;*培訓*。 不過，在訓練ML模型時，必須使用某些假設來解譯此資料，這些假設與[!DNL Adobe Analytics]中報告階段期間所做的預設假設不同。

具體來說，[!DNL Adobe Target] ML模型會使用造訪範圍的歸因模型。 也就是說，ML模型假設轉換必須發生在活動內容的顯示同一次造訪中，才能將轉換「歸因」於ML模型所做的決定。 這是[!DNL Target]保證及時訓練其模型的必要專案；[!DNL Target]無法等待最多30天的時間進行轉換（[!DNL Adobe Analytics]中報表的預設歸因期間），才能將其納入其模型的訓練資料。

因此，[!DNL Target]模型所使用的歸因（培訓期間）與查詢資料所使用的預設歸因（報告產生期間）之間的差異可能會導致差異。 ML模型甚至可能表現不佳，而實際上問題出在歸因上。

>[!TIP]
>
>如果ML模型針對某一量度進行最佳化，而該量度的歸因不同於您在報表中檢視的量度，則模型可能無法如預期般執行。 若要避免此問題，請確保報表上的目標量度使用[!DNL Target] ML模型使用的相同量度定義和歸因。

確切的量度定義和歸因設定取決於您在活動建立期間指定的[最佳化准則](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=zh-Hant#supported){target=_blank}。

### 目標定義的轉換，或具有[!DNL Analytics]最大化的每次造訪量度值&#x200B;*的*&#x200B;個量度

當量度是[!DNL Target]轉換，或具有[!DNL Analytics]每次造訪量度值最大化&#x200B;**的**&#x200B;量度時，目標量度定義允許在同一次造訪中發生多個轉換事件。

若要檢視具有[!DNL Target] ML模型所使用的相同歸因方法的目標量度，請執行下列步驟：

1. 將游標停留在目標量度的齒輪圖示上：

   ![gearicon.png](assets/gearicon.png)

1. 從產生的功能表，捲動至&#x200B;**[!UICONTROL Data settings]**。
1. 選取&#x200B;**[!UICONTROL Use non-default  attribution model]** （如果尚未選取）。

   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1. 按一下 **[!UICONTROL Edit]**。
1. 選取&#x200B;**[!UICONTROL Model]**： **[!UICONTROL Participation]**&#x200B;和&#x200B;**[!UICONTROL Lookback window]**： **[!UICONTROL Visit]**。

   ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)

1. 按一下 **[!UICONTROL Apply]**。

如果目標量度事件發生在有體驗顯示的同一次造訪中的&#x200B;*任何時間* （「參與率」），這些步驟可確保報表將目標量度歸因於體驗的顯示。

### 具有[!DNL Analytics]不重複造訪轉換率&#x200B;*的*&#x200B;量度

**定義具有正面量度區段的造訪**

在您選取&#x200B;*最大化不重複造訪轉換率*&#x200B;作為最佳化條件的案例中，轉換率的正確定義是度量值為正值的造訪次數比例。 若要這麼做，可建立區段篩選，找出量度值為正值的造訪，然後篩選造訪量度。

1. 和之前一樣，在&#x200B;**[!UICONTROL Components > Create Segment]**&#x200B;工具列中選取[!DNL Analysis Workspace]選項。
2. 指定區段的&#x200B;**[!UICONTROL Title]**。

   在下列範例中，區段名為[!DNL "Visits with an order"]。

3. 將您用於最佳化目標的基本量度拖曳至區段。

   在下列範例中，我們使用&#x200B;**訂單**&#x200B;量度，因此轉換率會測量已記錄訂單的造訪次數。

4. 在區段定義容器的左上方，選取&#x200B;**[!UICONTROL Include]** **造訪**。
5. 使用&#x200B;**[!UICONTROL is greater than]**&#x200B;運運算元，並將值設為0。

   將值設為0表示此區段包含訂單量度為正數的造訪。

6. 按一下 **[!UICONTROL Save]**。

![圖7.png](assets/Figure7.png)

*圖7：區段定義會篩選順序列出的造訪。 根據活動的最佳化量度，您必須以適當的量度取代訂單*

**將此套用至活動篩選量度中的造訪**

此區段現在可用來篩選具有正數訂單的造訪，以及[!DNL Auto-Target]活動有點選的造訪。 篩選量度的程式與之前類似，而且在套用新區段至已篩選的造訪量度後，報表面板應該會如圖8所示

![圖8.png](assets/Figure8.png)

*圖8：具有正確不重複造訪轉換量度的報表面板：記錄來自活動的點選，且轉換量度（此範例中的訂單）非零的造訪次數。*

## 最後步驟：建立可擷取上述神奇的轉換率

修改前幾節中的[!UICONTROL Visit]和目標量度後，您對[!DNL Auto-Target]報表面板的預設A4T應進行的最終修改，是建立正確比率的轉換率，也就是正確的目標量度與適當篩選的「造訪」量度的比率。

使用下列步驟建立[!UICONTROL Calculated Metric]，以執行此操作：

1. 選取&#x200B;**[!UICONTROL Components > Create Metric]**&#x200B;工具列中的[!DNL Analysis Workspace]選項。
1. 為您的量度指定&#x200B;**[!UICONTROL Title]**。 例如，「活動XXX的造訪修正轉換率」。
1. 選取&#x200B;**[!UICONTROL Format]** =百分比和&#x200B;**[!UICONTROL Decimal Places]** = 2。
1. 將活動的相關目標量度（例如[!UICONTROL Activity Conversions]）拖曳至定義，然後使用此目標量度上的齒輪圖示，將歸因模型調整為（參與率|造訪），如先前所述。
1. 從&#x200B;**[!UICONTROL Add > Container]**&#x200B;區段的右上角選取&#x200B;**[!UICONTROL Definition]**。
1. 選取兩個容器之間的除(÷)運運算元。
1. 拖曳您先前針對此特定[!UICONTROL Auto-Target]活動在本教學課程中建立的區段（名為「具有特定[!DNL Auto-Target]活動的點選」）。
1. 將&#x200B;**[!UICONTROL Visits]**&#x200B;量度拖曳至區段容器。
1. 按一下 **[!UICONTROL Save]**。

>[!TIP]
>
> 您也可以使用[快速計算量度功能](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=zh-Hant)來建立此量度。

此處顯示完整的計算量度定義。

![圖9.png](assets/Figure9.png)

*圖7：造訪校正和歸因校正的模型轉換率量度定義。 (請注意，此量度取決於您的目標量度和活動。 換句話說，此量度定義無法跨活動重複使用。)*

>[!IMPORTANT]
>
>來自A4T面板的[!UICONTROL Conversion]比率量度未連結至表格中的轉換事件或標準化量度。 當您進行本教學課程中建議的修改時，[!UICONTROL Conversion]費率不會自動適應這些變更。 因此，如果您修改轉換事件歸因或標準化量度（或兩者），您必須記住的最後一個步驟也是修改[!UICONTROL Conversion]比率，如上所示。

## 摘要： [!DNL Analysis Workspace]報告的最後範例[!UICONTROL Auto-Target]面板

將上述所有步驟合併成單一面板，下圖顯示[!UICONTROL Auto-Target]個A4T活動的建議報告完整檢視。 此報表與[!DNL Target] ML模型用來最佳化目標量度的報表相同。 此報表包含本教學課程中討論的所有細微差別和建議。 此報表也最接近傳統[!DNL Target]報表導向[!UICONTROL Auto-Target]活動中使用的計數方法。

按一下以展開影像。

在Analysis Workspace的![A4T報告中[!DNL Analysis Workspace]](assets/Figure10.png "最終的A4T報告"){width="600" zoomable="yes"}

*圖10： [!UICONTROL Auto-Target] [!DNL Adobe Analytics]中的最終A4T [!DNL Workspace]報告，此報告結合本教學課程前幾節中說明的所有量度定義調整。*
