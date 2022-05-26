# How to use

`npm run build`
Wither use live server plugin from visual studio code or:
`npm run start` (The open is optional -> creates a server and starts the browser)
https://www.robinwieruch.de/minimal-react-webpack-babel-setup/ -> noch anschauen für react

# Working environment

Based on https://www.learnhowtoprogram.com/user-interfaces/responsive-design-development-environments

## Install npm

1. Install via https://nodejs.org/en/download/
2. confirm installation: `npm -v` (version should appear)
3. Create a new folder for the project and cd into folder
4. Initializing npm: `npm init -y`
   1. -y for skipping configuration steps
   2. creates a `package.json` -> manifest (lists all installed dependencies)
5. Install dependencies with npm e.g. bootstrat
   1. `npm install bootstrap`
   2. `npm install jquery`
   3. Our package.json manifest file will be updated
   4. A new node_modules directory will appear in our project
   5. Depending on our version of npm, a package-lock.json file will appear too. -> This file helps avoid dependency versioning issues by "locking down" versions. **Don't touch this file**. npm is programmed to automatically maintain it for us. Just leave it as-is
6. Installing multiple dependencies if only the package.json exists or if for example the node_modules folder is deleted -> `npm install` will install all dependencies of the package.json
7. Create a `.gitignore` file!
   1. File with content:
   ```
    node_modules/
    .DS_Store
   ```
   .DS_Store is a mac specific file
   node_modules/ directory only contains code from dependencies and therefore not necessary because `npm install` can be used if necessary. 2. .gitignore must be committed before the commit with node_modules!
8. Uninstalling dependencies
   ```
    npm uninstall bootstrap
    npm uninstall jquery
   ```

## Install webpack

```
npm install webpack@4.0.1 --save-dev
npm install webpack@4.0.1 -g
npm install webpack-cli@2.0.9 --save-dev
npm install webpack-cli@2.0.9 -g
```

Explanation:

1. The --save-dev bit at the very end. This specifies that Webpack is a development dependencies.
2. -g stand for global -> "install this package in a specific directory, but globally on the computer itself. This ensures our terminal recognizes Webpack commands."
3. Webpack CLI assists in calling Webpack from the terminal.

### Try it with command `webpack` -> The following error will appear

```
Hash: d1e91c23aed606d345bb
Version: webpack 4.0.1
Time: 21ms
Built at: 26/05/2022 15:10:17

WARNING in configuration
The 'mode' option has not been set. Set 'mode' option to 'development' or 'production' to enable defaults for this environment.

ERROR in Entry module not found: Error: Can't resolve './src' in 'C:\source\modern-environment-practice'
```

1. Create entry point directory and file ./src/index.js with example content:
   ```
   console.log("hey!");
   ```
2. Add flag to command to specify mode: `webpack --mode development`
3. Now packaging should work and should create a dist directory (distribution)
4. .gitignore should also include the `dist/` folder
5. If for example the folder node_modules or dist folder were commited before adding it to .gitignore, run the following command for every folder that should not be tracked, e.g. with dist folder:
   ```
   git rm --cached dist
   ```

## Add npm scripts

1. add script for packaging and bundling with webpack. Add the following under the section scripts in `package.json`
   ```
    "scripts": {
    "build": "webpack --mode development",
    "test": "echo \"Error: no test specified\" && exit 1"
    },
   ```
2. Now you can use `npm run build`

## Webpack configuration file

`webpack.config.js`

```
const path = require('path');

module.exports = {

  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  },

  module: {

    rules: [
      // configurations for loaders will go here!
    ]

  },

  plugins: [
      // configurations for plugins will go here!
  ]

};

```

1. Here we're defining a JavaScript **constant**. Constants are like variables, but they forbid their values from being altered. That is, their values are constant. We'll learn more about them in our JavaScript course.
1. **require** is a JavaScript keyword that imports code from another part of the project, like from a dependency in node_modules.
1. **path** refers to a dependency named **Path**. This is an internal dependency of Webpack. The outside dependencies we install with npm usually rely on other dependencies in their own internal code. But we don't have to install these other dependencies; npm handles it for us.
1. The path library resolves file paths.
1. Webpack configurations are stored inside a special object called **module.exports**
1. You may recall Webpack already knew where to find our entry point file earlier. This is because we placed it in the default location. However, it's still best practice to explicitly declare it in configurations. (with the code "entry : './src/index.js'")

## Installing and configuring a webpack plugin -> html-webpack-plugin

Install via:

```
npm install html-webpack-plugin@3.2.0 --save-dev
```

Configure via the following in `webpack.config.js`

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {

  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  },

  module: {
    rules: [
      // configurations for loaders will go here!
    ]
  },

  plugins: [

    new HtmlWebpackPlugin({
      inject: 'body',
      template: './src/index.html',
      filename: 'index.html'
    })

  ]

};
```
