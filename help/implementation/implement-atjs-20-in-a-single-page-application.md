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

最新版`at.js`提供豐富的功能集，讓您的企業能夠運用新一代的用戶端技術，進行個人化。 此新版本的重點是升級`at.js`，以與單頁應用程式(SPA)產生和諧的互動。

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## 如何在SPA中實作at.js 2.0

* 在單頁應用程式的&lt;head>中實作`at.js` 2.0。
* 每當SPA中的檢視變更時，都實作`adobe.target.triggerView()`函式。 可運用各種技術來執行此作業，例如監聽URL雜湊變更、監聽由SPA引發的自訂事件，或直接將`triggerView()`程式碼內嵌至應用程式。 您應選擇最適合您特定單一頁面應用程式的選項。
* 視圖名稱是`triggerView()`函式的第一個參數。 使用簡單、清楚且唯一的名稱，讓您在Target的視覺體驗撰寫器中輕鬆加以選取。
* 您可以在小檢視變更以及非SPA內容（例如向下半段無限捲動頁面）中觸發檢視。
* `at.js` 2.0，而且 `triggerView()` 可透過標籤管理解決方案（例如Adobe Experience Platform Launch）實作。

## at.js 2.0限制

升級前，請注意以下`at.js` 2.0限制：

* `at.js` 2.0不支援跨網域追蹤
* `at.js` 2.0不支援mboxOverride.browserIp和mboxSession URL參數
* `at.js` 2.0中不建議使用舊版函式mboxCreate、mboxDefine、mboxUpdate。將顯示預設內容，且不會發出網路請求。

## 影片中使用的程式庫頁尾代碼

在視訊期間，下列程式碼已新增至`at.js`程式庫的「程式庫頁尾」區段。 當應用程式第一次載入時，就會觸發此變數，然後會在應用程式中的任何雜湊變更時觸發。 它使用已清除的散列版本作為視圖名稱，當雜湊為空時使用&quot;home&quot;。 請注意，若要識別SPA，程式碼會在URL中尋找「react/」文字，這很可能需要在您的網站上更新。 請記住，您的SPA將`triggerView()`從自訂事件中觸發或直接將程式碼內嵌至應用程式中，可能更適合您。

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