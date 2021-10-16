---
title: 如何在單頁應用程式中實作at.js 2.0(SPA)
description: Adobe Target的at.js 2.0提供豐富的功能組合，讓貴公司能以新世代用戶端技術為基礎進行個人化。 請依照下列步驟，在單頁應用程式(SPA)中實作at.js 2.0。
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# 在單頁應用程式中實作Adobe Target的at.js 2.0(SPA)

Adobe Target的`at.js` 2.0提供豐富的功能組合，讓貴公司能以新世代用戶端技術為基礎進行個人化。 此版本著重於升級`at.js`以與單頁應用程式(SPA)產生和諧互動。

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## 如何在SPA中實作at.js 2.0

* 在單頁應用程式的&lt;head>中實作`at.js` 2.0。
* 每當SPA中的檢視變更時，實作`adobe.target.triggerView()`函式。 可採用各種技術來執行此作業，例如監聽URL雜湊變更、監聽SPA引發的自訂事件，或直接將`triggerView()`程式碼嵌入您的應用程式。 您應選擇最適合特定單頁應用程式的選項。
* 視圖名稱是`triggerView()`函式的第一個參數。 使用簡單、清除和唯一的名稱，以便在Target的可視化體驗撰寫器中輕鬆選取。
* 您可以在小型檢視變更以及非SPA內容（例如向下半向無限捲動頁面）中觸發檢視。
* `at.js` 2.0和 `triggerView()` 可透過標籤管理解決方案(例如Adobe Experience Platform Launch)來實作。

## at.js 2.0限制

升級前，請注意`at.js` 2.0的下列限制：

* `at.js` 2.0不支援跨網域追蹤
* `at.js` 2.0不支援mboxOverride.browserIp和mboxSession URL參數
* `at.js` 2.0中不再使用舊版函式mboxCreate、mboxDefine、mboxUpdate。將顯示預設內容，且不會提出網路要求。

## 影片中使用的程式庫頁尾程式碼

影片期間，下列程式碼已新增至`at.js`程式庫的「程式庫頁尾」區段。 應用程式首次載入時就會引發，而應用程式中的任何雜湊變更則會隨即引發。 它會使用雜湊的清理版本作為檢視名稱，並在雜湊為空時使用「home」。 請注意，若要識別SPA，程式碼會在URL中尋找文字「react/」，而這很可能需要在您的網站上更新。 也請記住，SPA可能更適合從自訂事件或直接將程式碼內嵌至應用程式中，來引發`triggerView()`。

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

* [了解at.js 2.0的運作方式（架構圖表）](understanding-how-atjs-20-works.md)
* [針對單頁應用程式(SPA VEC)使用Adobe Target的可視化體驗撰寫器](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [從at.js 1.x升級至at.js 2.0檔案](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/upgrading-from-atjs-1x-to-atjs-20.html?lang=en)
