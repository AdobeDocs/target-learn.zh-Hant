---
title: 優化您的Adobe Target實施
description: 瞭解Adobe Target的實施和結構。 瞭解如何瞭解和審核您組織的設定。 瞭解為團隊建立知識庫的常見故障排除技巧和技巧。
solution: Target
exl-id: 49b69f41-0993-437c-bb69-84392be427df
source-git-commit: 46f61d8f503f230a79b4072ea0d75edd41403708
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# 優化您的Adobe Target實施

如果您是您公司的新人，並且希望熟悉測試和優化實踐中的具體內容，本文將幫助您開始工作。 我們首先將概述Adobe Target的實施和結構。 您將學習如何理解和審核您組織的設定。 最後，我們將討論為您的團隊建立知識儲存庫的常見故障排除技巧和技巧。

Adobe Target是一種工具，它允許測試不同訪問者的獨特內容並將其定位。 有關可用功能的概述， [訪問本指南](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en)。

## 目標實現和結構

在深入瞭解Adobe Target的實施過程或其結構之前，首先瞭解一些有關軟體的基本知識會有所幫助。

Adobe Target是一種工具，它允許對不同訪問者測試和定位獨特內容，而不必更改本地網站代碼。 Target會臨時更改最終用戶體驗，並在看到更改後跟蹤用戶的行為。 Target還提供了根據配置檔案資訊或先前操作改變最終用戶體驗的能力。

有三種目標基本活動類型：

1. A/B 測試
2. 多元測試
3. 體驗測試

**A/Btest** 比較兩個或兩個以上的經驗，以查看哪些經驗能最好地改善在預先指定的test期間的轉換。 A/Btest是一種高度受控的流量測量實驗，它按百分比而非規則進行分割，使您能夠：

* 分析test資料。
* 瞭解你的觀眾。
* 確定哪種體驗表現最好。

**多元測試** (MVT)比較頁面上元素之間的優惠組合，以查看哪種組合對特定受眾的效果最佳。 此test還標識頁中哪個元素在預指定的test期間最能改善轉換。 MVT提供：

* 一種在多個元素中顯示多個優惠的方法。
* 一種針對特定目標test所得獨特體驗的方法。
* 瞭解哪些要素對訪問者互動產生最大的負面或積極影響。

**體驗測試** （經驗針對性）根據一組由營銷人員定義的規則和標準向特定受眾提供內容。 該方法基於一組定義的分配規則向特定受眾定向特定內容的方法。

塔吉特是如何工作的？

下面是一個關於Target如何工作的高級示例：

1. 訪問者從您的伺服器請求頁面，並在瀏覽器中顯示。
1. 在訪問者的瀏覽器中設定第一方cookie以儲存行為。
1. 然後，該頁打給Adobe Target。
1. 內容根據用戶活動的規則顯示。
1. Adobe Target捕獲活動配置中定義的特定指標，以評估test體驗的影響。

Target構建在「全局Mbox」上，該框提供了影響頁面上任何內容的能力。 此功能將在頁面載入時部署，或者作為指向at.js檔案的硬編碼連結，或者使用「標籤管理器」(如「Adobe啟動」)交付。

## 瞭解您當前的實施

要瞭解您當前的實施，Adobe建議您查看目標用戶介面實施以及標籤管理器和頁面載入實施。

**查看 [!DNL Target] 用戶介面：**

1. 開始查看 [!DNL Target] UI:

   * 查看 [!DNL Target] 技術堆棧
   * 確認可用功能
   * 確定部署的活動位置

1. 審查活動以獲得最佳做法：

   * 審查方案成熟度的歷史市場活動

1. 停用舊活動：

   * 存檔和清理 [!DNL Target] 已不再具有當前或未來使用的資產

1. 查看觀眾。

1. 查看環境定義和關聯域。

1. 查看配置檔案指令碼以瞭解適用性

   * 所有配置檔案指令碼在每次目標調用上運行
   * 通過刪除不適用的指令碼來保持呼叫效率

要查看標籤管理器和頁載入：

1. 在標籤管理器中確認以下內容：

   * 部署預期 [!DNL Target] JavaScript代碼
   * 適當的內容隱藏解決方案
   * 設定必要規則以填充 [!DNL Target] 具有預期參數的調用

1. 在載入頁面期間確認以下內容：

   * 匹配請求URL和 [!DNL Target] 請求URL
   * 已填充經驗雲ID值（雲主體）
   * 顯示預期整合值（雲主體）
   * 已填充 [!DNL Target] 相應頁面上的參數

## [!DNL Target] 審計活動

避免手動瀏覽每個頁面進行審核 [!DNL Target] 活動，請使用Adobe審計員幫助瞭解您實施的當前技術狀態。 Adobe審計員由IspertPoint提供支援，可以設定為在手動級別運行，以確定您站點上的高級別實施問題。

Adobe審計員規定：

* 高位健康
* 實施問題的快速呼籲

Adobe建議執行月度手動審核，以：

* 標識未標籤的頁面
* 識別不一致的版本
* 查找最新版本
* 提供可導出的詳細資訊

## 常見故障排除

>[!NOTE]
>
>Adobe建議安裝Adobe Experience Platform調試器。

以下是輸入「Experience（體驗）」時的一般故障排除提示：

### 快取和Cookie**

* 清除快取和Cookie
* 使用專用模式時要小心(例如：Firefox中的私有模式可以阻止 [!DNL Target])

### 您有資格參加活動嗎？

* 檢查您執行的步驟是否與活動中使用的受眾相同
* 使用 `mboxTrace` 或響應令牌檢查配置檔案和段值

### 驗證可視/功能時的常規故障排除提示

如果在 [!DNL Target] 體驗，而您看不到預期的視覺體驗：

檢查 [!DNL Target] 響應：

* 如果代碼未執行：

1. 檢查衝突活動
1. 聯繫客戶保護

* 如果代碼已執行：

1. 在該方案中重新處理代碼

## 維護知識庫

知識庫是用於記錄和共用資訊的線上平台。 知識儲存庫包含特定於您的實施的資訊，並可包含特定於團隊的資訊。

理想情況下，儲存庫應允許在平台內編輯和自動保存。 初始配置後，便易於維護和保持最新。 知識庫中的內容是根據用戶角色進行管理的。

知識庫中的典型文檔包括：

* **概述文檔**  — 用於明確說明方案目標、目標、流程和結構的檔案
* **標識儲存庫**  — 用於管理和排定未準備好測試流程的潛在想法的文檔
* **計畫路線圖**  — 一份文檔，用於在想法準備好開始測試過程時管理測試活動的所有方面
* **活動計畫文檔**  — 用於概述構建和啟動活動所需資訊的文檔
* **活動計畫文檔**  — 用於向利益相關方通報結果和建議後續步驟的檔案
* **程式儀表板**  — 用於跟蹤計畫績效、節奏和收入收益的文檔。

有關詳細資訊，請查看 [網路研討會](https://adobecustomersuccess.adobeconnect.com/p4p7xlp7dh42mp4/) 高級顧問，懷爾德·弗里德。

瞭解有關策略和思想領導的更多資訊 [客戶成功](https://experienceleague.corp.adobe.com/docs/customer-success/customer-success/overview.html) 中。
