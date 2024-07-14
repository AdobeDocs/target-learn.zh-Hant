---
title: 功能標幟
description: Adobe Target可用來實驗色彩、復本、按鈕、文字和影像等UX功能，並將這些功能提供給特定對象。
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 034d13f2-63b1-44b0-b3dc-867efe37672f
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---

# 功能標幟

行動應用程式產品擁有者需要靈活地在他們的應用程式中推出新功能，而無需投資多個應用程式版本。 他們可能也會想要逐步將功能推出至使用者群的一定比例，以測試成效。 Adobe Target可用來實驗色彩、復本、按鈕、文字和影像等UX功能，並將這些功能提供給特定對象。

在本課程中，我們將建立「功能標幟」選件，可作為啟用特定應用程式功能的觸發條件。

## 學習目標

在本課程結束時，您將能夠：

* 新增位置至批次預先擷取請求
* 使用將作為功能標幟的選件建立[!DNL Target]活動
* 在您的應用程式中載入及驗證功能標幟選件

## 將新位置新增至首頁活動的預先擷取請求

在先前課程中的示範應用程式中，我們將在「首頁活動」中的預先擷取請求中新增一個名為「wetravel_feature_flag_recs」的位置，並使用新的Java方法將其載入到畫面中。

>[!NOTE]
>
>使用預先擷取要求的好處之一，是新增要求不會新增任何額外的網路負荷，或導致額外的載入工作，因為要求會封裝在預先擷取要求中

首先，確認wetravel_feature_flag_recs常數已新增至Constant.java檔案：

![新增功能標幟常數](assets/feature_flag_constant.jpg)

程式碼如下：

```java
public static final String wetravel_feature_flag_recs = "wetravel_feature_flag_recs";
```

現在將位置新增至預先擷取要求，並載入名稱為`processFeatureFlags()`的新函式：

![功能標幟碼](assets/feature_flag_code.jpg)

以下是完整的更新程式碼：

```java
public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();

    Map<String, Object> params1;
    params1 = new HashMap<String, Object>();
    params1.put("at_property", "7962ac68-17db-1579-408f-9556feccb477");

    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_feature_flag_recs, params1));

    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    engageMessage();
                    processFeatureFlags();
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}

public void processFeatureFlags() {
    Target.loadRequest(Constant.wetravel_feature_flag_recs, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Feature Flags : " + s);
                            if(s != null && !s.isEmpty()) {
                                //enable or disable features
                            }
                        }
                    });
                }
            });
}
```

### 驗證功能標幟請求

新增程式碼後，請在首頁活動上執行模擬器，並觀察Logcat是否有更新的回應：

![驗證功能標幟位置](assets/feature_flag_code_logcat.jpg)

## 建立功能標幟JSON選件

我們現在將建立簡單的JSON選件，做為特定對象（在應用程式中推出功能的對象）的標幟或觸發器。 在[!DNL Target]介面中，建立新的選件：

![建立功能標幟JSON選件](assets/feature_flag_json_offer.jpg)

以值{&quot;enable&quot;：1}將其命名為「功能標幟v1」

![feature_flag_v1 JSON選件](assets/feature_flag_json_name.jpg)

## 建立活動

現在來使用該選件建立A/B測試活動。 如需建立活動的詳細步驟，請參閱上一課。 此範例中，活動將只需要一個對象。 在即時案例中，您可能想要建置特定自訂對象以供特定功能推出，然後設定活動以使用這些對象。 在此範例中，我們僅會分配50/50的流量（50%給會看到功能更新的訪客，50%給會看到標準體驗的訪客）。 以下是活動的設定：

1. 將活動命名為「功能標幟」
1. 選取「wetravel_feature_flag_recs」位置
1. 將內容變更為「功能標幟v1」JSON選件

   ![功能標幟活動設定](assets/feature_flag_activity.jpg)

1. 按一下&#x200B;**[!UICONTROL Add Experience]**&#x200B;以新增體驗B。
1. 離開「wetravel_feature_flag_recs」位置
1. 保留&#x200B;**[!UICONTROL Default Content]**&#x200B;以取得內容
1. 按一下「**[!UICONTROL Next]**」以前往[!UICONTROL Targeting]畫面

   ![功能標幟活動設定](assets/feature_flag_activity_2.jpg)

1. 在[!UICONTROL Targeting]畫面上，確認[!UICONTROL Traffic Allocation]方法已設定為預設設定（手動），而且每個體驗都有預設的50%配置。 選取&#x200B;**[!UICONTROL Next]**&#x200B;以前進到&#x200B;**[!UICONTROL Goals & Settings]**。

   ![功能標幟活動設定](assets/feature_flag_activity_3.jpg)

1. 將&#x200B;**[!UICONTROL Primary Goal]**&#x200B;設為&#x200B;**[!UICONTROL Conversion]**。
1. 將動作設為&#x200B;**[!UICONTROL Viewed an Mbox]**。 我們將使用「wetravel_context_dest」位置（由於此位置位於「確認」畫面上，因此我們可使用它來檢視新功能是否帶來更多轉換）。
1. 按一下 **[!UICONTROL Save & Close]**。

   ![功能標幟活動設定](assets/feature_flag_activity_4.jpg)

啟動活動。

## 驗證功能標幟活動

現在使用模擬器來觀察請求。 由於我們已將目標定位設為50%的使用者，因此50%的使用者會看到功能標幟回應包含`{enable:1}`值。

![功能標幟驗證](assets/feature_flag_validation.jpg)

如果您沒有看到`{enable:1}`值，表示您未鎖定體驗的目標。 作為臨時測試，若要強制顯示選件，您可以：

1. 停用活動。
1. 在新功能體驗中將流量分配變更為100%。
1. 儲存並重新啟用。
1. 擦除模擬器上的資料，然後重新啟動應用程式。
1. 選件現在應該會傳回`{enable:1}`值。

在即時案例中，`{enable:1}`回應可用於在您的應用程式中啟用更多自訂邏輯，以顯示您要顯示目標對象的特定功能集。

## 結論

做得很好！您現在已具備將功能推出至特定使用者對象所需的技能。
