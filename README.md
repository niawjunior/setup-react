# Setup a React Environment Using webpack and Babel

### Prerequisites
```
yarn
```

### Installing

mac os

```
> brew update
> brew install yarn
```

windows

* [Download](https://yarnpkg.com/en/docs/install#windows-tab) - yarn for windows

### Getting Started
```
> mkdir hello-world-react
> cd hello-world-react
> yarn init
```
### Webpack installation and configuration
```
> yarn add webpack webpack-dev-server path
```

### Create a new file, webpack.config.js
```
> touch webpack.config.js
```
### Update the configuration file:
```
/*
    ./webpack.config.js
*/
const path = require('path');
module.exports = {
  entry: './client/index.js',
  output: {
    path: __dirname + "/dist",
    filename: "bundle.js"
  },
  module: {
    loaders: [
      { test: /\.js$/, loader: 'babel-loader', exclude: /node_modules/ },
      { test: /\.jsx$/, loader: 'babel-loader', exclude: /node_modules/ }
    ]
  }
}
```

### Setting up Babel

```
> yarn add babel-loader babel-core babel-preset-es2015 babel-preset-react --dev
```

### create .babelrc file

```
> touch .babelrc
```

### Then we can update the file to:

```
/* 
    ./.babelrc
*/  
{
    "presets":[
        "es2015", "react"
    ]
}
```

### Setting up our React Components

```
.
|-- node_modules
|-- .babelrc
|-- package.json
|-- webpack.config.js
|-- yarn.lock
```

### Create a new folder client and add an index.js file and an index.html file.

```
> mkdir client
> cd client
> touch index.js
> touch index.html
> cd .. 
```

### Now we have this:
```
.
|-- client
     |-- index.html
     |-- index.js
|-- .babelrc
|-- package.json
|-- webpack.config.js
|-- yarn.lock
```

### Open up index.js and add:
```
console.log('hello react')
```

### Update index.html to:
```
/*
    ./client/index.html
    basic html skeleton
*/
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>React App Setup</title>
  </head>
  <body>
    <div id="root">

    </div>
  </body>
</html>
```
### Html-Webpack-Plugin
Simplifies creation of HTML files to serve your webpack bundles
```
> yarn add html-webpack-plugin
```
Then open up your webpack.config.js and add a few configurations.
```
/* 
    ./webpack.config.js
*/
const path = require('path');

const HtmlWebpackPlugin = require('html-webpack-plugin');
const HtmlWebpackPluginConfig = new HtmlWebpackPlugin({
  template: './client/index.html',
  filename: 'index.html',
  inject: 'body'
})

module.exports = {

...

module: {
    loaders: [
        ...
    ]
},
// add this line
plugins: [HtmlWebpackPluginConfig]
}
```
### Run it!
 Open up your package.json and let's add a start script.
 ```
 /*
    ./package.json
*/
{
  "name": "hello-world-react",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",

  // add the scripts key to your package.json

  "scripts": {
    "start": "webpack-dev-server"
  },

  "dependencies": {
  ...
  },
  "devDependencies": {
  ...
  }
}
 ```
 
 Now we can go to our terminal and run:
 ```
 > yarn start
 ```
 Open your browser on http://localhost:8080/
  If you check your console you'll see our message "hello react"
