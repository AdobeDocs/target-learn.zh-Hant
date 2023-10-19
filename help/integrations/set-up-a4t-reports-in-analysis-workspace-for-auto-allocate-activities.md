---
title: 如何在中設定A4T報表 [!DNL Analysis Workspace] 的 [!UICONTROL 自動分配] 活動
description: 如何設定 [!UICONTROL 目標分析] 中的(A4T)報表 [!DNL Adobe] [!DNL Analysis Workspace] 執行時 [!UICONTROL 自動分配] 活動。
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 352f334e2ca8c1d0be3ff0f89482b97500685174
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 0%

---

# 在中設定A4T報表 [!DNL Analysis Workspace] 的 [!DNL Auto-Allocate] 活動

一個 [!UICONTROL 自動分配] 中的活動 [!DNL Adobe Target] 會從兩個或多個體驗中識別獲勝者，並自動重新分配訪客流量給獲勝者，同時測試會繼續執行和學習。 此 [!UICONTROL 目標分析] (A4T)整合 [!UICONTROL 自動分配] 可讓您在中檢視報表資料 [!DNL Adobe Analytics]，您也可以針對中定義的自訂事件或量度最佳化 [!DNL Analytics].

雖然提供豐富的分析功能，但 [!DNL Adobe Analytics] [!DNL Analysis Workspace]，對預設值進行了一些修改 [!UICONTROL 目標分析] 可能需要面板才能正確解譯 [!UICONTROL 自動分配] 活動。 由於中的細微差別，需要進行這些修改 [最佳化量度條件](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

每種最佳化量度型別在A4T中都需要不同的報表設定，如下所示：

* 使用 [!DNL Analytics] 量度

   * [!UICONTROL 最大化的每位訪客量度值]
   * [!UICONTROL 最大化的不重複訪客轉換率]

* 使用 [!DNL Target] — 定義的轉換量度

本教學課程涵蓋整體A4T指引，以及條件特定的報表設定步驟。

## 包含「」的Analytics量度[!UICONTROL 最大化的每位訪客量度值]&quot;最佳化條件

**定義**：（整體量度值） / （訪客數）

若要設定報表，請在A4T報表中進行下列變更：

| 所需變更 | [!DNL Target]-triggered report — 觸發的報告 | A4T面板報表 |
| --- | --- | --- |
| 將的量度值最大化 [!DNL Analytics] 量度 | <ul><li>[!UICONTROL 信賴度] 量度應移除。</li><li>[!UICONTROL 提升度（低）] 和 [!UICONTROL 提升度（高）] 應該已移除。</li><li>取消核取百分比簡報 [!UICONTROL 轉換率] 欄，以避免混淆。 另請參閱 [整體指引](#guidance) 底下。</li><li>轉換率量度應重新命名為「量度/訪客」。</li></ul> | <ul><li>[!UICONTROL 信賴度] 量度應移除。</li><li>[!UICONTROL 提升度（低）] 和 [!UICONTROL 提升度（高）] 應該已移除。</li><li>取消核取百分比簡報 [!UICONTROL 轉換率] 欄，以避免混淆。 另請參閱 [整體指引](#guidance) 底下。</li><li>轉換率量度應重新命名為「量度/訪客」。</li><li>確保日期和時間範圍與您在欄位中看到的值一致 [!DNL Target] 報告。 另請參閱 [整體指引](#guidance) 底下。</li></ul> |

![最大化的收入量度值](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] 具有「」的量度[!UICONTROL 不重複訪客轉換率]&quot;最佳化條件

**定義**：（「不重複訪客」數量與量度值為正數） / （不重複訪客總數）

範例：假設您的最佳化量度為 [!UICONTROL 收入]. 活動中有五個不重複訪客，其中三個不重複訪客已購買。 在此範例中，此值= (3位訪客，其 [!UICONTROL 收入] 為正數) / （不重複訪客總數5個） = 0.6 = 60%。

>[!NOTE]
>
>這裡所參照的轉換率可指訂單以外的動作，例如點按數、曝光數等。 在這些情況下，標準仍將是分別點按或檢視頁面的訪客計數最大化。

若要設定報表，請在A4T報表中進行下列變更：

| 所需變更 | 目標觸發的報告 | A4T面板報表 |
| --- | --- | --- |
| 將的轉換最大化 [!DNL Analytics] 量度 | <ul><li>[!UICONTROL 信賴度] 量度應移除。</li><li>全部 [!UICONTROL 提升度] 量度應移除。</li><li>取消核取百分比簡報 [!UICONTROL 轉換率] 欄，以避免混淆。 另請參閱 [整體指引](#guidance) 底下。</li></ul> | <ul><li>[!UICONTROL 信賴度] 量度應移除。</li><li>全部 [!UICONTROL 提升度] 量度應移除。</li><li>建立區段來篩選具有正量度值的訪客，這些訪客檢視分析的活動。 另請參閱 [建立區段](#segment) 底下。</li><li>取代自動填入的 [!UICONTROL 轉換率] 量度，因此是 [!UICONTROL 不重複訪客] 具有正的量度值和不重複訪客。 另請參閱 [更新轉換率量度](#update-conversion-metric) 底下。</li><li>取消核取百分比簡報 [!UICONTROL 轉換率] 欄，以避免混淆。 另請參閱 [整體指引](#guidance) 底下。</li><li>確保日期和時間範圍與您在欄位中看到的值一致 [!DNL Target] 報告。 另請參閱 [整體指引](#guidance) 底下。</li></ul> |

### 預設A4T面板報告 — 其他指南

以下幾節包含當您設定預設A4T面板報告時，有關其他指引的詳細資訊。

#### 建立區段 {#segment}

1. 按一下 **「+」符號** 旁邊 **[!UICONTROL 區段]** 在左側邊欄中。

   ![左側邊欄中區段旁的加號。](/help/integrations/assets/plus-sign.png)

1. 將區段命名為「具有正量度值的訪客」。
1. 在 **[!UICONTROL 定義]**，旁邊 **[!UICONTROL 包含]**，選取 **[!UICONTROL 訪客]**.
1. 在 **[!UICONTROL 定義]**&#x200B;中，選取活動中的最佳化量度。

   在此範例中，假設 [!UICONTROL 收入] 作為最佳化量度。

1. 選擇&quot;[!UICONTROL 大於]&quot;運運算元，然後指定&quot;0&quot;。

   這些設定會篩選具有正量度值的所有訪客。

1. 按一下&#x200B;**[!UICONTROL 儲存]**。

   ![正量度值](/help/integrations/assets/positive-metric-value.png)

1. 將新建立的區段「具有正量度值的訪客」新增到A4T面板。
1. 拖放 [!UICONTROL 不重複訪客] 與「具有正量度值的訪客」位於相同欄中的量度。

   此設定會針對量度值為正數的所有不重複訪客建立區段。 在此範例中，其收入大於零的所有不重複訪客。

#### 更新 [!UICONTROL 轉換率] 量度 {#update-conversion-metric}

1. 如果您尚未這樣做，請移除現有的 [!UICONTROL 轉換率] 欄，如下所述。
1. 按一下「+」旁的「+」號以新增量度 **[!UICONTROL 量度]** 區段。
1. 將量度命名為「轉換率」並定義為「(」[!UICONTROL 不重複訪客] 正量度值)」除以「不重複訪客」，如下所示。

   新增「具有正量度值的訪客」、除數運運算元、分子中的「不重複訪客」量度以及「不重複訪客」的新建立區段（定義於下方的步驟）作為分母。

   ![A4T面板中的轉換率。](/help/integrations/assets/conversion-rate.png)

1. 按一下&#x200B;**[!UICONTROL 儲存]**。

1. 將您新建立的「轉換率」量度拖放至現有面板。
1. 按一下齒輪圖示，然後取消選取 **[!UICONTROL 百分比]** 核取方塊，因為此值可能會導致混淆。

   正確設定報告應該會產生類似下列圖例的結果：

   ![A4T面板報表中的不重複造訪轉換率](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## [!DNL Target] — 定義的轉換率

若要設定報表，請在A4T報表中進行下列變更：

| 所需變更 | 目標觸發的報告 | A4T面板報表 |
| --- | --- | --- |
| [!DNL Analytics] 報告工具 [!DNL Target] 轉換量度 | <ul><li>[!UICONTROL 信賴度] 量度應移除。</li><li>[!UICONTROL 提升度（低）] 和 [!UICONTROL 提升度（高）] 應該已移除。</li><li>取消核取百分比簡報 [!UICONTROL 轉換率] 欄，以避免混淆。 另請參閱 [整體指引](#guidance) 底下。</li></ul> | <ul><li>[!UICONTROL 信賴度] 量度應移除。</li><li>[!UICONTROL 提升度（低）] 和 [!UICONTROL 提升度（高）] 應該已移除。</li><li>取消核取百分比簡報 [!UICONTROL 轉換率] 欄，以避免混淆。 另請參閱 [整體指引](#guidance) 底下。</li><li>確保日期和時間範圍與您在欄位中看到的值一致 [!DNL Target] 報告。 另請參閱 [整體指引](#guidance) 底下。</li></ul> |

正確設定報告應該會產生類似下列圖例的結果：

![活動轉換](/help/integrations/assets/optimized-table.png)

## 整體指引 [!UICONTROL 目標分析] (A4T) {#guidance}

您可以導覽至預先建立的 [!UICONTROL 目標分析] 按一下中報表畫面的連結，即可使用此面板 [!UICONTROL Adobe Target] (本指南稍後將這稱為&quot;[!DNL Target]-triggered report」)。 或者，您也可以在中建置A4T面板 [!DNL Analytics] （本節稍後將詳述）。

以下各節會根據您選擇的這些方法，指定所需的組態。 不過，下列步驟可作為整體指引：

* 無論面板建立方法為何（兩者皆將於下文詳細說明），都應從A4T面板移除信賴度量度。 請改為參考下列值： [!DNL Target] 報告。 此外，活動的獲勝者可識別 [!DNL Target] 報告。 有關活動獲勝者識別的詳細資訊，請參閱 [識別活動獲勝者](#winner) 一節。
>>
* 為避免混淆，請取消核取「[!UICONTROL 百分比]」簡報 [!UICONTROL 轉換率] 量度。 另請參閱 [隱藏百分比，從 [!UICONTROL 轉換率] 欄](#hide-percentage) 底下。
>>
* 如果您建置A4T面板，請確定日期和時間範圍符合您的 [!DNL Target] 報告。 另請參閱 [在A4T面板中對齊日期和時間](#aligning-date-and-time) 底下。

### 隱藏百分比，從 [!UICONTROL 轉換率] 欄 {#hide-percentage}

1. 按一下 **齒輪** 圖示加以存取（在標題旁） [!UICONTROL 轉換率] 欄。

   ![轉換率欄中的齒輪圖示](/help/integrations/assets/coversion-rate-gear-icon.png)

   此 [!UICONTROL 欄] 設定對話方塊顯示：

   ![欄設定對話方塊](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. 取消選取 **[!UICONTROL 百分比]** 核取方塊。

   您的A4T面板現在不包含百分比作為轉換率和相符項 [!DNL Target]，如下所示：

   ![顯示無百分比的「轉換率」欄](/help/integrations/assets/no-percentages.png)

### 在A4T面板中對齊日期和時間 {#aligning-date-and-time}

1. 在每個面板下方，檢查面板參考的日期範圍，確保日期範圍符合 [!DNL Target] 報告。

   ![A4T面板中的日期範圍](/help/integrations/assets/date-range.png)

1. 在 [!DNL Analytics]，將時間範圍設為上午12:00至晚上11:59。

### 識別活動獲勝者 {#winner}

[!DNL Auto-Allocate] 當成功轉換率的信賴值大於或等於95%時，就會選取活動獲勝者。 這些值應在以下連結中參照： [!DNL Target] 報表，因為可信度計算反映較保守的方法 [!DNL Target] 建議用於 [!UICONTROL 自動分配] 活動。 另請參閱 [自動分配的統計保證](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} 在 *[!UICONTROL Adobe Target商業從業者指南]*.

>[!NOTE]
>
「尚未有贏家」和「贏家」徽章在的A4T面板中無法使用 [!DNL Analysis Workspace]. 此外，獲勝者「星星」徽章會顯示在 [!DNL Target] 報表 [!UICONTROL 自動分配] 活動應被忽略。 另請參閱 [自動分配](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank} 在 *自動分配和自動鎖定目標活動的A4T支援* 在 *[!UICONTROL Adobe Target商業從業者指南]*.

### 建立A4T用於 [!UICONTROL 自動分配] 中的面板 [!DNL Analysis Workspace]

1. 若要為建立A4T面板 [!UICONTROL 自動分配] 活動報表，從 [!UICONTROL 目標分析] 中的面板 [!DNL Analysis Workspace]，如下所示。

   ![Analytics for Target — 自動分配報表](/help/integrations/assets/a4t-auto-allocate-report.png)

1. 進行下列選取：

   * **[!UICONTROL 控制體驗]**：選擇任何體驗。
   * **[!UICONTROL 標準化量度]**：選取 **[!UICONTROL 訪客]** （預設包含在A4T面板中）。 [!UICONTROL 自動分配] 一律會根據不重複訪客將轉換率標準化。
   * **成功量度**：選取您在活動建立期間使用的相同（最佳化）量度。 如果這是 [!DNL Target]-defined conversion metric，選取 **[!UICONTROL 活動轉換]**. 否則，請選取 [!DNL Adobe Analytics] 您使用的量度。









