> With Electron, creating a desktop application for your company or idea is easy. Initially developed for GitHub's Atom editor, Electron has since been used to create applications by companies like Microsoft, Facebook, Slack, and Docker.

```bash
npm install electron-reload --save
```

```javascript
// the parametr is the directory to watch
require("electron-reload")(__dirname);
```

## Using Phi

[Golden Ratio](https://en.wikipedia.org/wiki/Golden_ratio)

## Layouts

[React Desktop](http://reactdesktop.js.org/)

[Photon](http://photonkit.com/)

## Using Handlebars

```bash
npm install --save handlebars underscore
```

### Compile a View

```javascript
var fs = require('fs');
var path = require('path');
var Handlebars = require('handlebars');

var View = function(viewName){
    
    // the files should be in the root of the app
    var templatePath = path.join(__dirname, '../partials', viewName + '.hbs');
    var source = fs.readFileSync(templatePath,'utf-8');
    var template = Handlebars.compile(source);
    
    this.toHtml = function(data) {
        return template(data);
    }
};

module.exports = View;
```

### Dealing with events (view-seleccted and rendered)

```javascript
var Emitter = require('events').EventEmitter;
var util = require('util');
var path = require('path');
var fs = require('fs');
var View = require('./view');

var App = function() {
    
    this.on('view-selected', function(viewName){
        var view = new View(viewName);
        this.emit('rendered',view.toHtml());
    });
};

util.inherits(App, Emitter);
module.exports = new App();
```