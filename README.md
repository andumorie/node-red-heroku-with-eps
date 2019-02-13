# node-red-heroku-with-orchestrator

This is a wrapper for deploying [Node-RED](http://nodered.org) with ["UiPath Orchestrator" node](https://www.npmjs.com/package/@uipath/node-red-contrib-uipath-orchestrator) into [Heroku](https://www.heroku.com).

### Deploying Node-RED with UiPath Orchestrator node into Heroku

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/andumorie/node-red-heroku-with-orchestrator)

### Password protect the flow editor

By default, the editor is open for anyone to access and modify flows. To password-protect the editor:

Add the following user-defined variables.

* NODE_RED_USERNAME - the username to secure the editor with
* NODE_RED_PASSWORD - the password to secure the editor with