---
title: 最佳化Adobe Target實施
description: 取得Adobe Target實施與結構的概觀。 瞭解如何瞭解及稽核組織的設定。 瞭解為團隊建立知識存放庫的常見疑難排解技巧和提示。
solution: Target
feature: Overview
role: Leader, User
exl-id: 49b69f41-0993-437c-bb69-84392be427df
source-git-commit: 20bd1eb17ef6e287f7b76e14f727456e12d6f115
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# 最佳化Adobe Target實施

如果您是組織的新手，且想熟悉測試和最佳化實務中已進行的專案，本文可協助您開始使用。 我們將從概述Adobe Target實作和結構開始。 您將瞭解如何瞭解和稽核組織的設定。 最後，我們將討論常見的疑難排解技巧以及建立團隊知識存放庫的秘訣。

Adobe Target是可測試不重複內容並鎖定其目標給不同訪客的工具。 如需可用功能的概述， [請瀏覽本指南](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en).

## Target實作與結構

在我們深入探討Adobe Target的實作流程或架構方式之前，先瞭解一些關於軟體的基礎知識會很有幫助。

Adobe Target工具可測試和鎖定不同訪客的不重複內容，而不需變更原生網站程式碼。 Target會暫時變更一般使用者體驗，以及在看到變更後追蹤使用者行為。 Target也提供根據設定檔資訊或先前動作變更一般使用者體驗的功能。

有三種Target基本活動型別：

1. A/B 測試
2. 多變數測試(MVT)
3. 體驗測試

**A/B測試** 比較兩個或多個體驗，以檢視在預先指定的整個測試期間，哪個體驗最能改善轉換。 A/B測試是高度受控的流量測量實驗，依百分比而不是規則分割，允許您：

* 以分析測試資料。
* 以取得有關您對象的深入分析。
* 以判斷哪個體驗的效能最佳。

**多變數測試** (MVT)會比較頁面上元素之間選件的組合，以檢視哪個組合對特定對象執行時效果最佳。 此測試也會找出頁面的哪個元素在整個預先指定的測試期間最能改善轉換。 MVT提供：

* 在多個元素中顯示多個選件的方式。
* 根據特定目標測試所產生獨特體驗的方法。
* 深入瞭解哪些元素對訪客互動的負面或正面影響最大。

**體驗測試** （經驗豐富的鎖定目標）會根據一組行銷人員定義的規則和條件為特定對象提供內容。 此方法提供一種方法，可讓您根據一組已定義的配置規則，將特定內容鎖定在特定對象。

Target如何運作？

以下是Target運作方式的高層級範例：

1. 訪客向您的伺服器請求頁面，該頁面隨即顯示在瀏覽器中。
1. 訪客的瀏覽器中會設定第一方Cookie以儲存行為。
1. 然後，頁面會呼叫Adobe Target。
1. 內容會根據使用者活動的規則顯示。
1. Adobe Target會擷取活動設定中定義的特定量度，以評估測試體驗的影響。

Target是以「全域Mbox」為基礎所建置，可影響頁面上的任何專案。 此功能會在頁面載入時部署為at.js檔案的硬式編碼連結，或使用Tag Manager (例如Adobe Launch)傳遞。

## 瞭解您目前的實作

若要瞭解您目前的實施，Adobe建議您檢閱Target使用者介面實施，以及您的Tag Manager和頁面載入實施。

**若要檢閱您的 [!DNL Target] 使用者介面：**

1. 開始您的評論： [!DNL Target] UI：

   * 檢閱 [!DNL Target] 技術棧疊
   * 確認可用的功能
   * 識別部署上線的位置

1. 檢閱活動以取得最佳實務：

   * 檢閱方案成熟度的歷史行銷活動

1. 停用舊活動：

   * 封存和清除 [!DNL Target] 不再有目前或未來使用的資產

1. 檢閱對象。

1. 檢閱環境定義和相關網域。

1. 檢閱設定檔指令碼是否適用

   * 所有在每個目標呼叫上執行的設定檔指令碼
   * 移除不適用的指令碼，以維持呼叫效率

若要檢閱標籤管理器和頁面載入：

1. 在標籤管理員中確認下列專案：

   * 部署預期的 [!DNL Target] JavaScript代碼
   * 適當的內容隱藏解決方案
   * 設定必要規則以填入 [!DNL Target] 具有預期引數的呼叫

1. 在頁面載入期間確認下列專案：

   * 比對請求URL和的版本號碼 [!DNL Target] 請求URL
   * 已填入體驗中的雲端ID值（雲端內文）
   * 呈現預期的整合值（雲端內文）
   * 已填入 [!DNL Target] 相關頁面上的引數

## [!DNL Target] 稽核活動

避免手動瀏覽每個要稽核的頁面 [!DNL Target] 活動，請使用AdobeAuditor來協助瞭解您實作的目前技術狀態。 Adobe Auditor由ObservePoint提供技術支援，並可設定為以手動方式執行，以識別您網站上的高層級實作問題。

Auditor提供的Adobe：

* 高網站健康狀態
* 實作問題的快速通知

Adobe建議執行每月手動稽核至：

* 識別未標籤的頁面
* 識別不一致的版本
* 尋找過時的版本
* 提供可匯出的詳細資訊

## 常見疑難排解

>[!NOTE]
>
>Adobe建議安裝Adobe Experience Platform Debugger。

以下是進入Experience時的一般疑難排解提示：

### 快取和Cookie**

* 清除快取和Cookie
* 謹慎使用私密模式(例如：Firefox中的私密模式可能會封鎖 [!DNL Target])

### 您符合活動資格嗎？

* 檢查您是否已執行對象在活動中使用的相同步驟
* 使用 `mboxTrace` 或回應Token以檢查設定檔和區段值

### 驗證視覺效果/功能時的一般疑難排解提示

如果位於 [!DNL Target] 體驗，而您沒有看到預期的視覺體驗：

檢查 [!DNL Target] 回應：

* 如果未執行程式碼：

1. 檢查衝突的活動
1. 聯絡客戶服務

* 如果程式碼已執行：

1. 在該案例中重新使用程式碼

## 維護知識存放庫

知識存放庫是用於記錄和分享資訊的線上平台。 知識存放庫包含實作的特定資訊，並可包含團隊特定的資訊。

理想情況下，存放庫應允許在平台內進行編輯和自動儲存。 一旦完成初始設定，即可輕鬆維護並隨時掌握最新資訊。 知識存放庫中的內容是根據使用者角色進行管理。

知識存放庫中的典型檔案包括：

* **概觀檔案**  — 用來清楚說明方案目標、目的、流程和結構的檔案
* **創意力存放庫**  — 一份檔案，用於管理和優先處理尚未準備好進行測試程式的潛在想法
* **計畫藍圖**  — 一份檔案，用於在想法準備好開始測試流程後，管理測試活動的各個方面
* **活動計畫檔案**  — 概述建置和啟動活動所需資訊的檔案
* **活動計畫檔案**  — 一份用來向利害關係人傳達結果和建議後續步驟的檔案
* **計畫儀表板**  — 用來追蹤一段時間內計畫績效、步調和收入利益的檔案。

如需詳細資訊，請參閱我們的 [網路研討會](https://adobecustomersuccess.adobeconnect.com/p4p7xlp7dh42mp4/) 與資深顧問Wilder Freed合作。

若要進一步瞭解策略與思想領導力，請前往 [客戶成功](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html) 集線器。
