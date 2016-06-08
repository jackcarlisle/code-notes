# 📓✏️ ️️code-notes
### A short list of code snippet _how-to's_

## How to: access _localhost_ on a mobile device when using a webpack dev server...

1. In your ```package.json``` file add a host and port to your webpack dev server script using the following flags:
```json
"dev:serve": "webpack-dev-server -d --config ./webpack.config.js  --host 0.0.0.0 --port 8080"
```

2. Next run your dev server command:  
```$ npm run dev:serve```

3. In a new terminal tab type the following command:  
```$ ifconfig```   

4. Copy the first 4 numbers after ```inet``` in the ```en0``` section from what gets printed in your terminal:
![ip](https://cloud.githubusercontent.com/assets/12450298/15893251/654a2090-2d76-11e6-9459-dffd28bed528.png)

5. Next go to a web browser on your mobile device _(make sure you are on the same network as your dev server)_. Replace where you would usually type ```localhost``` with the 4 numbers from your terminal:  
```js
http://localhost:8080/  
http://10.166.136.33:8080/
```
#### You should now be able to see your local site on your mobile device!
