---
title: 在單頁應用程式(SPA)中實作Adobe Target的at.js 2.0
seo-title: 在單頁應用程式(SPA)中實作Adobe Target的at.js 2.0
description: 最新版 at.js 提供豐富的功能，讓貴公司能以新世代用戶端技術為基礎進行個人化。本次的新版本著重於升級 at.js，進而與單一頁面應用程式 (SPA) 產生和諧互動。
audience: developer
difficulty: 3
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 8%

---


# 在單頁應用程式(SPA)中實作Adobe Target的at.js 2.0

The newest version of `at.js` provides rich feature sets that equip your business to execute personalization on next-generation, client-side technologies. This new version is focused on upgrading `at.js` to have harmonious interactions with single page applications (SPAs).

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## 如何在SPA中實作at.js 2.0

* 在 `at.js` 單頁應用程式的&lt;head>中實作2.0。
* 在SPA中 `adobe.target.triggerView()` 檢視變更時實作函式。 可運用各種技術來執行此作業，例如監聽URL雜湊變更、監聽由SPA引發的自訂事件，或直接將程式碼內嵌 `triggerView()` 在您的應用程式中。 您應選擇最適合您特定單一頁面應用程式的選項。
* 視圖名稱是函式的第一個參 `triggerView()` 數。 使用簡單、清楚且唯一的名稱，讓您在Target的視覺體驗撰寫器中輕鬆加以選取。
* 您可以在小檢視變更以及非SPA內容（例如向下半段無限捲動頁面）中觸發檢視。
* `at.js` 2.0和 `triggerView()` 可透過標籤管理解決方案實作，例如Adobe Experience Platform Launch。

## at.js 2.0限制

升級前，請注意下列 `at.js` 2.0限制：

* 2.0不支援跨網域 `at.js` 追蹤
* mboxOverride.browserIp和mboxSession URL參數在 `at.js` 2.0中不受支援
* 舊有函式mboxCreate、mboxDefine、mboxUpdate在 `at.js` 2.0中已過時。 將顯示預設內容，且不會發出網路請求。

## 影片中使用的程式庫頁尾代碼

在視訊期間，程式庫的「程式庫頁尾」區 `at.js` 段已新增下列程式碼。 當應用程式第一次載入時，就會觸發此變數，然後會在應用程式中的任何雜湊變更時觸發。 它使用已清除的散列版本作為視圖名稱，當雜湊為空時使用&quot;home&quot;。 請注意，若要識別SPA，程式碼會在URL中尋找「react/」文字，這很可能需要在您的網站上更新。 請記住，您的SPA可能更適合從自訂事件中 `triggerView()` 觸發，或直接將程式碼內嵌至應用程式。

```javascript
function sanitizeViewName(viewName) {
  if (viewName.startsWith('#')) {
    viewName = viewName.substr(1);
  }
  if (viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }
  return viewName;
}
function triggerView(viewName) {
  viewName = sanitizeViewName(viewName) || 'home';
  // Validate if the Target Libraries are available on your website
  if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
    adobe.target.triggerView(viewName);
    console.log('AT: View triggered on page load: '+viewName)
  }
}
//fire triggerView when the SPA loads and when the hash changes in the SPA
if(window.location.pathname.indexOf('react/') >-1){
    triggerView(location.hash);
}
window.onhashchange = function() {
    if(window.location.pathname.indexOf('react/') >-1){
        triggerView(location.hash);
    }
}
```

## 其他資源

* [瞭解at.js 2.0的運作方式（架構圖）](understanding-how-atjs-20-works.md)
* [使用Adobe Target的Visual Experience Composer進行單頁應用程式(SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [從at.js 1.x升級至at.js 2.0檔案](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/upgrading-from-atjs-1x-to-atjs-20.html)