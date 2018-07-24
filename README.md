# node-red-heroku-with-eps

This is a wrapper for deploying [Node-RED](http://nodered.org) with ["Einstein Platform Services" node](https://github.com/hinabasfdc/node-red-contrib-atelierhi-eps) into the [Heroku](https://www.heroku.com).

### Deploying Node-RED with "Einstein Platform Serviecs" node into Heroku

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/hinabasfdc/node-red-heroku-with-eps)

### Password protect the flow editor

By default, the editor is open for anyone to access and modify flows. To password-protect the editor:

Add the following user-defined variables.

* NODE_RED_USERNAME - the username to secure the editor with
* NODE_RED_PASSWORD - the password to secure the editor with

### About Einstein Platform Services
* "Einstein Platform Services" is an artificial inteligence API service provided by Salesforce. [https://einstein.ai](https://einstein.ai)
* If you use the "Deploy to Heroku" button, a free trial license (2,000 prediction api call/month) will be deployed automaticaly. Otherwise, you need to manually get and set for account id & private key of the Einstein Platform Services. 

## Sample flows
* Copy the source code first, and then paste it to a dialog (Menu -> Import -> Clipboard)
### API Usage
```
[{"id":"8156ca79.2e39c8","type":"inject","z":"9e5132fc.eebbf8","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":120,"y":40,"wires":[["11aefea2.95b611"]]},{"id":"11aefea2.95b611","type":"function","z":"9e5132fc.eebbf8","name":"Test Api Usage","func":"msg.eps = {};\nmsg.eps.feature = \"APIUSAGE\";\nreturn msg;","outputs":1,"noerr":0,"x":300,"y":40,"wires":[["15dcbb75.568015"]]},{"id":"15dcbb75.568015","type":"Einstein-Platform-Services","z":"9e5132fc.eebbf8","name":"Einstein Platform Services","request_url":"https://api.einstein.ai/v2/","default_feature":"IMAGECLASSIFICATION","default_modelid":"GeneralImageClassifier","account_id":"","private_key":"","x":530,"y":40,"wires":[["77d181c5.34e3e"]]},{"id":"77d181c5.34e3e","type":"debug","z":"9e5132fc.eebbf8","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","x":750,"y":40,"wires":[]}]
```
### Image Classification (URL)
```
[{"id":"cc97620c.f03ec","type":"inject","z":"5a87ee21.d2cf48","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":120,"y":60,"wires":[["85ec7c33.3b95b"]]},{"id":"85ec7c33.3b95b","type":"function","z":"5a87ee21.d2cf48","name":"Test Image Classification","func":"msg.eps = {};\nmsg.eps.feature = \"IMAGECLASSIFICATION\"\nmsg.eps.sampleLocation = \"https://upload.wikimedia.org/wikipedia/commons/d/d3/Supreme_pizza.jpg\";\nmsg.eps.modelid = \"FoodImageClassifier\";\nreturn msg;","outputs":1,"noerr":0,"x":330,"y":60,"wires":[["c82b5a83.de5a8"]]},{"id":"c82b5a83.de5a8","type":"Einstein-Platform-Services","z":"5a87ee21.d2cf48","name":"Einstein Platform Services","request_url":"https://api.einstein.ai/v2/","default_feature":"IMAGECLASSIFICATION","default_modelid":"GeneralImageClassifier","account_id":"","private_key":"","x":590,"y":60,"wires":[["db94f4c9.259b2"]]},{"id":"db94f4c9.259b2","type":"debug","z":"5a87ee21.d2cf48","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","x":810,"y":60,"wires":[]}]
```
### Image Recognition (base64string from an image file)
```
[{"id":"a2ca3912.0e48a8","type":"http in","z":"c6c23f52.370f48","name":"","url":"/eps_imagerecognition","method":"get","upload":false,"swaggerDoc":"","x":140,"y":40,"wires":[["84a0bd4a.816de8"]]},{"id":"84a0bd4a.816de8","type":"template","z":"c6c23f52.370f48","name":"","field":"payload","fieldType":"msg","format":"html","syntax":"mustache","template":"<html>\n    <head>\n        <title>Einstein Vision with Node-RED</title>\n    </head>\n    <body>\n        <h1>Einstein Vision with Node-RED</h1>\n        <h2>Select an image file</h2>\n        <form  action=\"/eps_imagerecognition\" method=\"post\" enctype=\"multipart/form-data\">\n            <input type=\"file\" name=\"imagedata\" accept=\"image/*\" />\n            <input type=\"submit\" value=\"Predict\"/>\n        </form>\n    </body>\n</html>","output":"str","x":363,"y":40,"wires":[["6a99c807.21c59"]]},{"id":"6a99c807.21c59","type":"http response","z":"c6c23f52.370f48","name":"","statusCode":"","headers":{},"x":510,"y":40,"wires":[]},{"id":"d656ee3.21bef1","type":"Einstein-Platform-Services","z":"c6c23f52.370f48","name":"Einstein Platform Services","request_url":"https://api.einstein.ai/v2/","default_feature":"IMAGECLASSIFICATION","default_modelid":"GeneralImageClassifier","account_id":"","private_key":"","x":650,"y":100,"wires":[["3c9725bb.8d917a"]]},{"id":"29d4c3ce.d38774","type":"http in","z":"c6c23f52.370f48","name":"","url":"/eps_imagerecognition","method":"post","upload":true,"swaggerDoc":"","x":140,"y":100,"wires":[["8e291330.a488e"]]},{"id":"8e291330.a488e","type":"function","z":"c6c23f52.370f48","name":"File to base64 string","func":"msg.eps = {};\nmsg.eps.sampleBase64Content = msg.req.files[0].buffer.toString('base64');\nreturn msg;","outputs":1,"noerr":0,"x":400,"y":100,"wires":[["d656ee3.21bef1"]]},{"id":"3c9725bb.8d917a","type":"http response","z":"c6c23f52.370f48","name":"","statusCode":"","headers":{},"x":850,"y":100,"wires":[]}]
```
### Text Sentiment
```
[{"id":"3a9a9d76.447baa","type":"inject","z":"fc91f63f.f4e028","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":100,"y":40,"wires":[["1ed9b0b7.dead67"]]},{"id":"1ed9b0b7.dead67","type":"function","z":"fc91f63f.f4e028","name":"Test Sentiment","func":"msg.eps = {};\nmsg.eps.feature = \"SENTIMENT\"\nmsg.eps.document = \"the presentation was great and i learned a lot\";\nmsg.eps.modelid = \"CommunitySentiment\";\nreturn msg;","outputs":1,"noerr":0,"x":280,"y":40,"wires":[["b1fa2436.1c2bc"]]},{"id":"b1fa2436.1c2bc","type":"Einstein-Platform-Services","z":"fc91f63f.f4e028","name":"Einstein Platform Services","request_url":"https://api.einstein.ai/v2/","default_feature":"IMAGECLASSIFICATION","default_modelid":"GeneralImageClassifier","account_id":"","private_key":"","x":510,"y":40,"wires":[["da447020.eeedd8"]]},{"id":"da447020.eeedd8","type":"debug","z":"fc91f63f.f4e028","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","x":730,"y":40,"wires":[]}]
```