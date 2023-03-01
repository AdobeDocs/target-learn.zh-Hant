---
title: 如何在 [!DNL Analysis Workspace] for [!DNL Auto-Target] 活動
description: 如何在 [!DNL Analysis Workspace] 在運行時獲取預期結果 [!UICONTROL 自動鎖定目標] 活動？
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium" tooltip="See what's included in Target Premium."
badgeBeta: label="Beta" type="Informative"
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 12dc82a96a8df234d02dc56e9e5904571f2152ba
workflow-type: tm+mt
source-wordcount: '2636'
ht-degree: 1%

---

# 在中設定A4T報表 [!DNL Analysis Workspace] for [!DNL Auto-Target] 活動

>[!NOTE]
>
>此功能目前仍在測試中，將可供所有使用 [Target Premium](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium){target=_blank} 客戶。

>[!IMPORTANT]
>
>針對 [!UICONTROL 自動鎖定目標] 活動，您必須在 [!DNL Analytics Workspace] 和手動建立A4T面板。

此 [!UICONTROL Analytics for Target] (A4T)整合 [!DNL Auto-Target] 活動使用 [!DNL Adobe Target]的整體機器學習(ML)演算法，可根據訪客的設定檔、行為和內容，為每位訪客選擇最佳體驗，同時使用 [!DNL Adobe Analytics] 目標量度。

雖然 [!DNL Adobe Analytics] [!DNL Analysis Workspace]，對預設值進行一些修改 **[!UICONTROL Analytics for Target]** 需要面板才能正確解譯 [!DNL Auto-Target] 活動，因為實驗活動（手動A/B和自動分配）與個人化活動([!UICONTROL 自動鎖定目標])。

本教學課程將逐步說明分析時的建議修改 [!UICONTROL 自動鎖定目標] 活動 [!DNL Workspace]，這些概念以下列重要概念為基礎：

* 此 **[!UICONTROL 控制與目標]** 維度可用來區分控制體驗和提供的體驗 [!UICONTROL 自動鎖定目標] 整合ML算法。
* 檢視體驗層級績效劃分時，應將造訪設為標準化量度。 此外， [Adobe Analytics的預設計數方法可能包含使用者實際上看不到活動內容的造訪](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics)，但可使用適當範圍的區段來修改此預設行為（詳見下方）。
* 使用的是造訪回顧範圍歸因（在指定的歸因模型上稱為「造訪回顧期間」） [!DNL Adobe Target]在其訓練階段建立的ML模型，而劃分目標量度時，應使用相同的（非預設）歸因模型。

## 為建立A4T [!UICONTROL 自動鎖定目標] 面板 [!DNL Workspace]

為建立A4T [!UICONTROL 自動鎖定目標] 報表，以開頭 **[!UICONTROL Analytics for Target]** 面板 [!DNL Workspace]，如下所示，或以自由表格開頭。 然後進行下列選取：

1. **[!UICONTROL 控制體驗]**:您可以選擇任何體驗；不過，您稍後會覆寫此選項。 請注意， [!UICONTROL 自動鎖定目標] 活動，控制體驗實際上是控制策略，可能是a)在所有體驗中隨機提供，或b)提供單一體驗(此選項是在活動建立時於 [!DNL Adobe Target])。 即使您選擇(b)- [!UICONTROL 自動鎖定目標] 將特定體驗指定為控制的活動 — 您仍應遵循本教學課程中概述的方法，來分析 [!UICONTROL 自動鎖定目標] 活動。
2. **[!UICONTROL 標準化量度]**:選取造訪。
3. **[!UICONTROL 成功量度]**:雖然您可以選取要報告的任何量度，但一般應檢視所選用於最佳化的相同量度的報告，此量度在 [!DNL Target].

![圖1.png](assets/Figure1.png)
*圖1: [!UICONTROL Analytics for Target] 面板設定 [!UICONTROL 自動鎖定目標] 活動。*

>[!NOTE]
>
>設定 [!UICONTROL Analytics for Target] 面板 [!UICONTROL 自動鎖定目標] 活動，選擇任何控制體驗，選擇 [!UICONTROL 瀏覽] 做為標準化量度，然後選擇與 [!DNL Target] 活動建立。

## 使用 [!UICONTROL 控制與目標] 要比較的維度 [!DNL Target] 將整體ML模型整合到控制項

預設的A4T面板專為傳統（手動）A/B測試或 [!UICONTROL 自動分配] 目標是比較個別體驗與控制體驗的效能的活動。 在 [!UICONTROL 自動鎖定目標] 不過，第一階比較應該是控制項之間 *策略* 和目標 *策略* (換言之，決定 [!UICONTROL 自動鎖定目標] 整體ML模型（控制策略）。

若要執行此比較，請使用 **[!UICONTROL 控制與鎖定(Analytics for Target)]** 維度。 拖放以取代 **[!UICONTROL 目標體驗]** 維度。

請注意，此取代會讓A4T面板的預設提升度和可信度計算失效。 若要避免混淆，您可以從預設面板中移除這些量度，並保留下列報表：

![圖2.png](assets/Figure2.png)

*圖2:建議的基準報告 [!DNL Auto-Target] 活動。 此報表已設定來比較目標流量（由整體ML模型提供）和您的控制流量。*

>[!NOTE]
>
>目前，提升度和可信度數字不適用於 [!UICONTROL 控制與目標] 維度(適用於 [!UICONTROL 自動鎖定目標]. 在新增支援之前，您可以借由下載 [信賴度計算器](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en).

## 加入量度的體驗層級劃分

若要進一步了解整體ML模型的執行方式，您可以檢查 **[!UICONTROL 控制與目標]** 維度。 在 [!DNL Workspace]，拖曳 **[!UICONTROL 目標體驗]** 維度，然後分別劃分「控制」和「目標」維度。

![圖3.png](assets/Figure3.png)
*圖3:依目標體驗劃分目標維度*

產生的報表範例如下所示。

![圖4.png](assets/Figure4.png)
*圖4:標準 [!UICONTROL 自動鎖定目標] 包含體驗層級劃分的報表。 請注意，您的目標量度可能不同，而您的控制策略可能只有單一體驗。*

>[!TIP]
>
>在 [!DNL Workspace]，按一下齒輪圖示以隱藏 [!UICONTROL 轉換率] 欄，協助您持續關注體驗轉換率。 請注意，轉換率將格式化為小數，但會據此解譯為百分比。

## 為何「造訪」是 [!UICONTROL 自動鎖定目標] 活動

分析 [!UICONTROL 自動鎖定目標] 活動，一律選擇 [!UICONTROL 瀏覽] 做為預設標準化量度。 [!UICONTROL 自動鎖定目標] 個人化會為訪客在每次造訪時選取一次體驗(正式、每次 [!DNL Adobe Target] 工作階段)，這表示向使用者顯示的體驗可在每次造訪時變更。 因此，若您使用 [!UICONTROL 不重複訪客] 標準化量度時，單一使用者最後可能看到多個體驗（跨不同的造訪），將導致轉換率混淆。

一個簡單的示例演示了此點：假設有兩個訪客進入的促銷活動只有兩個體驗。 第一個訪客瀏覽兩次。 他們會在第一次造訪時指派給體驗A，但在第二次造訪時指派給體驗B（因為其設定檔狀態在第二次造訪時有所變更）。 第二次造訪後，訪客會透過下單進行轉換。 轉換會歸因於最近顯示的體驗（體驗B）。 第二個訪客也瀏覽了兩次，且兩次都顯示體驗B，但從未轉換。

讓我們比較訪客層級和造訪層級報表：

| 體驗 | 獨特訪客 | 瀏覽次數 | 轉換 | 訪客基準。 康夫。 比率 | 訪問規範。 康夫。 比率 |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33.3% |
| 總計 | 2 | 4 | 1 | 50% | 25% |

*表1:比較訪客標準化報表和造訪標準化報表的範例，其中決策與造訪有黏性（而非訪客，如同一般A/B測試）。 此情境中會混淆訪客標準化量度。*

如表格所示，訪客層級的數字有明顯的不一致。 儘管事實上有兩個不重複訪客總計，但這並非每個體驗的個別不重複訪客總和。 雖然訪客層級轉換率不一定是錯誤的，但比較個別體驗時，瀏覽層級的轉換率可以說更合理。 從形式上講，分析單位（「造訪」）與決策黏著度單位相同，這表示可以新增和比較量度的體驗層級劃分。

## 篩選活動的實際造訪次數

此 [!DNL Adobe Analytics] 造訪的預設計數方法 [!DNL Target] 活動可能包括使用者未與 [!DNL Target] 活動。 這是因為 [!DNL Target] 活動指派持續存在於 [!DNL Analytics] 訪客內容。 因此， [!DNL Target] 活動有時會膨脹，導致轉換率下降。

如果您偏好報告使用者實際與互動的造訪 [!UICONTROL 自動鎖定目標] 活動（透過活動、顯示/造訪事件或轉換），您可以：

1. 建立特定區段，其中包含 [!DNL Target] 相關活動，然後
1. 篩選 [!UICONTROL 瀏覽] 量度。

**若要建立區段：**

1. 選取 **[!UICONTROL 元件>建立區段]** 選項 [!DNL Workspace] 工具欄。
2. 輸入 **[!UICONTROL 標題]** 的URL區段。 在下列範例中，區段的名稱為 [!DNL "Hit with specific Auto-Target activity"].
3. 拖曳 **[!UICONTROL 目標活動]** 維度至區段 **[!UICONTROL 定義]** 區段。
4. 使用 **[!UICONTROL 等於]** 運算元。
5. 搜尋您的特定 [!DNL Target] 活動。
6. 選取齒輪圖示，然後選取 **[!UICONTROL 歸因模型>例項]** 如下圖所示。
7. 按一下&#x200B;**[!UICONTROL 儲存]**。

![圖5.png](assets/Figure5.png)
*圖5:使用區段（如此處所示）來篩選 [!UICONTROL 瀏覽] 量度 [!UICONTROL 自動鎖定目標] 報告*

建立區段後，使用它來篩選 [!UICONTROL 瀏覽] 量度，因此 [!UICONTROL 瀏覽] 量度僅包含使用者與 [!DNL Target] 活動。

**若要篩選 [!UICONTROL 瀏覽] 使用此區段：**

1. 從元件工具列拖曳新建立的區段，並將滑鼠移到 **[!UICONTROL 瀏覽]** 量度標籤直到藍色 **[!UICONTROL 篩選依據]** 出現提示。
2. 發行區段。 篩選器會套用至該量度。

最終面板將顯示如下。

![圖6.png](assets/Figure6.png)
*圖6:報表面板，其中「點擊特定自動鎖定目標活動」區段已套用至 [!UICONTROL 瀏覽] 量度。 這可確保只有使用者實際與互動的造訪 [!DNL Target] 相關活動會包含在報表中。*

## 確定目標量度和歸因與您的最佳化標準一致

A4T整合可讓 [!UICONTROL 自動鎖定目標] 要為的ML模型 *訓練* 使用與 [!DNL Adobe Analytics] 使用 *生成效能報告*. 然而，在培訓ML模型時，在解釋此資料時，必須採用若干假設，這與在報告階段(即 [!DNL Adobe Analytics].

具體而言， [!DNL Adobe Target] ML模型使用造訪範圍歸因模型。 也就是說，他們假設轉換必須發生在活動內容顯示的相同瀏覽中，以便將轉換「歸因」至ML模型所做的決策。 這是 [!DNL Target] 保證模式的及時培訓； [!DNL Target] 轉換最多等候30天（中報表的預設歸因視窗） [!DNL Adobe Analytics])，再加入其模型的訓練資料中。

因此， [!DNL Target] 模型（在訓練期間）與查詢資料時（在產生報表期間）所使用的預設歸因，可能會導致差異。 事實上，歸因問題所在， ML模型的效能甚至可能看起來很差。

>[!TIP]
>
>如果ML模型針對與您在報表中檢視的量度不同而歸因的量度進行最佳化，則模型可能無法如預期般執行！ 為避免此情況，請確定報表上的目標量度使用與Target ML模型所使用相同的量度定義和歸因。

確切的量度定義和歸因設定取決於 [優化准則](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported) 在活動建立期間指定。

### 定位定義的轉換，或使用 *將每次造訪的量度值最大化*

當量度為Target轉換，或Analytics量度具有 **將每次造訪的量度值最大化**，目標量度定義可讓多個轉換事件在同一次造訪中發生。
若要檢視與Adobe Target ML模型所使用歸因方法相同的目標量度，請遵循下列步驟：

![gearicon.png](assets/gearicon.png)

1. 從產生的功能表，捲動至 **[!UICONTROL 資料設定]**.
1. 選擇 **[!UICONTROL 使用非預設歸因模型]** （如果尚未選取）:

![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1. 按一下&#x200B;**[!UICONTROL 編輯]**。
1. 選擇 **[!UICONTROL 模型]**: **[!UICONTROL 參與率]**，和 **[!UICONTROL 回顧期間]**: **[!UICONTROL 瀏覽]**.

![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)

1. 按一下&#x200B;**[!UICONTROL 「套用」]**。

這些步驟可確保如果目標量度事件發生，您的報表會將目標量度歸因於體驗的顯示 *任何時間* （「參與率」）。

### Analytics量度搭配 *不重複造訪轉換率*

**以正量度區段定義造訪**

在您選取的案例中 *最大化獨特造訪轉換率* 作為最佳化條件，則轉換率的正確定義是度量值為正的造訪次數的百分比。 這可透過建立區段來達成，依量度的正值向下篩選至造訪，然後篩選造訪量度。


1. 和之前一樣，選取 **[!UICONTROL 元件>建立區段]** 選項。
2. 輸入 **[!UICONTROL 標題]** 的URL區段。 在下列範例中，區段的名稱為 [!DNL "Visits with an order"].
3. 將您在最佳化目標中使用的基礎量度拖曳至區段。 在下列範例中，我們會使用 **訂購** 量度，因此轉換率會測量記錄訂單的造訪比例。
4. 在區段定義容器的左上角，選取 **[!UICONTROL 包括]** **瀏覽**.
5. 使用 **[!UICONTROL 大於]** 運算元，並將值設為0（亦即，此區段包含訂購量度為正的造訪）
6. 按一下&#x200B;**[!UICONTROL 儲存]**。

![圖7.png](assets/Figure7.png)
*圖7:以正序篩選瀏覽的區段定義。 根據活動的最佳化量度，您必須以適當的量度取代訂單*

**將此項目套用至活動篩選量度中的造訪**

此區段現在可用來篩選具有正數訂購的造訪，以及 [!DNL Auto-Target]活動。 篩選量度的程式與之前類似，而將新區段套用至已篩選的造訪量度後，報表面板看起來應該類似圖8

![圖8.png](assets/Figure8.png)
*圖8:具有正確獨特造訪轉換量度的報表面板 — 亦即記錄來自活動點擊的造訪次數，以及轉換量度（此範例中的訂購）非零的造訪次數。*


## 最後一步：建立擷取上述神奇效果的轉換率

修改 [!UICONTROL 瀏覽] 和前幾節的目標量度，以及您應針對 [!UICONTROL 自動鎖定目標] 「報表面板」是建立正確的轉換率，也就是具有正確歸因之目標量度與適當篩選之 [!UICONTROL 瀏覽] 量度。

請使用下列步驟建立計算量度來執行此操作：

1. 選取 **[!UICONTROL 元件>建立量度]** 選項 [!DNL Workspace] 工具欄。
1. 輸入 **[!UICONTROL 標題]** ，以取得量度。 例如，「活動XXX的瀏覽更正轉換率」。
1. 選擇 **[!UICONTROL 格式]** =百分比和 **[!UICONTROL 小數位數]** = 2。
1. 拖曳活動的相關目標量度(例如 [!UICONTROL 活動轉換])，並使用此目標量度上的齒輪圖示，將歸因模型調整為（參與率|造訪），如先前所述。
1. 選擇 **[!UICONTROL 新增>容器]** 從 **[!UICONTROL 定義]** 區段。
1. 選取兩個容器之間的除法(÷)運算子。
1. 拖曳先前建立的區段 — 名為「特定點擊」 [!UICONTROL 自動鎖定目標] 本教學課程中的「活動」，針對此特定 [!DNL Auto-Target] 活動。
1. 拖曳 **[!UICONTROL 瀏覽]** 量度放入區段容器中。
1. 按一下&#x200B;**[!UICONTROL 儲存]**。

>[!TIP]
>
> 您也可以使用 [快速計算量度功能](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en).

完整的計算量度定義會顯示在此處。

![圖9.png](assets/Figure9.png)
*圖9:修正造訪和歸因的模型轉換率量度定義。 (請注意，此量度取決於您的目標量度和活動。 換句話說，此量度定義無法在各活動間重複使用。)*

>[!IMPORTANT]
>
>A4T面板中的轉換率量度沒有連結至表格中的轉換事件或標準化量度。 當您進行本教學課程中建議的修改時，轉換率不會自動適應變更。 因此，如果您對轉換事件歸因和標準化量度中的一個（或兩者）進行修改，則您必須記住，最後一步也要修改轉換率，如上所示。

## 摘要：最終範例 [!DNL Workspace] 面板 [!UICONTROL 自動鎖定目標] 報告

將上述所有步驟合併成單一面板，下圖將顯示建議報表的完整檢視 [!UICONTROL 自動鎖定目標] A4T活動。 此報表與 [!DNL Target] ML模型來最佳化您的目標量度，並納入本教學課程中討論的所有細微差別和建議。 此報告也最接近傳統計算方法 [!DNL Target] — 報告驅動 [!UICONTROL 自動鎖定目標] 活動。

![圖10.png](assets/Figure10.png)
*圖10:最終的A4T [!UICONTROL 自動鎖定目標] 報告 [!DNL Adobe Analytics] [!DNL Workspace]，結合本檔案前幾節中所述對量度定義的所有調整。*
