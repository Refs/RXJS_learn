
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


```json
{
  "name": "babel_webpack_starter",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    // use npm build to build our peoject
    "build": "webpack"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "babel-core": "^6.26.0",
    "babel-loader": "^7.1.4",
    "babel-preset-env": "^1.6.1",
    "webpack": "^4.1.1",
    "webpack-dev-server": "^3.1.1"
  }
}

```