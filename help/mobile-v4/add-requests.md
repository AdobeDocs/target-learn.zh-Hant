---
title: 添加Adobe Target請求
description: 'AdobeMobile Services SDK(v4)提供Adobe Target方法與功能，讓您針對不同的使用者提供不同的體驗，以個人化您的應用程式。   '
role: 開發人員
level: 中級
topic: 行動、個人化
feature: 實施行動
doc-type: tutorial
kt: 3040
thumbnail: null
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 0%

---


# 添加Adobe Target請求

AdobeMobile Services SDK(v4)提供Adobe Target方法和功能，讓您針對不同的使用者提供不同的體驗，以個人化您的應用程式。 通常，會從應用程式向Adobe Target提出一或多個要求，以擷取個人化內容並評估該內容的影響。

在本課中，您將透過實作[!DNL Target]請求，準備We.Travel應用程式以進行個人化。

## 必要條件

請務必[下載並更新範例應用程式](download-and-update-the-sample-app.md)。

## 學習目標

在本課程結束時，您將能夠：

* 使用批次預回遷請求快取多個[!DNL Target]選件（即個人化內容）
* 載入預取的[!DNL Target]位置
* 即時載入[!DNL Target]位置（未預取）
* 從快取中清除預取位置
* 驗證預取和即時請求

## 術語

以下是我們在本教學課程的其餘部分中使用的一些關鍵Target術語。

* **請求：**  對Adobe Target伺服器的網路請求
* **選件：**  在使用者介面（或使用API）中定義的程式碼片段或其他文字 [!DNL Target] 內容，會在回應中傳送。當[!DNL Target]用於原生行動應用程式時，通常為JSON。
* **位置：**  指定給請求的使用者定義名稱，用於介 [!DNL Target] 面中，以關聯選件與特定請求
* **批次請求：**  包含多個位置的單一請求
* **預回遷請**  求：擷取選件並將選件快取至記憶體中的單一請求，以供日後在應用程式中使用
* **批預回遷請求：**  一個預回遷多個位置選件的請求
* **觀眾：**  在介面中定義或從其 [!DNL Target] 他Adobe應 [!DNL Target] 用程式共用的訪客群(例如「iPhone X訪客」、「加州的訪客」、「第一個應用程式開啟」)
* **活動：**  在使 [!DNL Target] 用者介面（或使用API）中定 [!DNL Target] 義的建構，連結位置、優惠和觀眾以建立個人化體驗

## 添加批預回遷請求

我們將在We.Travel中實作的第一個請求是批預回遷請求，主螢幕上有兩個[!DNL Target]位置。 在稍後的課程中，我們將針對顯示訊息的位置設定選件，以協助引導新使用者完成訂房程式。

預回遷請求通過快取Adobe Target伺服器響應（選件）盡可能少地提取[!DNL Target]內容。 批預回遷請求檢索並快取多個選件，每個選件與不同位置相關聯。 所有預先擷取的位置都會快取在裝置上，以供日後在使用者作業中使用。 透過預先擷取「首頁畫面」上的多個位置，我們可以擷取選件，以便在訪客瀏覽應用程式時稍後使用。 有關預回遷方法的詳細資訊，請參閱[預回遷文檔](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html)。

### 添加批預回遷請求

讓我們更新HomeActivity控制器（主畫面的原始碼），它位於應用程式> main > java > com.wetravel >控制器下。 我們將新增紅色顯示的兩個程式碼區塊：

我們將從HomeActivity控制器（主畫面的原始碼）開始，它位於應用程式> main > java > com.wetravel >控制器下。

我們將新增紅色顯示的兩個程式碼區塊：

![HomeActivity預回遷代碼](assets/homeactivity.jpg)

向下滾動到HomeActivity代碼的末尾，並在`setHeader()`函式和&#x200B;*替換*&#x200B;當前`onResume()`函式後添加下面提供的代碼：

```java
@Override
protected void onResume() {
    super.onResume();
    targetPrefetchContent();
}

public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, null));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, null));
    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}
```

IDE可能會警告您檔案中沒有導入的[!DNL Target]類。 請務必匯入位於HomeActivity控制器頂端的[!DNL Target]類別，如下列紅色所示：

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![匯入目標類別](assets/import.jpg)

您可能也會看到「找不到符號變數wetravel_engage_home」和「找不到符號變數wetravel_engage_search」的錯誤。 將這些新增至`Constant.java`檔案（在應用程式> src > main > java > com > wetravel > Utils）:

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![將位置名稱添加到Constant.java檔案](assets/constants.jpg)

### 批預回遷請求代碼說明

| 程式碼 | 說明 |
|--- |--- |
| `targetPrefetchContent()` | 使用[!DNL Target]方法來擷取和快取兩個[!DNL Target]位置的使用者定義函式（非SDK的一部分）。 |
| `prefetchContent()` | 發送預回遷請求的[!DNL Target] SDK方法 |
| `Constant.wetravel_engage_home` | 預取[!DNL Target]位置名稱，將在首頁畫面上顯示其選件內容 |
| `Constant.wetravel_engage_search` | 預取[!DNL Target]位置名稱，此名稱會在搜尋結果畫面上顯示其選件內容。 由於這是預回遷中的第二個位置，因此此預回遷請求稱為「預回遷批請求」。 |
| setUp() | 在預取[!DNL Target]選件後轉譯應用程式首頁的使用者定義函式 |

### 關於非同步與同步

使用我們剛剛實施的代碼，預回遷請求會在主螢幕呈現之前作為同步、阻止的調用發出。 將新代碼貼上到HomeActivity控制器中時，我們將`setUp()`函式執行從`onResume()`函式移至Target請求後。 當您想要在應用程式首次開啟時個人化內容時，這可能會有所裨益，因為它可確保來自Target伺服器的個人化內容在第一個畫面轉譯前已傳回（或逾時）。 若要允許請求以非同步方式載入（在背景），請改為在`onCreate()`函式中呼叫`setUp()`。

### 驗證批預回遷請求

重新建立應用程式並開啟Android模擬器。 （下列螢幕擷取畫面使用Android Q 9+版、API層級29上的Pixel 2）。 預回遷響應應讀取「收到預回遷響應」:

在顯示「首頁」螢幕時，應載入預回遷請求。 使用Logcat，篩選[!DNL "Target"]以查看請求和回應：

![在主畫面上驗證請求](assets/prefetch_validation.jpg)

如果您未看到成功的回應，請驗證`ADBMobileConfig.json`檔案中的設定，以及HomeActivity檔案中的程式碼語法。

現在會將兩個位置快取至裝置。 位置名稱很快就會延遲載入至[!DNL Target]介面，當您在活動中使用這些名稱時，可在各種下拉式選單中選取。

### 為每個快取位置新增載入請求

現在位置已預先擷取，且其回應已快取至裝置，現在讓我們新增`Target.loadRequest()`方法，從快取中擷取選件內容，讓您使用它來更新應用程式。 我們將添加名為`engageMessage()`的新自定義方法，該方法將隨預回遷請求一起運行。 `engageMessage()` 會打電話 `Target.loadRequest()`。`engageMessage()` 在設定 `setUp()` 畫面之前執行，以確保已呼叫載入請求。

首先，在HomeActivity中為wetravel_engage_home位置添加`engageMessage()`調用和方法：

![新增第一個載入請求](assets/wetravel_engage_home_loadRequest.jpg)

以下是更新的程式碼：

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
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_home, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Engage Message : " + s);
                            if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                        }
                    });
                }
            });
    }
```

現在，在SearchBusActivity中新增wetravel_engage_search位置的`engageMessage()`呼叫與方法。 請注意，在呼叫`setUpSearch()`之前，`engageMessage()`呼叫是在`onResume()`方法中設定的，因此會在設定畫面之前執行：

![新增第二個載入請求](assets/wetravel_engage_search_loadRequest.jpg)

以下是更新的程式碼：

```java
    @Override
    public void onResume() {
        super.onResume();
        engageMessage();
        setUpSearch();
    }
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_search, "", null, null, null,
                new Target.TargetCallback<String>(){
                    @Override
                    public void call(final String s) {
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                System.out.println("Engage Message : " + s);
                                if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                            }
                        });
                    }
                });
    }
```

由於您剛剛將Target方法新增至SearchBusActivity，請務必匯入[!DNL Target]類別：

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## 新增即時請求

我們將新增至應用程式的下一個要求是「感謝」畫面上的即時要求。 「即時」是指會立即提出請求並套用回應（不會在稍後快取）。 在稍後的課程中，我們將使用此要求建立個人化的體驗，以符合使用者的旅行目的地。

因此，我們在「感謝」畫面上新增即時要求。 在ThankYouActivity檔案中，我們將進行以紅色顯示的變更：
![在感謝畫面上新增即時位置](assets/thankyou.jpg)

捲動至ThankYouActivity檔案的結尾。 注釋`getRecommandations()`函式中的三行，並添加`targetLoadRequest()`函式的調用：

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

將此代碼行添加到`getRecommandations()`函式：

```java
targetLoadRequest(recommandation.recommandations);
```

現在，我們需要定義`targetLoadRequest()`函式：
![在感謝畫面上新增即時位置](assets/thankyou2.jpg)

在`filterRecommendationBasedOnOffer()`函式後面添加此代碼塊：

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, null, new Target.TargetCallback<String>() {
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
}
```

由於您剛剛將Target方法新增至ThankYouActivity，請務必匯入Target類別：

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### targetLoadRequest()代碼說明

| 程式碼 | 說明 |
|--- |--- |
| `targetLoadRequest()` | 使用者定義的函式（非SDK的一部分），會觸發`Target.loadRequest()`，載入並顯示wetravel_context_dest位置 |
| `Target.loadRequest()` | 向Target伺服器提出要求的SDK方法 |
| Constant.wetravel_context_dest | 在[!DNL Target]介面中建立活動時，我們稍後將使用的請求所指派的位置名稱 |
| `filterRecommendationBasedOnOffer()` | 應用程式中的使用者定義函式，從Target回應中擷取位置的選件，並決定應用程式應如何根據選件的內容而變更 |
| `recommandations.addAll()` | 應用程式中的使用者定義函式，在載入ThankYou畫面時預設會執行，但現在會在`filterRecommendationBasedOnOffer()`收到Target回應並剖析後執行 |

這是我們對應用程式進行的更複雜更新，然後在首頁畫面中加入要求，讓我們花點時間來回顧一下我們的工作：

1. 我們在注釋掉程式碼行後，中斷了應用程式先前顯示三個預設促銷活動的行為
1. 我們告訴應用程式執行新函式，並隨意命名targetLoadRequest
1. 我們定義了`targetLoadRequest`函式，使用Target.loadRequest方法向Target提出請求，並在收到[!DNL Target]選件回應時立即執行`filterRecommendationBasedOnOffer()`函式
1. `filterRecommendationBasedOnOffer()`函式會解譯回應並決定哪些促銷應套用至螢幕

在行動應用程式中使用[!DNL Target]時，這是非常常見的使用模式。  它不但功能強大，而且幾乎可以個人化行動應用程式的任何層面。 此外，還需要在應用程式程式碼和選件之間進行協調，我們稍後會在[!DNL Target]介面中定義選件。 由於這種協調，某些個人化使用案例可能會要求您更新應用程式商店中的應用程式，以啟動活動。

### 驗證即時請求

開啟Android模擬器並執行所有步驟來預訂行程：「首頁」>「匯流排搜索結果」>「座位選擇」、「付款選項」（任何含空白資料的付款選項都可用）。

在最後的「感謝」螢幕上，請觀看Logcat的回應。 回應應應為「Wetravel_context_dest」傳回預設內容：

![在「感謝」畫面上新增即時位置](assets/thankyou_validation.jpg)

## 從快取中清除預取位置

在作業階段中，可能需要清除預取位置。 例如，當發生預訂時，清除快取位置是有意義的，因為使用者現在已「參與」並瞭解預訂程式。 如果他們在作業期間預訂另一次行程，他們不需要主畫面和搜尋結果畫面上的原始位置來指導預訂。 從快取中清除位置，並預取新優惠，或許是折扣的第二次訂房或其他相關情形，將更有意義。 如果在作業階段期間發生預訂，可將邏輯新增至主畫面和搜尋結果畫面，以預取新位置。

在此範例中，我們將在預訂發生時，清除作業階段的預取位置。 這是透過呼叫`Target.clearPrefetchCache()`函式來完成。 在`targetLoadRequest()`函式內設定函式，如下所示：

```java
Target.clearPrefetchCache()
```

![從快取中清除預取位置](assets/clearPrefetch.jpg)

恭喜！ 您的應用程式現在已具備個人化的架構。 在下一課中，我們將透過新增參數至這些位置來增強個人化功能。

**[下一個：&quot;添加參數&quot; >](add-parameters.md)**
