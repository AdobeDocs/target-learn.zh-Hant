---
title: 如何在 [!DNL Analysis Workspace] 中為[!UICONTROL 自動分配]活動設定A4T報告
description: 執行[!UICONTROL 自動分配]活動時，如何在 [!DNL Adobe] [!DNL Analysis Workspace]中設定[!UICONTROL Analytics for Target] (A4T)報告。
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
TQID: https://experienceleague.adobe.com/5oQMgqqxw2VN-6cb29j4bwEP6VYmGRLXIp5AMJ3WWM4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2:
  - id: df62f171-ac37-440f-8f0f-f41a72ebdd34
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 1546
ht-degree: 0%

---

# 在[!DNL Analysis Workspace]中為[!DNL Auto-Allocate]個活動設定A4T報告

[!DNL Adobe Target]中的[[!UICONTROL 自動分配]活動](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=zh-Hant){target=_blank}會從兩個或多個體驗中識別獲勝者，並在測試持續執行和學習期間，自動重新分配訪客流量給獲勝者。 [!UICONTROL 自動分配]的[!UICONTROL Analytics for Target] (A4T)整合可讓您在[!DNL Adobe Analytics]中檢視報表資料，而且您可以最佳化[!DNL Analytics]中定義的自訂事件或量度。

雖然[!DNL Adobe Analytics] [!DNL Analysis Workspace]中提供了豐富的分析功能，但可能需要對預設[!UICONTROL Analytics for Target]面板進行一些修改，才能正確解譯[!UICONTROL 自動分配]活動。 由於[最佳化量度條件](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=zh-Hant#supported){target=_blank}中的細微差別，所以需要這些修改。

每種最佳化量度型別在A4T中都需要不同的報表設定，如下所示：

* 使用[!DNL Analytics]量度

   * [!UICONTROL 最大化的每位訪客量度值]
   * [!UICONTROL 最大化的不重複訪客轉換率]

* 使用[!DNL Target]定義的轉換量度

本教學課程涵蓋整體A4T指引，以及條件特定的報表設定步驟。

## 具有「每位訪客的量度值最大化」最佳化條件的Analytics量度

**定義**： （整體量度值） / （訪客數）

若要設定報表，請在A4T報表中進行下列變更：

| 所需變更 | [!DNL Target]觸發的報告 | A4T面板報表 |
| --- | --- | --- |
| 將[!DNL Analytics]量度的量度值最大化 | <ul><li>移除[!UICONTROL 信賴度]量度。</li><li>移除[!UICONTROL 提升度（低）]和[!UICONTROL 提升度（高）]。 保留[!UICONTROL 提升度(Med)]。</li><li>取消核取[!UICONTROL 轉換率]資料行的百分比簡報，以避免混淆。 請參閱下列[A4T](#guidance)的整體指引。</li><li>將[!UICONTROL 轉換]比率量度重新命名為「量度/訪客」。</li></ul> | <ul><li>移除[!UICONTROL 信賴度]量度。</li><li>移除[!UICONTROL 提升度（低）]和[!UICONTROL 提升度（高）]保留[!UICONTROL 提升度（中）]。</li><li>取消核取[!UICONTROL 轉換率]資料行的百分比簡報，以避免混淆。 請參閱下列[A4T](#guidance)的整體指引。</li><li>將[!UICONTROL 轉換]比率量度重新命名為「量度/訪客」。</li><li>確保日期和時間範圍符合您在[!DNL Target]報表中看到的值。 請參閱下列[A4T](#guidance)的整體指引。</li></ul> |

![將收入的量度值最大化](/help/integrations/assets/maximize-metric-value-revenue.png)

## 具有「[!UICONTROL 獨特訪客轉換率]」最佳化條件的[!DNL Analytics]個量度

**定義**： （量度值為正值的獨特訪客數） / （獨特訪客總數）

範例：假設您的最佳化量度為[!UICONTROL 收入]。 活動中有五個不重複訪客，其中三個不重複訪客已購買。 在此範例中，此值= （3位訪客的[!UICONTROL 收入]為正數） / （5位不重複訪客總數） = 0.6 = 60%。

>[!NOTE]
>
>這裡所參照的轉換率可指訂單以外的動作，例如點按數、曝光數等。 在這些情況下，標準仍將是分別點按或檢視頁面的訪客計數最大化。

若要設定報表，請在A4T報表中進行下列變更：

| 所需變更 | 目標觸發的報告 | A4T面板報表 |
| --- | --- | --- |
| 最大化[!DNL Analytics]量度的轉換 | <ul><li>移除[!UICONTROL 信賴度]量度。</li><li>移除所有三個[!UICONTROL 提升]量度。</li><li>取消核取[!UICONTROL 轉換率]資料行的百分比簡報，以避免混淆。 請參閱下列[A4T](#guidance)的整體指引。</li></ul> | <ul><li>移除[!UICONTROL 信賴度]量度。</li><li>移除所有三個[!UICONTROL 提升]量度。</li><li>建立區段來篩選具有正量度值的訪客，這些訪客檢視了分析過的活動。 請參閱下方的[建立區段](#segment)。</li><li>取代自動填入的[!UICONTROL 轉換率]量度，以便[!UICONTROL 不重複訪客]之間的除法為正量度值和不重複訪客。 請參閱下方的[更新轉換率量度](#update-conversion-metric)。</li><li>取消核取[!UICONTROL 轉換率]資料行的百分比簡報，以避免混淆。 請參閱下列[A4T](#guidance)的整體指引。</li><li>確保日期和時間範圍符合您在[!DNL Target]報表中看到的值。 請參閱下列[A4T](#guidance)的整體指引。</li></ul> |

### 預設A4T面板報告 — 其他指南

以下幾節包含當您設定預設A4T面板報告時，有關其他指引的詳細資訊。

#### 建立區段 {#segment}

1. 按一下左側邊欄中&#x200B;**[!UICONTROL 區段]**&#x200B;旁的&#x200B;**「+」符號**。

   左側邊欄中的區段旁有![加號。](/help/integrations/assets/plus-sign.png)

1. 將區段命名為「具有正量度值的訪客」。
1. 在&#x200B;**[!UICONTROL 定義]**&#x200B;下，**[!UICONTROL 包含]**&#x200B;旁邊，選取&#x200B;**[!UICONTROL 訪客]**。
1. 在&#x200B;**[!UICONTROL 定義]**&#x200B;下，選取活動中的最佳化量度。

   在此範例中，假設[!UICONTROL 收入]為最佳化量度。

1. 選取「[!UICONTROL 大於]」運運算元，然後指定「0」。

   這些設定會篩選具有正量度值的所有訪客。

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

   ![正的量度值](/help/integrations/assets/positive-metric-value.png)

1. 將新建立的區段「具有正量度值的訪客」新增到A4T面板。
1. 將[!UICONTROL 不重複訪客]量度拖放至與「具有正量度值的訪客」相同的欄。

   此設定會針對量度值為正數的所有不重複訪客建立區段。 在此範例中，其收入大於零的所有不重複訪客。

#### 更新[!UICONTROL 轉換率]量度 {#update-conversion-metric}

1. 如果您尚未這樣做，請從面板中移除現有的[!UICONTROL 轉換率]欄，如下所述。
1. 按一下左側邊欄中&#x200B;**[!UICONTROL 量度]**&#x200B;區段旁的「+」號，以新增量度。
1. 將量度命名為「轉換率」，並將其定義為「（[!UICONTROL 具有正量度值的不重複訪客]）」除以「不重複訪客」，如下所示。

   新增「具有正量度值的訪客」、除數運運算元、分子中的「不重複訪客」量度以及「不重複訪客」的新建立區段（定義於下方的步驟）作為分母。

   A4T面板中的![轉換率](/help/integrations/assets/conversion-rate.png)

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

1. 將您新建立的「轉換率」量度拖放至現有面板。
1. 按一下齒輪圖示，然後取消選取&#x200B;**[!UICONTROL 百分比]**&#x200B;核取方塊，因為此值可能會導致混淆。

   正確設定報告應該會產生類似下列圖例的結果：

   A4T面板報表中的![不重複造訪轉換率](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## [!DNL Target]定義的轉換率

若要設定報表，請在A4T報表中進行下列變更：

| 所需變更 | 目標觸發的報告 | A4T面板報表 |
| --- | --- | --- |
| 使用[!DNL Target]轉換量度的[!DNL Analytics]報告 | <ul><li>移除[!UICONTROL 信賴度]量度。</li><li>移除[!UICONTROL 提升度（低）]和[!UICONTROL 提升度（高）]。 保持提升度（中等）。</li><li>取消核取[!UICONTROL 轉換率]資料行的百分比簡報，以避免混淆。 請參閱下列[A4T](#guidance)的整體指引。</li></ul> | <ul><li>移除[!UICONTROL 信賴度]量度。</li><li>移除[!UICONTROL 提升度（低）]和[!UICONTROL 提升度（高）]。 保留[!UICONTROL 提升度(Med)]。</li><li>取消核取[!UICONTROL 轉換率]資料行的百分比簡報，以避免混淆。 請參閱下列[A4T](#guidance)的整體指引。</li><li>確保日期和時間範圍符合您在[!DNL Target]報表中看到的值。 請參閱下列[A4T](#guidance)的整體指引。</li></ul> |

正確設定報告應該會產生類似下列圖例的結果：

![活動轉換](/help/integrations/assets/optimized-table.png)

## A4T的整體指引 {#guidance}

您可以從[!UICONTROL Target]的報告畫面按一下連結，導覽至預先建立的[!UICONTROL Analytics for Target]面板（這在本指南稍後稱為「[!DNL Target]觸發的報告」）。 或者，您可以在[!DNL Analytics]中建置A4T面板（本節稍後將詳述）。

以下各節會根據您選擇的這些方法，指定所需的組態。 不過，下列步驟可作為A4T的整體指引：

* 無論面板建立方法為何，都會從A4T面板移除信賴度量度（兩者皆詳見下文）。 請改為在[!DNL Target]報表中參考這些值。 此外，可在[!DNL Target]報告中識別活動獲勝者。 有關活動獲勝者識別的詳細資訊，請參閱下面的[識別活動獲勝者](#winner)區段。
&#x200B;>>
* 為避免混淆，請取消核取[!UICONTROL 轉換率]量度的[!UICONTROL 百分比]表示法。 請參閱下面的[隱藏轉換率]資料行(#hide-percentage)中的百分比。
&#x200B;>>
* 如果您正在建立A4T面板，請確定日期和時間範圍符合[!DNL Target]報表的日期和時間範圍。 請參閱下面的[在A4T面板](#aligning-date-and-time)中將日期和時間對齊。

### 從[!UICONTROL 轉換率]資料行隱藏百分比 {#hide-percentage}

1. 按一下[!UICONTROL 轉換率]資料行標題旁的&#x200B;**齒輪**&#x200B;圖示。

   轉換率資料行![&#128279;](/help/integrations/assets/coversion-rate-gear-icon.png)中的齒輪圖示

   顯示[!UICONTROL 欄]設定對話方塊：

   ![資料行設定對話方塊](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. 取消選取&#x200B;**[!UICONTROL 百分比]**&#x200B;核取方塊。

   您的A4T面板現在不包含百分比作為[!UICONTROL 轉換率]，且符合[!DNL Target]，如下所示：

   ![顯示無百分比的轉換率資料行](/help/integrations/assets/no-percentages.png)

### 在A4T面板中對齊日期和時間 {#aligning-date-and-time}

1. 在每個面板下方，檢查面板參考的日期範圍，確保日期範圍符合[!DNL Target]報表的日期範圍。

   ![A4T面板中的日期範圍](/help/integrations/assets/date-range.png)

1. 在[!DNL Analytics]中，將時間範圍設定為12:00am - 11:59pm。

### 識別活動獲勝者 {#winner}

當有成功轉換率的信賴值大於或等於95%時，就會選取[!DNL Auto-Allocate]個活動獲勝者。 這些值應在[!DNL Target]報表中參考，因為可信度計算反映[!UICONTROL 自動分配]活動中[!DNL Target]建議的較保守方法。 請參閱&#x200B;*[!UICONTROL Adobe Target商業從業者指南]*&#x200B;中的[自動分配的統計保證](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html?lang=zh-Hant#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank}。

>[!NOTE]
>
>[!DNL Analysis Workspace]中的A4T面板無法使用「尚未有贏家」和「贏家」徽章。 此外，應該忽略在[!UICONTROL 自動分配]活動的[!DNL Target]報告中顯示的獲勝者「星星」徽章。 請參閱&#x200B;*[!UICONTROL Adobe Target商業從業者指南]*&#x200B;中的&#x200B;*A4T對自動分配和自動鎖定目標活動的*&#x200B;支援[自動分配](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=zh-Hant#aa){target=_blank}。

### 在[!DNL Analysis Workspace]中為[!UICONTROL 自動分配]面板建立A4T

1. 若要建立[!UICONTROL 自動分配]活動報告的A4T面板，請從[!DNL Analysis Workspace]中的[!UICONTROL Analytics for Target]面板開始，如下所示。

   ![目標分析 — 自動分配報告](/help/integrations/assets/a4t-auto-allocate-report.png)

1. 進行下列選取：

   * **[!UICONTROL 控制體驗]**：選擇任何體驗。
   * **[!UICONTROL 標準化量度]**：選取&#x200B;**[!UICONTROL 訪客]** （預設包含在A4T面板中）。 [!UICONTROL 自動分配]一律會依據不重複訪客將轉換率標準化。
   * **成功量度**：選取您在活動建立期間使用的相同（最佳化）量度。 如果這是[!DNL Target]定義的轉換量度，請選取&#x200B;**[!UICONTROL 活動轉換]**。 否則，請選取您使用的[!DNL Adobe Analytics]量度。









