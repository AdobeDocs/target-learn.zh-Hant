---
title: 如何在 [!DNL Analysis Workspace] for [!UICONTROL 自動分配] 活動
description: 如何在 [!DNL Analysis Workspace] 在運行時獲取預期結果 [!UICONTROL 自動分配] 活動。
role: User
badgeBeta: label="Beta" type="Informative" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#beta newtab=true" tooltip="What are Target Beta release features?"
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: b29362ea45196d09dcbfbceeaaed5bc20467ea16
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# 在中設定A4T報表 [!DNL Analysis Workspace] for [!DNL Auto-Allocate] 活動

安 [!DNL Auto-Allocate] 活動會從兩個或多個體驗中識別獲勝者，並在測試繼續執行和學習時自動重新分配更多流量給獲勝者。 此 [!UICONTROL Analytics for Target] (A4T)整合 [!UICONTROL 自動分配] 可讓您在 [!DNL Adobe Analytics]，您甚至可以最佳化中定義的自訂事件或量度 [!DNL Analytics].

雖然 [!DNL Adobe Analytics] [!DNL Analysis Workspace]，對預設值進行一些修改 **[!UICONTROL Analytics for Target]** 需要面板才能正確解譯 [!DNL Auto-Allocate] 活動，由於 [最佳化准則](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

本教學課程將逐步說明分析時的建議修改 [!DNL Auto-Allocate] 活動 [!DNL Analysis Workspace]. 主要概念包括：

* [!UICONTROL 訪客] 應一律作為 [!DNL Auto-Allocate] 活動。
* 當量度為 [!DNL Adobe Analytics] 量度，轉換率的適當分子取決於活動設定期間選擇的最佳化條件類型。
   * 「最大化獨特訪客轉換率」最佳化標準的轉換率，其分子是具有量度正值的獨特訪客計數。
   * 「每位訪客最大化量度值」的轉換率，其分子為 [!DNL Adobe Analytics]. 預設會提供於 **[!UICONTROL Analytics for Target]** 面板 [!DNL Analysis Workspace].
* 當最佳化量度為 [!DNL Target] 定義的轉換量度，預設 **[!UICONTROL Analytics for Target]** 面板 [!DNL Analysis Workspace] 控制代碼。
* 全部 [!UICONTROL 自動分配] 在 [!DNL Target Standard/Premium] 23.3.1版（2023年3月30日） [!DNL Analytics Workspace] 和 [!DNL Target] 顯示 [!UICONTROL 信賴度].

   全部 [!UICONTROL 自動分配] 2023年3月30日之後建立的活動，信賴區間值會顯示在 [!DNL Analysis Workspace] 不會反映 [更保守的統計 [!UICONTROL 自動分配]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} 如果這些活動 *both* 下列條件之中：

   * [!DNL Analytics] 作為報表來源(A4T)
   * [!DNL Analytics] 最佳化量度

   若 *both* 其中，應從A4T面板中移除信賴度量。 請改為在 [!DNL Target] 報告。

## 為建立A4T [!DNL Auto-Allocate] 面板 [!DNL Analysis Workspace]

為建立A4T [!DNL Auto-Allocate] 報表從 **[!UICONTROL Analytics for Target]** 面板 [!DNL Analysis Workspace]，如下所示。 然後進行下列選取：

1. **[!UICONTROL 控制體驗]**:您可以選擇任何體驗。
2. **[!UICONTROL 標準化量度]**:選取訪客。 [!DNL Auto-Allocate] 一律會依不重複訪客將轉換率標準化。
3. **[!UICONTROL 成功量度]**:選取您在活動建立期間使用的相同量度。 如果這是 [!DNL Target] 定義的轉換量度，請選取 **活動轉換**. 否則，請選取 [!DNL Adobe Analytics] 量度。

![[!UICONTROL Analytics for Target] 面板設定 [!DNL Auto-Allocate] 活動。](assets/AAFigure1.png)

*圖1: [!UICONTROL Analytics for Target] 面板設定 [!DNL Auto-Allocate] 活動。*

>[!NOTE]
>
> 您也可以取得預先建立的 **[!UICONTROL Analytics for Target]** 中的 [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL 轉換] 量度或 [!DNL Analytics] 具有「每位訪客最大化量度值」最佳化條件的量度

預設的A4T面板控點 [!DNL Auto-Allocate] 目標量度為 [!DNL Target] 轉換或 [!DNL Analytics] 量度，其最佳化標準為「將每位訪客的量度值最大化」。

此面板的一個範例顯示於 [!UICONTROL 收入] 量度中，選取「每位訪客最大化量度值」作為活動建立時的最佳化條件。 如前所述， [!DNL Auto-Allocate] 使用比中所用更保守的信賴計算 **[!UICONTROL Analytics for Target]** 中。 Adobe建議您從A4T面板中移除信賴度量，以及相關的上下提升度量。 請改為在 [!DNL Target] 報告。

![[!UICONTROL 目標分析 — 自動分配報表] 面板](assets/AAFigure2.png)

*圖2:建議的 [!DNL Auto-Allocate] 活動 [!DNL Analytics] 量度「將每個訪客的量度值最大化」條件。 針對這些類型的量度，以及 [!DNL Target] 定義的轉換量度，預設&#x200B;**[!UICONTROL Analytics for Target]**面板 [!DNL Analysis Workspace] 可供使用。*

## [!DNL Analytics] 具有「最大化獨特訪客轉換率」最佳化條件的量度

當 [!DNL Adobe Analytics] 量度與 *最大化獨特訪客轉換率*，預設值 **[!UICONTROL Analytics for Target]** 面板 [!DNL Analysis Workspace] 必須修改。

成功量度現在是轉換量度為正的不重複訪客計數。 您可以建立群體來篩選具有量度正值的點擊，借此達成此目的。 建立此區段的方式如下：

1. 選取 **[!UICONTROL 元件]** > **[!UICONTROL 建立區段]** 選項 [!DNL Analysis Workspace] 工具欄。
1. 從左側面板拖曳活動建立時使用的量度至 **[!UICONTROL 定義]** 框。
1. 選取以下量度的值： **大於** 0的數值。
1. 從 **[!UICONTROL 包括]** 下拉式清單，選取 **[!UICONTROL 訪客]**.
1. 為您的區段指定適當的名稱。

區段建立的範例如下圖所示，您可在此選取 [!UICONTROL 收入為正的訪客].

![[!UICONTROL 收入為正的訪客] 區段 [!DNL Analysis Workspace]](assets/AAFigure3.png)

*圖3:區段建立 [!DNL Adobe Analytics] 最佳化條件等於「[!UICONTROL 最大化獨特訪客轉換率].&quot; 在此範例中，量度為 [!UICONTROL 收入]，而最佳化目標是以正收入將訪客數量最大化。*

建立適當的區段後，預設  **[!UICONTROL Analytics for Target]** 面板 [!DNL Analysis Workspace] 可以修改。

1. 新增秒數 **不重複訪客** 量度與現有 [!UICONTROL 訪客] 量度欄。
2. 將新建立的段拖動到第一列下，以生成類似圖4的面板。 請注意差異：收入為正的獨特訪客數量，是指派給每個體驗之獨特訪客總數的一小部分。

   ![圖4.png](assets/AAFigure4.png)

   *圖4:篩選 [!UICONTROL 不重複訪客] 依新建立的區段*

3. 轉換率可以是 [快速計算](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) 加亮第一欄和第二欄，按一下右鍵，選擇 **[!UICONTROL 從選取範圍建立量度]** > **[!UICONTROL 除]**.

   預設轉換率應移除，並取代為這個新計算量度，如下圖所示。 您可能需要編輯新建立的計算量度，才會顯示為 **[!UICONTROL 格式]** > **[!UICONTROL 百分比]** 最多兩位小數，如所示。

   ![圖5.png](assets/AAFigure5.png)

   *圖5:最後 [!UICONTROL 自動分配] 顯示二進位收入轉換量度的轉換率的面板*

## 摘要

本教學課程中的步驟示範如何正確設定 [!DNL Analysis Workspace] 顯示 [!UICONTROL 自動分配] 報告資料。

總而言之:

* 當量度為 [!DNL Target] 定義的轉換量度或 [!DNL Adobe Analytics] 量度搭配最佳化標準「每位訪客最大化量度值」時，應使用以訪客為標準化量度的預設工作區面板。
* 當量度為 [!DNL Adobe Analytics] 量度搭配最佳化標準「最大化獨特訪客轉換率」，您必須使用轉換率，此轉換率定義為量度為正的訪客比例。 若要這麼做，請建立對應的區段來篩選 [!UICONTROL 不重複訪客] 量度。
