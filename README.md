# react-skeleton

Creando React app sin ejecutar `create-react-app`


# Ejecutar con `git clone`
```sh
git clone https://github.com/hectormoreira/react-skeleton.git
cd react-skeleton
npm install
npm start
```
# Tutorial
## 1. Instalar dependencias
```sh
npm init -y
npm install react react-dom 
# install babel
npm install @babel/core @babel/preset-env @babel/preset-react babel-loader -D
# install webpack
npm install webpack webpack-cli webpack-dev-server -D
# install loaders
npm install html-webpack-plugin style-loader css-loader file-loader -D


```

## 2. Crear archivo `.babelrc`
```json
{  
 "presets": [
        "@babel/preset-react",
        "@babel/preset-env"
            ]
}
```

## 3. Crear archivo `webpack.config.js `
```js
const HtmlWebpackPlugin = require("html-webpack-plugin");
const path = require("path");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.[hash].js",
    path: path.resolve(__dirname, "dist"),
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html",
    }),
  ],
  resolve: {
    modules: [__dirname, "src", "node_modules"],
    extensions: ["*", ".js", ".jsx", ".tsx", ".ts"],
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: require.resolve("babel-loader"),
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"],
      },
      {
        test: /\.png|svg|jpg|gif$/,
        use: ["file-loader"],
      }, 
    ],
  },
};
```
## 4. Crear folder `src` y dentro crear archivo `App.js`
```js
import React from "react";

const App = () => ( 
    <div>
        <h1>Hello React</h1>
    </div>
);

export default App;
```

## 5. Crear archivo `index.js`
```js
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

ReactDOM.render(<App/>,document.querySelector("#root"));
```

## 6. Crear archivo `index.html`
```html
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React</title>
</head>

<body>
    <div id="root"></div>
</body>

</html>
```

## 7. Agregar scripts en `package.json`
```js
"scripts": {
    "start": "webpack serve  --hot --open",
    "build": "webpack --config webpack.config.js --mode production"
  }
```

# Run project `npm start`