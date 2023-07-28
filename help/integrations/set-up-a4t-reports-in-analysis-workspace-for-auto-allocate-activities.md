---
title: 如何在中設定A4T報表 [!DNL Analysis Workspace] 的 [!UICONTROL 自動分配] 活動
description: 如何在中設定A4T報表 [!DNL Analysis Workspace] 以取得執行時的預期結果 [!UICONTROL 自動分配] 活動。
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 8ef61ac0abf008039561bebe7d8d20b84f447487
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---

# 在中設定A4T報表 [!DNL Analysis Workspace] 的 [!DNL Auto-Allocate] 活動

一個 [!DNL Auto-Allocate] 活動會從兩個或多個體驗中識別獲勝者，並自動重新分配您的流量給獲勝者，同時測試會繼續執行和學習。 此 [!UICONTROL 目標分析] (A4T)整合 [!UICONTROL 自動分配] 可讓您在中檢視您的報告資料 [!DNL Adobe Analytics]，您甚至可以針對中定義的自訂事件或量度進行最佳化 [!DNL Analytics].

雖然提供豐富的分析功能，但 [!DNL Adobe Analytics] [!DNL Analysis Workspace]，對預設值進行了一些修改 **[!UICONTROL 目標分析]** 可能需要面板才能正確解譯 [!DNL Auto-Allocate] 活動，由於中的細微差別 [最佳化量度條件](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

本教學課程會逐步引導您瞭解建議的修改方式，以便分析 [!DNL Auto-Allocate] 中的活動 [!DNL Analysis Workspace]. 主要概念為：

* [!UICONTROL 訪客] 應一律用作中的標準化量度 [!DNL Auto-Allocate] 活動。
* 當量度為 [!DNL Adobe Analytics] 量度，轉換率的計算會因活動設定期間定義的最佳化條件型別而異。
   * 「最大化每位訪客的量度值」轉換率：分子是中的一般量度值 [!DNL Adobe Analytics] (這預設由 [!UICONTROL 目標分析] 中的面板 [!DNL Analysis Workspace])。
      * 換句話說：將每位訪客的轉換次數最大化（「每位訪客各計數」）。
      * 此方法不需要額外的區段來比對 [!DNL Target] UI。
   * 「最大化不重複訪客轉換率」轉換率：分子是以量度為正值的獨特訪客計數。
      * 其含義是：將轉換的訪客數量最大化（「每位訪客計數一次）。
      * 此方法 *DO* 需要在報告中建立額外的區段，以符合 [!DNL Target] UI。

* 當您的最佳化量度為 [!DNL Target] 定義的轉換量度，預設值 **[!UICONTROL 目標分析]** 中的面板 [!DNL Analysis Workspace] 處理面板的設定。
* 全部 [!UICONTROL 自動分配] 在以下日期之前建立的活動： [!DNL Target Standard/Premium] 23.3.1版（2023年3月30日） [!DNL Analytics Workspace] 和 [!DNL Target] 顯示相同的值 [!UICONTROL 信賴度].

  全部 [!UICONTROL 自動分配] 在2023年3月30日之後建立的活動，在中看到的信賴區間值 [!DNL Analysis Workspace] 不要反映 [使用較為保守的統計資料 [!UICONTROL 自動分配]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} 在，如果這些活動具有 *兩者* 下列條件之一：

   * [!DNL Analytics] 做為報表來源(A4T)
   * [!DNL Analytics] 最佳化量度

  可信度量度應從A4T面板中移除。 請改為參考下列值： [!DNL Target] 報告。

## 建立A4T用於 [!DNL Auto-Allocate] 中的面板 [!DNL Analysis Workspace]

若要為建立A4T面板 [!DNL Auto-Allocate] 報告開始於 **[!UICONTROL 目標分析]** 中的面板 [!DNL Analysis Workspace]，如下所示。 然後進行下列選取：

1. **[!UICONTROL 控制體驗]**：您可以選擇任何體驗。
1. **[!UICONTROL 標準化量度]**：選取訪客（預設情況下，訪客包含在A4T面板中）。 [!DNL Auto-Allocate] 一律會根據不重複訪客將轉換率標準化。
1. **[!UICONTROL 成功量度]**：選取您在活動建立期間使用的相同量度。 如果這是 [!DNL Target] 定義的轉換量度，選取 **活動轉換**. 否則，請選取 [!DNL Adobe Analytics] 您使用的量度。

![[!UICONTROL 目標分析] 面板設定 [!DNL Auto-Allocate] 活動。](assets/AAFigure1.png)

*圖1： [!UICONTROL 目標分析] 面板設定 [!DNL Auto-Allocate] 活動。*

您也可以取得預先建立的 **[!UICONTROL 目標分析]** 面板（如果您按一下中報表畫面的連結） [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL 轉換] 量度或 [!DNL Analytics] 具有「每位訪客量度值最大化」最佳化條件的量度

當目標量度為下列其中一項：

* 目標轉換量度
* 最佳化條件為「每位訪客量度值最大化」的Analytics量度

預設的A4T面板會自動設定報表。

此面板的一個範例顯示於 [!UICONTROL 收入] 量度，其中「每位訪客的量度值最大化」在活動建立時選取為最佳化條件。 如前所述， [!DNL Auto-Allocate] 使用的信賴度計算比中使用的更保守 **[!UICONTROL 目標分析]** 面板。 Adobe建議您從A4T面板中移除可信度量度，以及相關的下限和上限提升量度。 請改為參考中的信賴值 [!DNL Target] 報告。

>[!NOTE]
>
>A4T報表中的信賴值較不保守 [!DNL Target] 報告，並可能提前指出贏家 [!UICONTROL 自動分配] 活動。


![[!UICONTROL Analytics for Target — 自動分配報表] 面板](assets/AAFigure2.png)

*圖2：的建議報表 [!DNL Auto-Allocate] 具有的活動 [!DNL Analytics] 量度「將每位訪客的量度值最佳化最大化」條件。 對於這些型別的量度，以及 [!DNL Target] 定義的轉換量度，預設值&#x200B;**[!UICONTROL 目標分析]**中的面板 [!DNL Analysis Workspace] 可使用。*

## [!DNL Analytics] 具有「最大化不重複訪客轉換率」最佳化條件的量度

最佳化標準「最大化不重複訪客轉換率」指的是量度值為正數的訪客計數。 例如，如果轉換率定義為收入，則「最大化不重複訪客轉換率」標準將會針對收入大於0的不重複訪客計數進行最佳化。 換言之，此標準將最大化產生收入的訪客計數，而不是收入本身的值。

>[!NOTE]
>
>這裡所參照的轉換率可指訂單以外的動作，例如點按數、曝光數等。 在這些情況下，標準仍將是分別點按或檢視頁面的訪客計數最大化。

此 [!DNL Analytics for Target] 中的面板 [!DNL Analysis Workspace] 如果將此最佳化准則與 [!DNL Adobe Analytics] 量度。

使用此最佳化標準時，成功量度是轉換量度為正的不重複訪客的計數。 因此，若要檢視此值，必須建立新區段，以篩選量度具有正值的點選。

建立此區段如下：

1. 選取 **[!UICONTROL 元件]** > **[!UICONTROL 建立區段]** 中的選項 [!DNL Analysis Workspace] 工具列。
1. 將活動建立時所使用的量度從左側面板拖曳至 **[!UICONTROL 定義]** 方塊中。
1. 選取以下量度的值： **大於** 0的數值。
1. 從 **[!UICONTROL 包含]** 下拉式清單，選取 **[!UICONTROL 訪客]**.
1. 為區段提供適當的名稱。

區段的建立範例如下圖所示，其中成功量度為 [!UICONTROL 有正面收入的訪客].

![[!UICONTROL 有正面收入的訪客] 中的區段 [!DNL Analysis Workspace]](assets/AAFigure3.png)

*圖3：建立區段 [!DNL Adobe Analytics] 最佳化條件等於&quot;[!UICONTROL 最大化的不重複訪客轉換率].」 在此範例中，量度為 [!UICONTROL 收入]，而最佳化目標是最大化具有正收入的訪客數量。*

建立適當的區段後，您可以修改預設值  **[!UICONTROL 目標分析]** 中的面板 [!DNL Analysis Workspace] 以檢視最佳化准則值。 可透過下列方式達成：

1. 新增秒 **不重複訪客** 量度與現有 [!UICONTROL 訪客] 量度欄。
2. 將新建立的區段拖曳到第一欄下，以產生類似圖4的面板。 請注意欄值的差異：收入為正的不重複訪客數應為指派給每個體驗的不重複訪客總數的一小部分（如下所示）。

   ![圖4.png](assets/AAFigure4.png)

   *圖4：篩選 [!UICONTROL 不重複訪客] 依新建立的區段*

3. 轉換率可以是 [快速計算](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) 反白第一欄和第二欄，按一下滑鼠右鍵，選取 **[!UICONTROL 從選取專案建立量度]** > **[!UICONTROL 除]**.

   應移除預設轉換率，並取代為此新計算量度，如下圖所示。 您可能需要編輯新建立的計算量度，以顯示為 **[!UICONTROL 格式]** > **[!UICONTROL 百分比]** 最多小數點兩位數，如圖所示。

   ![圖5.png](assets/AAFigure5.png)

   *圖5：決賽 [!UICONTROL 自動分配] 顯示二進位收入轉換量度轉換率的面板*

## 摘要

本教學課程中的步驟示範如何正確設定 [!DNL Analysis Workspace] 以顯示 [!UICONTROL 自動分配] 報表資料。

總而言之:

* 當量度為 [!DNL Target] 定義的轉換量度或 [!DNL Adobe Analytics] 應使用最佳化條件為「每位訪客量度值最大化」的量度，此為預設工作區面板，且已設定為將訪客設為標準化量度。
* 當量度為 [!DNL Adobe Analytics] 使用最佳化准則「最大化不重複訪客轉換率」的量度，您必須判斷具有正量度值的訪客相對於訪客總數的比例。 若要這麼做，請建立對應的區段來篩選 [!UICONTROL 不重複訪客] 在該量度上。
