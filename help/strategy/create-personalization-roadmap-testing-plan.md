---
title: 用於個性化測試和路線圖建立的快速入門
description: 瞭解一個框架，您可以使用該框架開始驗證個性化活動並建立個性化路線圖，以通過Adobe Target和Adobe Analytics執行。
solution: Target,Analytics
exl-id: c0b6f9a0-7074-4e25-81e6-9781a54e2156
source-git-commit: 46f61d8f503f230a79b4072ea0d75edd41403708
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 0%

---

# 用於個性化測試和路線圖建立的快速入門

個性化功能強大，但必須通過測試來驗證，以確保它真正帶來價值。 測試是確定您應該個性化的人、方式和內容的最有效策略。

隨著我們進入21世紀的第二個十年，像您這樣的組織正在拋棄過時的消費者目標戰略和不準確的資料分析。 這是個性化的開始，在這個時代，消費者們開始期待的不過是定制體驗。 企業級個性化是一個複雜且不斷變化的過程，但是，在有效完成後，它將最大限度地提高客戶滿意度並大幅提高ROI。

以下文章提供了一個框架，您可以使用它開始驗證個性化活動並建立個性化路線圖，以通過Adobe Target和Adobe Analytics執行。 Adobe的快速啟動框架包括：

1. **確定個性化機會**  — 利用資料分析確定影響您站點上關鍵績效指標的機會，這些指標與您組織的業務目標相關。

1. **制定使用案例**  — 定義個性化活動的目標，同時考慮特定的訪問者屬性，明確說明策劃的內容將如何改善訪問者的體驗，預先確定成功的樣子以及從test學習中可以採取哪些措施。

1. **建立路線圖**  — 匯總清單並排定個性化使用案例的優先順序，確保您的工作重點放在高價值活動上；希望根據所學知識改進和修訂使用案例和路線圖。

1. **設計和執行**  — 構建並啟動Adobe Target活動，為您的優先受眾提供策劃的內容。

1. **對結果採取操作**  — 分析活動績效並匯總活動結果、見解、建議和後續步驟。

## 步驟1:確定個性化機會{#personalization}

這是開始建立個性化路線圖的起點。 在運行成功的個性化程式時，必須將重點放在關鍵業務目標和關鍵績效指標上。 個人化努力應相應地加以調整，以便提供價值。 Adobe商業顧問保羅莫里斯說：&quot;如果你所做的一切都符合這些目標，你的計畫極有可能創造巨大的價值。 但是，如果您採用一種分散的測試方法，您可能會發現一些成功，但您的整體計畫不會像以前那樣成功。」

>[!NOTE]
>
>如果您不立即瞭解您的主要業務目標是什麼，那麼盡快確定這些目標非常重要。 確保：


* 建立業務目標與可操作假設之間的協調。 這樣，您就可以優先安排為業務帶來最大價值的使用案例。

* 讓目標可以衡量，以便跟蹤目的並與收入影響相關聯。

* 調整每個機會應影響一個單一目標指標。

有時，你可能有一些最初看上去也不那麼明確的目標，比如品牌價值或忠誠度。 至關重要的是，您能夠測量這些資料，以便將它們用作個性化活動的目標指標。 通常，這些類型的目標仍可以與收入影響（如終生客戶價值或購置成本）相協調。在您進行過程中，請確保定期根據關鍵業務目標檢查程式效能，以確保價值從您的個性化計畫中得到驅動。

重點資料分析，確定可改進的網站的特定區域。 Adobe建議從Adobe Analytics開始生成目標使用案例。 如果您有一個分析團隊，請讓他們查看以下內容：

1. 個人表格前表 — 提供無限細目並可以幫助您回答可能存在的任何問題或假設的理想功能。
1. 高級分段 — 分段IQ允許您比較站點不同部分的訪問者。
1. 法律評論 — 確定您的網站哪些部分最能從個性化中受益。 這些評論允許您退後一步，像客戶一樣瀏覽您的站點。
1. 競爭對手分析 — 很可能，其他企業也面臨著與你一樣的挑戰。 這一分析不僅限於同行業的公司。

這一步驟的目標是以假設的形式產生可操作的洞察力。 假設是你在進行實驗之前所做的預測。 它清楚地說明了正在發生的變化，你相信結果會是什麼，以及你為什麼認為是這樣。 進行這個實驗要麼會證明，要麼會反駁你的假設。 在此步驟的最後，您應該有一套個性化機會的假設，這些假設將改善您的網站和訪問者滿意度。

## 步驟2:制定使用案例{#use-cases}

從步驟1中生成的假設開始，然後圍繞這些假設展開活動。 現在，您可以開發在步驟1A中建立的預表格；每個關鍵績效指標都有一套假設，然後變成Adobe Target內的個人test。 如果您正在努力達到這一點，請盡可能簡單地開始，例如關注頻繁訪問您站點的返程訪問者。 請考慮如何為返回的訪問者定制首頁。 一旦您有了一組假設，您需要定義每個活動，以有效地排定每個使用案例的優先順序。

1. 定義您要向其提供個性化內容的優先受眾，同時注意定義其身份和想要什麼的獨特訪問者屬性（例如，現有客戶與潛在客戶客戶）優先受眾的需求和需要應與您的業務目標保持一致

1. 確定訪問者行程中個性化內容影響最大的特定位置。 重點介紹您期望訪問各種不同角色的訪問者或具有不同需求/意圖的訪問者的頁面。

1. 開始計畫變型的設計工作。 內容應根據特定的受眾需求和需求進行仔細的規劃，考慮他們的旅途。 正確的內容應是獨特和不同的。

## 第3步：建立路線圖、聚合和排定使用案例的優先順序

聚合一個完整的個性化機會清單，該清單可以最少捕獲個性化活動的位置、理念和優先順序。

優先順序步驟分為兩個因素：

**值：** 利用行業研究、基準評估和過去類似的使用案例，瞭解您的每個假設都可能帶來的預期價值。 您希望將您的價值直接連結到您的關鍵業務成果(KBO)之一，並採用標準格式，以便您的每個使用案例可以相互比較。 最常見的方法是對每個用例應用貨幣值進行比較。

* 成本 — 在目標系統內構建設計變型，然後潛在推廣，會帶來自然成本。 現在，您需要估計與每個使用案例關聯的成本。 成本包括構建test體驗、計畫和後期test分析所需的時間和資源。

Adobe建議您將每個使用案例按1到5的比例進行排序；1簡單，5複雜。 您現在可以在Adobe Target內test一組按優先順序排列的活動。 這些活動將構成您年度個性化活動的基礎。 Adobe建議定期重新評估個性化路線圖。 每項活動的學習將影響您的前瞻性路線圖優先順序。 如果及時採取行動，學習和建議將更具影響力。 全年的優先事務可能會發生變化，但執行迭代方法可確保您始終擁有戰略行動計畫，並能夠跟蹤團隊和公司目標。

## 第4步：設計和執行

利用建立的文檔為個性化用例制定策略，在目標內構建個性化活動，為優先受眾提供已整理的內容。 確保活動類型、設定、經驗和報告功能與使用案例的目標相一致。 設計、QA和啟動個性化工作在涉及現有組織流程時最為有效。

## 第5步：對結果採取操作

在您的個性化活動與具有代表性的訪問者示例進行接洽後，您就可以開始利用洞察力進行分析，以指導後續步驟。 在分析中以資料為導向，將建議與使用案例假設聯繫起來，並清楚地說明對業務目標的影響。

### 詳細資訊

我們建議您觀看此視頻，討論以下每個步驟： [https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/](https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/)

瞭解有關策略和思想領導的更多資訊 [客戶成功](https://experienceleague.corp.adobe.com/docs/customer-success/customer-success/overview.html) 中。