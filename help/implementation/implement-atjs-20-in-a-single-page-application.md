---
title: 如何在單頁應用程式(SPA)中實作at.js 2.0
description: Adobe Target的at.js 2.0提供豐富的功能，讓貴公司能以新世代使用者端技術為基礎進行個人化。 請依照下列步驟，在單頁應用程式(SPA)中實作at.js 2.0。
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
source-wordcount: '399'
ht-degree: 0%

---

# 在單頁應用程式(SPA)中實作Adobe Target的at.js 2.0

Adobe Target的 `at.js` 2.0提供豐富的功能，讓貴公司能以新世代使用者端技術為基礎進行個人化。 此版本著重於升級 `at.js` 與單頁應用程式(SPA)產生和諧互動。

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## 如何在SPA中實作at.js 2.0

* 實作 `at.js` 2.0於 &lt;head> 單頁應用程式的URL編號。
* 實作 `adobe.target.triggerView()` 函式(每當在SPA中檢視變更時)。 您可以運用各種技術來達成此目的，例如接聽URL雜湊變更、接聽SPA觸發的自訂事件，或內嵌 `triggerView()` 程式碼直接輸入您的應用程式中。 您應該選擇最適合您的特定單頁應用程式的選項。
* 檢視名稱是 `triggerView()` 函式。 使用簡單、清晰且唯一的名稱，讓在Target的視覺化體驗撰寫器中選取這些名稱更容易。
* 您可以在較小的檢視變更中以及在非SPA內容中觸發檢視，例如向下一個無限捲動頁面的一半。
* `at.js` 2.0和 `triggerView()` 可透過Adobe Experience Platform Launch等標籤管理解決方案實作。

## at.js 2.0限制

請留意以下限制 `at.js` 2.0升級前：

* 不支援跨網域追蹤 `at.js` 2.0
* 不支援mboxOverride.browserIp和mboxSession URL引數 `at.js` 2.0
* 舊版函式mboxCreate、mboxDefine、mboxUpdate在中已過時 `at.js` 2.0.將顯示預設內容，且不會提出網路要求。

## 視訊中使用的資料庫頁尾程式碼

下列程式碼已新增至的「資料庫頁尾」區段 `at.js` 程式庫在影片播放期間。 它會在應用程式首次載入，然後在應用程式中的任何雜湊變更時引發。 它會使用雜湊的清理版本作為檢視名稱，並在雜湊為空時使用「home」。 請注意，為了識別SPA，程式碼會在URL中尋找「react/」文字，這極可能需要在您的網站上更新。 也請記住，您的SPA可能更適合觸發 `triggerView()` 關閉自訂事件，或直接將程式碼內嵌至您的應用程式中。

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
* [使用適用於單頁應用程式的Adobe Target Visual Experience Composer (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
