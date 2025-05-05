---
title: 將引數新增至請求
description: 在本課程中，我們會將Adobe生命週期量度和自訂引數新增至上一個課程中新增的Target請求。 這些量度和引數將用於在本教學課程稍後建立個人化對象。
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 0250e55f-a233-4060-84e1-86d1f88a6106
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# 將引數新增至請求

在本課程中，我們會將Adobe生命週期量度和自訂引數新增至上個課程中新增的[!DNL Target]請求。 這些量度和引數將用於在本教學課程稍後建立個人化對象。

## 學習目標

在本課程結束時，您將能夠：

* 新增Adobe行動生命週期量度
* 將引數新增至預先擷取請求
* 將引數新增至即時位置
* 驗證兩個請求的引數

## 新增生命週期引數

讓我們啟用[Adobe行動生命週期量度](https://experienceleague.adobe.com/docs/mobile-services/android/metrics.html?lang=en)。 這會將引數新增至位置請求，其中包含使用者裝置和與應用程式互動的豐富資訊。 我們將在下一個課程中，使用生命週期請求提供的資料來建立對象。

若要啟用生命週期量度，請再次開啟HomeActivity控制器，並將`Config.collectLifecycleData(this);`新增至onResume()函式：

![生命週期要求](assets/lifecycle_code.jpg)

### 驗證預先擷取請求的生命週期引數

執行模擬器並使用Logcat來驗證生命週期引數。 篩選「預先擷取」以尋找預先擷取回應，並尋找新引數：
![生命週期驗證](assets/lifecycle_validation.jpg)

即使我們只將`Config.collectLifecycleData()`新增至HomeActivity控制器，您也應該會在ThankYou畫面上看到與Target要求一併傳送的生命週期量度。

## 將at_property引數新增至預先擷取請求

Adobe Target屬性定義於[!DNL Target]介面中，用來建立個人化應用程式和網站的界限。 at_property引數可識別用來存取及維護您的優惠方案和活動的特定屬性。 我們將為預先擷取和即時位置請求新增屬性。

>[!NOTE]
>
>視您的授權而定，您在[!DNL Target]介面中可能會看到，也可能不會看到[內容]選項。 如果您沒有這些選項，或您未在公司中使用屬性，請跳至本課程的下一節。

您可以在[!UICONTROL Setup] > [!UICONTROL Properties]底下的[!DNL Target]介面中擷取您的at_property值。  將游標停留在屬性上，選取程式碼片段圖示並複製`at_property`值：

![複製at_property](assets/at_property_interface.jpg)

將其新增為預先擷取請求中每個位置的引數，如下所示：
![新增at_property引數](assets/params_at_property.jpg)
這是`targetPrefetchContent()`函式的更新程式碼（請務必更新&#x200B;_[!UICONTROL your at_property value goes here]_&#x200B;預留位置文字！）：

```java
public void targetPrefetchContent() {
        List<TargetPrefetchObject> prefetchList = new ArrayList<>();

        Map<String, Object> params1;
        params1 = new HashMap<String, Object>();
        params1.put("at_property", "your at_property value goes here");

        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
        Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
            @Override
            public void call(final Boolean status) {
                HomeActivity.this.runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        String cachingStatus = status ? "YES" : "NO";
                        System.out.println("Received Response from prefetch : " + cachingStatus);
                        engageMessage();
                        setUp();

                    }
                });
            }};
        Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
    }
```

### 關於引數的注意事項

對於未來的專案，您可能會想要實作其他引數。 `createTargetPrefetchObject()`方法允許三種型別的引數： `locationParams`、`orderParams`和`productParams`。 請參閱[有關將這些引數新增至預先擷取要求](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=en)的詳細資訊。

另請注意，可以將不同的位置引數新增至預先擷取請求中的每個位置。 例如，您可以建立另一個名為param2的Map，在其中放置新引數，然後在一個位置設定param2，並在另一個位置設定param1。 範例如下：

```java
prefetchList.add(Target.createTargetPrefetchObject(location1_name, params1);
prefetchList.add(Target.createTargetPrefetchObject(location2_name, params2);
```

## 驗證預先擷取請求中的at_property引數

現在執行模擬器，並使用Logcat來驗證at_property是否顯示在預先擷取的請求上，以及兩個位置的回應：
![驗證at_property引數](assets/parameters_at_property_validation.jpg)

## 新增自訂引數至即時位置請求

已在上一個課程中新增即時位置請求(wetravel_context_dest)，因此我們可以在預訂程式的最終確認畫面上顯示相關促銷。 我們想要根據使用者的目的地來個人化促銷活動，若要這麼做，我們會將其新增為請求中的引數。 我們也會新增原點和at_property值的引數。

將下列引數新增至ThankYouActivity控制器中的targetLoadRequest()函式：
![新增引數至即時位置要求](assets/parameters_live_location.jpg)
以下是targetLoadRequest()函式的更新程式碼（請務必更新「在此處新增您的at_property值」預留位置文字！）：

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Map<String, Object> locationParams = new HashMap<>();
    locationParams.put("at_property","add your at_property value here");
    locationParams.put("locationSrc", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.departure,"")));
    locationParams.put("locationDest", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.destination,"")));

    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, locationParams, new Target.TargetCallback<String>() {
        @Override
        public void call(final String response) {
        try {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    AppDialogs.dialogLoaderHide();
                    filterRecommendationBasedOnOffer(recommandations, response);
                    recommandationbAdapter.notifyDataSetChanged();
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        }
        }
    });
    Target.clearPrefetchCache();
}
```

### 驗證即時位置請求中的自訂引數

執行模擬器並開啟Logcat。 篩選其中一個引數，以確認請求包含所需的引數：
![驗證即時位置要求中的自訂引數](assets/parameters_live_location_validation.jpg)

>[!NOTE]
>
>訂單確認請求與引數：雖然未用於此示範專案，但訂單詳細資料通常會在實際實施中擷取，因此[!DNL Target]可將訂單詳細資料用作量度/維度。 請參閱檔案，瞭解如何[實作訂單確認請求和引數](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-target-methods.html?lang=en)的說明。

>[!NOTE]
>
>Analytics for Target (A4T)：可以將Adobe Analytics設定為[!DNL Target]的報告來源。 如此一來，您就可以在Adobe Analytics中檢視Target SDK收集的所有量度/維度。 如需詳細資訊，請參閱[A4T總覽](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=zh-Hant)。

做得很好！引數已就緒後，我們準備使用這些引數在Adobe Target中建立對象和選件。

**[下一步：「建立對象和選件」>](create-audiences-and-offers.md)**
