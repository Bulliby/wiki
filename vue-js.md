---
title: vue.js
description: Note about vue.js developement
published: true
date: 2021-05-22T16:12:55.149Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:59:14.514Z
---

# Vue.js

## Installation

Vue.js come with npm : `npm install vue`

We need the **webpack** bundler for bundling us a main.js to include in our html code:

```shell
npm install webpack webpack-cli --save-dev
npm install vue-loader vue-template-compiler
npm install css-loader vue-style-loader
```
* `webpack-cli` and `webpack` : for cli interface of webpack on development mode.
* `vue-loader` : for parse `.vue` file.
* `vue-template-compiler` : for pasrse `<template>` tag in single file component.
* `css-loader` : for handle `.css`
* `vue-style-loader` : parse `<style>` tag in single file component.

#### webpack.config.dev.js

```js
const path = require('path');
const VueLoaderPlugin = require('vue-loader/lib/plugin');
const webpack = require('webpack');

module.exports = {
    entry: './src/Vue/app.js',
    mode: 'development',
    output: {
        path: path.resolve(__dirname, '../dist')
    },
    module: {
        rules: [
            {
                test: /\.vue$/,
                loader: 'vue-loader',
            },
            {
                test: /\.css$/,
                use: [
                    'vue-style-loader',
                    'css-loader'
                ]
            },
            {
                test: /\.(png|jpg)$/,
                use: [
                    'file-loader'
                ]
            },
            {
                test: /\.(woff(2)?|ttf|eot|svg)(\?v=\d+\.\d+\.\d+)?$/,
                use: [{
                    loader: 'file-loader',
                    options: {
                        name: '[name].[ext]',
                        outputPath: 'fonts/'
                    }
                }]
            },
        ]
    },
    plugins: [
        new VueLoaderPlugin(),
        new webpack.DefinePlugin({
            'process.env': require('../config/prod.env')
            //Permit to load the environments variables of the file prod.env.
        })  
    ]
};
```

#### package.json

```json
{
  "license": "MIT",
  "description": "A trafic monitoring on Github",
  "repository": {
    "type": "git",
    "url": "https://github.com/Bulliby/didactic-bassoon.git"
  },
  "dependencies": {
    "vue": "^2.5.17"
  },
  "devDependencies": {
    "css-loader": "^1.0.1",
    "vue-loader": "^15.4.2",
    "vue-style-loader": "^4.1.2",
    "vue-template-compiler": "^2.5.17",
    "webpack": "^4.26.1",
    "webpack-cli": "^3.1.2"
  },
  "scripts": {
    "watch": "webpack -w --config ./build/webpack.config.dev.js",
    "build": "webpack --config ./build/webpack.config.dev.js"
  }
}

```
