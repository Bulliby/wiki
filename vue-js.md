<!-- TITLE: vue.js -->
<!-- SUBTITLE: Note about vue.js developement  -->

# Vue.js

## Installation

Vue.js come with npm : `npm install vue`

We need the **webpack** bundler for parsing vue's files : `.vue` with:

```shell
npm install webpack webpack-cli --save-dev
npm install vue-loader vue-template-compiler
npm install css-loader vue-style-loader
```
* `webpack-cli` : for cli interface of webpack.
* `vue-loader` : for parse `.vue` file.
* `vue-template-compiler` : for pasrse `<temlate>` tag.
* `css-loader` : for handle `.css`
* `vue-style-loader` : parse `<style>` tag.

#### webpack.config.dev.js

```js
const path = require('path');
const VueLoaderPlugin = require('vue-loader/lib/plugin');

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
        ]
    },
    plugins: [
        new VueLoaderPlugin()
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
