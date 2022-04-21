---
title: Guidelines
description: 
published: true
date: 2022-04-21T11:11:16.934Z
tags: 
editor: markdown
dateCreated: 2022-04-18T12:11:51.610Z
---

## **Types**

See this [document](https://devexpress.sharepoint.com/:w:/s/devextreme/EY6mFj_sHM1FlmzKnsk9CtABH_WpvZm2g6_ub0pHQxCAYw?e=PbpjQQ)

## **How to work with public repo and build up the site locally**

All info is described in our [guide](https://devexpress.sharepoint.com/:w:/s/devextreme/EZXnoPoMzkBLg5iL9VAONd4BJkOlG6FEXAuYOqa8JshDQQ?e=tNFZMl). Feel free to contribute to it if you find that any information is obsolete/need to be corrected

Staging is available at [http://jsserver:8080](http://jsserver:8080/)

## **Localization**

We provide localized messages in four [languages](https://github.com/DevExpress/DevExtreme/blob/21_1/js/localization/messages/en.json):

\- Russian (developer responsibility)  
\- English (developer and techwriter responsibility)  
\- German (ask Oli Sturm)  
\- Japanese (ask Albert Totten)

**Note**

*All english texts should be reviewed by Ray (remind your technical writer to submit the text for review)*

For other locales it's good to add a placeholder for a new contant. And when publishing the release, ask the maintainers to update the new constants.

You can use localization strings for German and Japanese from trusted sources (e.g. [Microsoft Language Portal](https://www.microsoft.com/en-us/language/Search?&searchTerm=Subscript&langID=354&Source=true&productid=0)). Just don't forget to ask Oliver and Albert to check the added lines before release. We usually create a table (e.g. [21.1](https://devexpress-my.sharepoint.com/:x:/p/dmitry_levkovskiy/ESX_dZjdJDROsJv7HIk2d7gBkcY82a91GcGaVyi96qfjLQ?e=PH8Eq3) ) in which we list the constants and their meaning for supported languages. It is not superfluous to add a note (in English and / or a small screenshot) about the context of using this text

## **Styles**

### **19.2 changes**

В ветке 19\_2 мы начали использовать gulp-less для билдежки стилей, поэтому в Less можно использовать полноценные @import.

`gulp dev, gulp style-compiler-themes-dev` таски теперь генерят по умолчанию только dx.common.css, dx.light.css, dx.material.blue.light.css. Вторая таска прозрачно используется в QUnit тестах, которые вообще используют только common и light.

Если нужно поотлаживать другую тему, можно запустить gulp dev с параметром --bundles. Имена бандлов соответствуют файлам в папках styles/bundles или artifacts/css без 'dx.' и расширения, указываются через запятую.

Например,

\`gulp dev --bundles=common,dark,material.blue.dark\`

## **Accessibility**

### **Tools**

**1\. Readers**

\- NVDA ([https://www.nvaccess.org/download/)​](https://www.nvaccess.org/download/)%E2%80%8B)​  
\- JAWS ([https://support.freedomscientific.com/Downloads/JAWS)​](https://support.freedomscientific.com/Downloads/JAWS)%E2%80%8B)

**2\. Validators**

\- Accesibility insight ([https://chrome.google.com/webstore/detail/accessibility-insights-fo/pbjjkligggfmakdaogkfomddhfmpjeni?hl=en)​](https://chrome.google.com/webstore/detail/accessibility-insights-fo/pbjjkligggfmakdaogkfomddhfmpjeni?hl=en)%E2%80%8B)  
​- Axe ([https://chrome.google.com/webstore/detail/axe-web-accessibility-tes/lhdoppojpmngadmnindnejefpokejbdd/related)​](https://chrome.google.com/webstore/detail/axe-web-accessibility-tes/lhdoppojpmngadmnindnejefpokejbdd/related)%E2%80%8B)  
\- Wave ([https://chrome.google.com/webstore/detail/wave-evaluation-tool/jbbplnpkjmmeebjpijfedlgcdilocofh)​](https://chrome.google.com/webstore/detail/wave-evaluation-tool/jbbplnpkjmmeebjpijfedlgcdilocofh)%E2%80%8B)  
\- Color Contrast Analyzer ([https://chrome.google.com/webstore/detail/color-contrast-analyzer/dagdlcijhfbmgkjokkjicnnfimlebcll)​](https://chrome.google.com/webstore/detail/color-contrast-analyzer/dagdlcijhfbmgkjokkjicnnfimlebcll)%E2%80%8B)

### **Guidelines, examples**

\- Accessibility Developer guide (created by ASP.NET team) - [https://docs.google.com/document/d/1qExVmxgGnrmJO0uHagyc-dW0pgPO-ET\_aaBW\_rA\_1nA/edit#heading=h.yfojcdkzio0o](https://docs.google.com/document/d/1qExVmxgGnrmJO0uHagyc-dW0pgPO-ET_aaBW_rA_1nA/edit#heading=h.yfojcdkzio0o)

\- DevExtreme Accessibility Template - [https://devexpress-my.sharepoint.com/:x:/p/victor\_shchelkunov/EekeY-O2xZJGgFO1Vbe\_srkBWwUjlhg\_5A3pihVAaVXaxg?rtime=z09D7IzG2Eg](https://devexpress-my.sharepoint.com/:x:/p/victor_shchelkunov/EekeY-O2xZJGgFO1Vbe_srkBWwUjlhg_5A3pihVAaVXaxg?rtime=z09D7IzG2Eg)

\- ASP.NET Accessibility Template - [https://devexpress-my.sharepoint.com/:x:/p/anna\_kondratova/EehwQMYe3RFDuiZeZXx5GJMBZMakFzCoQ8AP0V5Q1ft8TQ?e=qeDTOp](https://devexpress-my.sharepoint.com/:x:/p/anna_kondratova/EehwQMYe3RFDuiZeZXx5GJMBZMakFzCoQ8AP0V5Q1ft8TQ?e=qeDTOp)

\- WPF Accessibility Template - [https://devexpress.sharepoint.com/:w:/s/XPFSupport/EQxo0ETJH9FFg-kMepdcp-oBJ3o7FmwxZ0-a3c0y1LPg\_w?e=nZ8wJm](https://devexpress.sharepoint.com/:w:/s/XPFSupport/EQxo0ETJH9FFg-kMepdcp-oBJ3o7FmwxZ0-a3c0y1LPg_w?e=nZ8wJm)

Best Practices - [https://www.w3.org/TR/wai-aria-practices-1.1/](https://www.w3.org/TR/wai-aria-practices-1.1/)

### **Documentation**

\- WCAG 2.1 - [https://www.w3.org/TR/WCAG21/](https://www.w3.org/TR/WCAG21/)

\- Section 508 - [https://www.access-board.gov/ict/#301-general](https://www.access-board.gov/ict/#301-general)

\- EN 301 549 v3.1.1 (2019-11) - [www.etsi.org/deliver/etsi\_en/301500\_301599/301549/03.01.01\_60/en\_301549v030101p.pdf](https://www.etsi.org/deliver/etsi_en/301500_301599/301549/03.01.01_60/en_301549v030101p.pdf)

### **Video explanation (Q & A)**

[Link to video](https://devexpress.sharepoint.com/sites/devextreme/Shared%20Documents/General/Recordings/Meeting%20in%20_General_-20210205_130116-Meeting%20Recording.mp4?web=1)

Please note that accessibility is composed of several factors:

\- visual design \[e.g. contrasting themes, color blindness mode\]  
\- layout (ARIA attributes for screen readers)  
\- logical and usual keyboard navigation:

    - hot keys work as expected;

    - focus does not disappear in the process of work;

    - it is convenient to work with the application using one manipulator (keyboard only)

## **Our widgets API**

Widget and its descendants has the `setAria` method.

**setAria(AriaAttribute, AttributeValue)** => set the aria attibute with the AttributeValue value to the widget’s ARIA target element (by \`\_getAriaTarget\` method).

E.g. this.setAria(‘checked’, true) => <div aria-checked=”true” />

**setAria(AriaAttribute, AttributeValue, TargetElement)** => set the aria attribute with the AttributeValue value to the TargetElement.

E.g. widget.setAria('describedby', 'mytext', $innerButton) =>

    *<label id="mytext">Awesome button</label>*

    *<widget role="qwerty"><button aria-describedby="mytext" /></widget>*

  
**Note:** *id* and *role* attributes does not have the \`aria-\` prefix  
**Note:** to remove attribute - set the \`null\` value: *this.setAria(‘role’, null)*

**\_getAriaTarget()** => returns an element on which ARIA attributes should be applied by default. By default matches the focus element (this.\_focusTarget())

## **How to check widgets?**

Try screen readers - [NVDA](https://www.nvaccess.org/download/) or [JAWS](https://www.freedomscientific.com/products/software/jaws/) \[during development, we focused on using NVDA as a recommended screen reader\]  
Accessibility scanners - [Accessibility Insight](https://chrome.google.com/webstore/detail/accessibility-insights-fo/pbjjkligggfmakdaogkfomddhfmpjeni?hl=en) chrome extension, Lighthouse Audits panel in Chrome DevTools or [axe](https://chrome.google.com/webstore/detail/axe-web-accessibility-tes/lhdoppojpmngadmnindnejefpokejbdd) \[Be ready to deal with false positive results. The scanners are checking the entire page. Problems can be detected not only because of widget layout errors, but also because the page layout errors.\]