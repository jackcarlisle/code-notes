# 📓✏️ ️️code-notes
### A short list of random code snippet _how-to's_:

## How to: access _localhost_ on a mobile device when using a webpack dev server...

1. In your ```package.json``` file add a host and port to your webpack dev server script using the following flags:
```json
"dev:serve": "webpack-dev-server -d --config ./webpack.config.js  --host 0.0.0.0 --port 8080"
```

2. Next run your dev server command:  
```$ npm run dev:serve```

3. In a new terminal tab type the following command:  
```$ ifconfig | grep inet```   

4. Copy the following 4 numbers after ```inet``` from what gets printed in your terminal (this is your IP address for your localhost):
![ip](https://cloud.githubusercontent.com/assets/12450298/16200515/95cea400-3705-11e6-8e26-19e3619500de.png)

5. Next go to a web browser on your mobile device _(make sure you are on the same network as your dev server)_. Replace where you would usually type ```localhost``` with the 4 numbers from your terminal:  
```js
http://localhost:8080/  
http://10.166.136.78:8080/
```
#### You should now be able to see your local site on your mobile device!


## How to: detect which browser a user is using...

Usually you would check the User agent string but this can be unreliable because it can be spoofed easily. A more reliable way to detect the browser is to check whether it has features specific to that platform:

```js
// Opera 8.0+
var isOpera = (!!window.opr && !!opr.addons) || !!window.opera || navigator.userAgent.indexOf(' OPR/') >= 0;
// Firefox 1.0+
var isFirefox = typeof InstallTrigger !== 'undefined';
// At least Safari 3+: "[object HTMLElementConstructor]"
var isSafari = Object.prototype.toString.call(window.HTMLElement).indexOf('Constructor') > 0;
// Internet Explorer 6-11
var isIE = /*@cc_on!@*/false || !!document.documentMode;
// Edge 20+
var isEdge = !isIE && !!window.StyleMedia;
// Chrome 1+
var isChrome = !!window.chrome && !!window.chrome.webstore;
// Blink engine detection
var isBlink = (isChrome || isOpera) && !!window.CSS;
```
