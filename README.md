# fuckingfast-direct-link
paste on tampermonkey and enjoy it

```javascript
// ==UserScript==
// @name         Fuckingfast Direct Link
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  get direct link from fuckingfast
// @author       You
// @match        *://fuckingfast.co/*
// @grant        unsafeWindow
// ==/UserScript==

(function() {
    'use strict';

    window.addEventListener('load', function() {
        let dynamicDownloadURL = null;

        const scriptTags = document.querySelectorAll('script');
        scriptTags.forEach(scriptTag => {
            const scriptContent = scriptTag.innerHTML;

            const urlMatch = scriptContent.match(/"https:\/\/fuckingfast\.co\/dl[^"]+/);
            if (urlMatch) {
                dynamicDownloadURL = urlMatch[0].replace(/\\/g, '');
            }
        });

        if (dynamicDownloadURL) {
            console.log('Dynamic Download URL found:', dynamicDownloadURL);
        } else {
            console.log('Failed to scrape dynamic download URL.');
        }

        unsafeWindow.download = function() {
            window.open(dynamicDownloadURL.split("https://fuckingfast.co/")[1]);
        };
    });

})();
