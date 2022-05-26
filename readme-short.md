# Working environment short:

## run commands inside project directory:

As administrator in powershell:

```
npm install --global windows-build-tools
```

In a terminal, e.g. in visual studio code terminal

```
npm init-y
npm install webpack --save-dev
npm install webpack -g
npm install webpack-cli --save-dev
npm install webpack-cli -g
npm install html-webpack-plugin --save-dev
npm install style-loader --save-dev
npm install css-loader --save-dev
npm install sass-loader --save-dev
npm install sass --save-dev
npm install webpack-dev-server --save-dev
npm install url-loader --save-dev
npm install terser-webpack-plugin --save-dev
```

create files
`/src/index.html`

```
<html>
  <head> </head>
  <body>
    <div>Hello world!</div>
  </body>
</html>
```

`/src/index.js`

```
console.log("hey!");
```

.gitignore

```
node_modules/
.DS_Store
dist/
```

`webpack-config.js`

```
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "main.js",
    path: path.resolve(__dirname, "dist")
  },

  module: {
    rules: [
      // configurations for loaders will go here!
    ]
  },

  plugins: [
    new HtmlWebpackPlugin({
      inject: "body",
      template: "./src/index.html",
      filename: "index.html"
    })
  ]
};
```

`./src/css/styles.css`

```
body {
  background-color: aqua;
}
```

add to `package.json`:

```
"scripts": {
 "build": "webpack --mode development",
 "test": "echo \"Error: no test specified\" && exit 1"
 },
```
