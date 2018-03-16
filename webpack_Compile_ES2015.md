
# Use Babel & Webpack To Compile ES2015 - ES2017

https://www.youtube.com/watch?v=iWUR04B42Hc


## 配置基本的目录结构 

```bash
mkdir babel_webpack_starter

npm init

npm install --save-dev webpack webpack-dev-server babel-core babel-loader babel-preset-env

# webpack config file
touch webpack.config.js

```

![](./images/rxjs_env.png)


```json

// following cousers have to install specific release of libraries;
{
  "name": "babel_webpack_starter",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    // use `npm run build` to build our peoject
    "build": "webpack"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "babel-core": "^6.26.0",
    "babel-loader": "^7.1.4",
    "babel-preset-env": "^1.6.1",
    "webpack": "^3.8.1",
    "webpack-dev-server": "^2.9.5"
  }
}

```

```js
// webpack.config.json


const path = require('path');

module.exports = {
    entry: {
        app: './src/app/js'
    },
    output: {
        path: path.resolve(__dirname, 'build'),
        filename: 'app.bundle.js'
    },
    module: {
        loaders: [{
            test: /\.js?$/,
            exclude: /node_modules/,
            loader: 'babel-loader',
            query: {
                preset: ['env']
            }
        }]
    }
}

```

> test this config

```bash
mkdir src
cd src
touch app.js

+ src
| + app.js

vi app.js

```