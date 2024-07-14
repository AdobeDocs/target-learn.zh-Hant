---
title: 如何在單頁應用程式(SPA)中實作at.js 2.0
description: Adobe Target的at.js 2.0提供豐富的功能組合，讓貴公司能以新世代使用者端技術為基礎進行個人化。 請依照下列步驟，在單頁應用程式(SPA)中實作at.js 2.0。
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 在單頁應用程式(SPA)中實作Adobe Target的at.js 2.0

Adobe Target的`at.js` 2.0提供豐富的功能組合，讓貴公司能以新世代使用者端技術為基礎進行個人化。 此版本著重於升級`at.js`，以便與單頁應用程式(SPA)產生和諧互動。

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## 如何在SPA中實作at.js 2.0

* 在單頁應用程式的&lt;head>中實作`at.js` 2.0。
* 每次在您的SPA中檢視變更時實作`adobe.target.triggerView()`函式。 您可以運用各種技術來達成此目的，例如接聽URL雜湊變更、接聽SPA觸發的自訂事件，或將`triggerView()`程式碼直接內嵌至您的應用程式。 您應該選擇最適合您特定單頁應用程式的選項。
* 檢視名稱是`triggerView()`函式的第一個引數。 使用簡單、清楚且唯一的名稱，以便在Target的視覺化體驗撰寫器中輕鬆選取。
* 您可以在小型檢視變更以及非SPA內容（例如無限捲動頁面的一半）中觸發檢視。
* `at.js` 2.0和`triggerView()`可透過標籤管理解決方案(例如Adobe Experience Platform Launch)實作。

## at.js 2.0限制

升級前，請注意下列`at.js` 2.0的限制：

* `at.js` 2.0不支援跨網域追蹤
* `at.js` 2.0不支援mboxOverride.browserIp和mboxSession URL引數
* 舊版函式mboxCreate、mboxDefine、mboxUpdate在`at.js` 2.0中已過時。將顯示預設內容，且不會提出網路要求。

## 視訊中使用的資料庫頁尾程式碼

下列程式碼已在視訊期間新增至`at.js`資料庫的「資料庫頁尾」區段。 它會於應用程式先載入，接著在應用程式中的任何雜湊變更時引發。 它會使用雜湊的清理版本當作檢視名稱，並在雜湊為空時使用「home」。 請注意，為了識別SPA，程式碼會在URL中尋找「react/」文字，這很可能需要在您的網站上更新。 也請記住，您的SPA從自訂事件引發`triggerView()`或直接將程式碼內嵌到您的應用程式中可能更合適。

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

* [瞭解at.js 2.0的運作方式（架構圖表）](understanding-how-atjs-20-works.md)
* [使用適用於單頁應用程式的Adobe Target Visual Experience Composer (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
