## $${\color{red}Useful \ Bookmarklets \ Collection}$$

"A bookmarklet is a small, specialized software application—specifically a JavaScript snippet—stored as a URL within a standard web browser bookmark. When clicked, it executes code on the currently active webpage, allowing users to instantly modify page content, extract data, or automate tasks without installing browser extensions."

### Sounds useful to me!

---


 - QR code generator
   
```javascript
javascript:(function() {  var url = encodeURIComponent(window.location.href);  var qrCodeUrl = "https://api.qrserver.com/v1/create-qr-code/?data=" + url;  window.open(qrCodeUrl, "_blank");})();
```

- Page translator
  
```javascript
javascript:(function() {  var lang = prompt("Enter language code to translate to:", "en");  var translationUrl = "https://translate.google.com/translate?sl=auto&tl=" + lang + "&u=" + encodeURIComponent(window.location.href);  window.open(translationUrl, "_blank");})();
```

- Dark Mode

```javascript
javascript:(function() {  var style = document.createElement('style');  style.innerHTML = `    * {      color: white !important;      background-color: #111000 !important;    }  %60;  document.head.appendChild(style);})();
```

- Email copier

```
javascript:(function() {  const email = "you@example.com";  const dummyElement = document.createElement("textarea");  document.body.appendChild(dummyElement);  dummyElement.value = email;  dummyElement.select();  document.execCommand("copy");  document.body.removeChild(dummyElement);})();
```

- SEO checker

```javascript
javascript:(function() {  var pageUrl = window.location.href;  var tips = processDiagnosticData();  if (tips) {    alert('Page Diagnosis Tips:\n\n' + tips);  }  function processDiagnosticData() {    var tips = '';    var titleTag = document.querySelector('title');    if (!titleTag) {      tips += 'Title Tag is missing\n';    }    var metaDescriptionTag = document.querySelector('meta[name="description"]');    if (!metaDescriptionTag) {      tips += 'Meta Description is missing\n';    }    var headingTags = document.querySelectorAll('h1, h2, h3, h4, h5, h6');    if (headingTags.length === 0) {      tips += 'Heading Tags are missing\n';    }    var imgTags = document.querySelectorAll('img');    if (imgTags.length === 0) {      tips += 'Image Tags are missing\n';    }    var anchorTags = document.querySelectorAll('a');    if (anchorTags.length === 0) {      tips += 'Anchor Tags are missing\n';    }    var scriptTags = document.querySelectorAll('script');    if (scriptTags.length === 0) {      tips += 'Script Tags are missing\n';    }    var linkTags = document.querySelectorAll('link');    if (linkTags.length === 0) {      tips += 'Link Tags are missing\n';    }    var metaViewportTag = document.querySelector('meta[name="viewport"]');    if (!metaViewportTag) {      tips += 'Viewport Meta Tag is missing\n';    }    var canonicalTag = document.querySelector('link[rel="canonical"]');    if (!canonicalTag) {      tips += 'Canonical Tag is missing\n';    }    var robotsTag = document.querySelector('meta[name="robots"]');    if (!robotsTag) {      tips += 'Robots Meta Tag is missing\n';    }    var ogTags = document.querySelectorAll('meta[property^="og:"]');    if (ogTags.length === 0) {      tips += 'Open Graph Tags are missing\n';    }    var twitterTags = document.querySelectorAll('meta[name^="twitter:"]');    if (twitterTags.length === 0) {      tips += 'Twitter Card Tags are missing\n';    }    var altAttributes = document.querySelectorAll('img:not([alt])');    if (altAttributes.length > 0) {      tips += 'Alt Attributes are missing for some Images\n';    }    var formTags = document.querySelectorAll('form');    if (formTags.length === 0) {      tips += 'Form Tags are missing\n';    }    var inputTags = document.querySelectorAll('input');    if (inputTags.length === 0) {      tips += 'Input Tags are missing\n';    }    var textareaTags = document.querySelectorAll('textarea');    if (textareaTags.length === 0) {      tips += 'Textarea Tags are missing\n';    }    var buttonTags = document.querySelectorAll('button');    if (buttonTags.length === 0) {      tips += 'Button Tags are missing\n';    }    var tableTags = document.querySelectorAll('table');    if (tableTags.length === 0) {      tips += 'Table Tags are missing\n';    }    var metaCharsetTag = document.querySelector('meta[charset]');    if (!metaCharsetTag) {      tips += 'Charset Meta Tag is missing\n';    }    return tips;  }})();
```

- Page Elements Highlighter

```javascript
javascript:(function(){  function getRandomColor() {    var letters = "0123456789ABCDEF";    var color = "#";    for (var i = 0; i < 6; i++) {      color += letters[Math.floor(Math.random() * 16)];    }    return color;  }  function getContrastingColor(color) {    var hex = color.slice(1);    var r = parseInt(hex.substr(0, 2), 16);    var g = parseInt(hex.substr(2, 2), 16);    var b = parseInt(hex.substr(4, 2), 16);    var yiq = (r * 299 + g * 587 + b * 114) / 1000;    return yiq >= 128 ? "#000000" : "#FFFFFF";  }  function applyRandomStyle(element) {    var randomColor = getRandomColor();    element.style.backgroundColor = randomColor;    element.style.color = getContrastingColor(randomColor);  }  var elements = document.getElementsByTagName("*");  for (var i = 0; i < elements.length; i++) {    applyRandomStyle(elements[i]);  }})();
```

- JSON formatter

```javascript
javascript:(function() { function syntaxHighlight(json) { json = JSON.stringify(json, undefined, 4); json = json.replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;'); return json.replace(/("(\\u[a-zA-Z0-9]{4}|\\[^u]|[^\\"])*"(\s*:)?|\b(true|false|null)\b|-?\d+(?:\.\d*)?(?:[eE][+-]?\d+)?)/g, function (match) { var cls = %27color: black;%27; if (/^"/.test(match)) { if (/:$/.test(match)) { cls = %27color: green;%27; } else { cls = %27color: darkorange;%27; } } else if (/true|false/.test(match)) { cls = %27color: red;%27; } else if (/null|-?\d+(?:\.\d*)?(?:[eE][+-]?\d+)?/.test(match)) { cls = %27color: purple;%27; } return %27<span style="%27 + cls + %27">%27 + match + %27</span>%27; }); } var contentType = document.contentType; if (contentType === "application/json") { var json = JSON.parse(document.body.innerText); var highlighted = syntaxHighlight(json); document.body.innerHTML = %27<pre>%27 + highlighted + %27</pre>%27; document.body.style.fontFamily = "Arial, sans-serif"; document.body.style.fontSize = "15px"; } else { alert("This page does not contain JSON."); }}());
```

- Color Picker

```javascript
javascript:(function(){  var container = document.createElement('div');  container.style.position = 'fixed';  container.style.top = '10px';  container.style.right = '10px';  container.style.zIndex = '9999';  container.style.backgroundColor = 'white';  container.style.borderRadius = '10px';  container.style.padding = '10px';  container.style.boxShadow = '0 0 10px rgba(0, 0, 0, 0.3)';  container.style.display = 'flex';  container.style.alignItems = 'center';  var colorInput = document.createElement('input');  colorInput.type = 'color';  colorInput.style.width = '30px';  colorInput.style.height = '30px';  colorInput.style.marginRight = '10px';  var copyButton = document.createElement('button');  copyButton.textContent = 'Copy';  copyButton.style.padding = '5px 10px';  copyButton.style.marginRight = '10px';  copyButton.style.backgroundColor = '#4CAF50';  copyButton.style.color = 'white';  copyButton.style.border = 'none';  copyButton.style.borderRadius = '5px';  copyButton.style.cursor = 'pointer';  var closeButton = document.createElement('button');  closeButton.textContent = 'Close';  closeButton.style.padding = '5px 10px';  closeButton.style.backgroundColor = '#f44336';  closeButton.style.color = 'white';  closeButton.style.border = 'none';  closeButton.style.borderRadius = '5px';  closeButton.style.cursor = 'pointer';  copyButton.addEventListener('click', function() {    var color = colorInput.value;    var tempInput = document.createElement('input');    tempInput.value = color;    document.body.appendChild(tempInput);    tempInput.select();    document.execCommand('copy');    document.body.removeChild(tempInput);    alert('Color copied to clipboard: ' + color);  });  closeButton.addEventListener('click', function() {    container.remove();  });  container.appendChild(colorInput);  container.appendChild(copyButton);  container.appendChild(closeButton);  document.body.appendChild(container);})();
```

- Page SpeedInsight Test

```javascript
javascript:window.location='https://developers.google.com/speed/pagespeed/insights/?url=%27+encodeURI(window.location);
```

- Ad Blocker
  
```javascript
javascript:(function(){    /* Ad-B-Gone: Bookmarklet that removes obnoxious ads from pages */    var selectors = [    /* By ID: */    '#sidebar-wrap', '#advert', '#xrail', '#middle-article-advert-container',    '#sponsored-recommendations', '#around-the-web', '#sponsored-recommendations',    '#taboola-content', '#taboola-below-taboola-native-thumbnails', '#inarticle_wrapper_div',    '#rc-row-container', '#ads', '#at-share-dock', '#at4-share', '#at4-follow', '#right-ads-rail',    'div#ad-interstitial', 'div#advert-article', 'div#ac-lre-player-ph',    /* By Class: */    '.ad', '.avert', '.avert__wrapper', '.middle-banner-ad', '.advertisement',    '.GoogleActiveViewClass', '.advert', '.cns-ads-stage', '.teads-inread', '.ad-banner',    '.ad-anchored', '.js_shelf_ads', '.ad-slot', '.antenna', '.xrail-content',    '.advertisement__leaderboard', '.ad-leaderboard', '.trc_rbox_outer', '.ks-recommended',    '.article-da', 'div.sponsored-stories-component', 'div.addthis-smartlayers',    'div.article-adsponsor', 'div.signin-prompt', 'div.article-bumper', 'div.video-placeholder',    'div.top-ad-container', 'div.header-ad', 'div.ad-unit', 'div.demo-block', 'div.OUTBRAIN',    'div.ob-widget', 'div.nwsrm-wrapper', 'div.announcementBar', 'div.partner-resources-block',    'div.arrow-down', 'div.m-ad', 'div.story-interrupt', 'div.taboola-recommended',    'div.ad-cluster-container', 'div.ctx-sidebar', 'div.incognito-modal', '.OUTBRAIN', '.subscribe-button',    '.ads9', '.leaderboards', '.GoogleActiveViewElement', '.mpu-container', '.ad-300x600', '.tf-ad-block',    '.sidebar-ads-holder-top', '.ads-one', '.FullPageModal__scroller',    '.content-ads-holder', '.widget-area', '.social-buttons', '.ac-player-ph',    /* Other: */    'script', 'iframe', 'video', 'aside#sponsored-recommendations', 'aside[role="banner"]', 'aside',    'amp-ad', 'span[id^=ad_is_]', 'div[class*="indianapolis-optin"]', 'div[id^=google_ads_iframe]',    'div[data-google-query-id]', 'section[data-response]', 'ins.adsbygoogle', 'div[data-google-query-id]',    'div[data-test-id="fullPageSignupModal"]', 'div[data-test-id="giftWrap"]' ];    for(let i in selectors) {        let nodesList = document.querySelectorAll(selectors[i]);        for(let i = 0; i < nodesList.length; i++) {            let el = nodesList[i];            if(el && el.parentNode)                el.parentNode.removeChild(el);        }    }})();
```

- Page Technology Checker

```javascript
javascript:(function() {  var currentSite = window.location.hostname;  var redirectUrl = "https://w3techs.com/sites/info/" + currentSite;  window.location.href = redirectUrl; })();
```

- Clear Tab Cache

```javascript
javascript:(function(){  localStorage.clear();  sessionStorage.clear();  alert('Cache cleared!');})();
```

- Tiny URL maker

```javascript
void(open('http://tinyurl.com/create.php?url=%27+encodeURIComponent(location.href)))
```
javascript:(function(){  localStorage.clear();  sessionStorage.clear();  alert('Cache cleared!');})();
```
