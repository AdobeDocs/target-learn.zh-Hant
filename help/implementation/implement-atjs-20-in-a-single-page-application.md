---
title: 如何在單頁應用程式中實作at.js 2.0(SPA)
description: Adobe Target的at.js 2.0提供豐富的功能集，讓您的企業能夠運用新一代的用戶端技術，進行個人化。 請依照下列步驟，在單頁應用程式(SPA)中實作at.js 2.0。
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# 在單頁應用程式中實作Adobe Target的at.js 2.0(SPA)

Adobe Target的`at.js` 2.0提供豐富的功能集，讓您的企業能夠在下一代的用戶端技術上執行個人化。 此版本的重點是升級`at.js`，以與單頁應用程式(SPA)產生協調的互動。

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## 如何在SPA

* 在單頁應用程式的&lt;head>中實作`at.js` 2.0。
* 每當檢視變更時，實作`adobe.target.triggerView()`函SPA數。 可運用各種技術來執行此作業，例如監聽URL雜湊變更、監聽您引發的自訂事件SPA，或直接將`triggerView()`程式碼內嵌至您的應用程式。 您應選擇最適合您特定單一頁面應用程式的選項。
* 視圖名稱是`triggerView()`函式的第一個參數。 使用簡單、清楚且唯一的名稱，讓您在Target的視覺體驗撰寫器中輕鬆加以選取。
* 您可以在小檢視變更中以及非上下文(例SPA如向下半向無限捲動頁面)中觸發檢視。
* `at.js` 2.0，並可 `triggerView()` 透過標籤管理解決方案(例如Adobe Experience Platform Launch)實作。

## at.js 2.0限制

升級前，請注意以下`at.js` 2.0限制：

* `at.js` 2.0不支援跨網域追蹤
* `at.js` 2.0不支援mboxOverride.browserIp和mboxSession URL參數
* `at.js` 2.0中不建議使用舊版函式mboxCreate、mboxDefine、mboxUpdate。將顯示預設內容，且不會發出網路請求。

## 影片中使用的程式庫頁尾代碼

在視訊期間，下列程式碼已新增至`at.js`程式庫的「程式庫頁尾」區段。 當應用程式第一次載入時，就會觸發此變數，然後會在應用程式中的任何雜湊變更時觸發。 它使用已清除的散列版本作為視圖名稱，當雜湊為空時使用&quot;home&quot;。 請注意，若要識SPA別，程式碼會在URL中尋找「react/」文字，這很可能需要在您的網站上更新。 請同時記住，將`triggerView()`從自訂事件SPA中觸發，或直接將程式碼內嵌至您的應用程式，可能更適合您。

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
* [使用Adobe Target的Visual Experience Composer進行單頁應用程SPA式(VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [從at.js 1.x升級至at.js 2.0檔案](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/upgrading-from-atjs-1x-to-atjs-20.html)