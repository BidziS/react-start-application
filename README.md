# react-start-application
**How to setup react environment with basic configuration**
1. Write cmd in start
2. Write in console:
```
mkdir your_application_name && cd your_application_name
npm init
npm install -S react react-dom
npm install -D babel-core bable-loader babel-preset-react
npm install -D webpack webpack-dev-server html-webpack-plugin
npm install --save-dev babel-preset-stage-0

```
3. Create a file ".babelrc.js" in your root directory. Inside this file write:
```js
{ presets: ['react']}
```
4. Create a file "webpack.config.js" in your root directory. Inside this file write:
```js
var HTMLWebpackPlugin = require('html-webpack-plugin');

var HTMLWebpackPluginConfig = new HTMLWebpackPlugin({
    template: __dirname + '/app/index.html',
    filename: 'index.html',
    inject: 'body'
});

module.exports = {
    entry: __dirname + '/app/index.js',
    module:{
        loaders: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                loader: 'babel-loader?presets[]=react',
                query:{
                    presets: ['es2015', 'react','stage-0']
                }
            }
        ]
    },
    output: {
        filename: 'transformed.js',
        path: __dirname + '/build'
    },
    plugins:[HTMLWebpackPluginConfig]
};
```
5. In package.json, replace the "scripts" with this:
```json
"scripts": {
    "build": "webpack",
    "start": "webpack-dev-server",
    "deploy": "npm run build && npm run git-commit && npm run git-push"
  }
```
6. In yor root directory create "app" folder. In this folder create: index.html and index.js file.
7. In "app" folder create "components" folder. In this folder create app.js file.
8. In index.html write:
```html
<!DOCTYPE html>
<html lang="pl">
    <head>
        <meta charset="UTF-8">
        <title>React Application</title>
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
    </head>
    <body>
        <div id="app"></div>
    </body>
</html>
```
9. In index.js file write:
```js
var React = require('react');
var ReactDOM = require('react-dom');

import { App } from './components/app';

ReactDOM.render(
    <App />,
    document.getElementById('app')
);
```
10. In app.js file write:
```js
import React, { Component } from 'react';
    render() {
        return (
        <div className="container">
            Hello!
        </div>
        );
    }
}
```
