# dotenv-webpack

A secure webpack plugin that supports dotenv and other environment variables and **only exposes what you choose and use**.

### Status

[![npm](https://img.shields.io/npm/v/dotenv-webpack.svg?maxAge=0&style=flat)](https://www.npmjs.com/package/dotenv-webpack)
[![Travis](https://travis-ci.org/mrsteele/dotenv-webpack.svg?branch=master)](https://travis-ci.org/mrsteele/dotenv-webpack)
[![Coverage Status](https://coveralls.io/repos/github/mrsteele/dotenv-webpack/badge.svg?branch=master)](https://coveralls.io/github/mrsteele/dotenv-webpack?branch=master)
[![Dependency Status](https://david-dm.org/mrsteele/dotenv-webpack.svg)](https://david-dm.org/mrsteele/dotenv-webpack)
[![devDependency Status](https://david-dm.org/mrsteele/dotenv-webpack/dev-status.svg)](https://david-dm.org/mrsteele/dotenv-webpack?type=dev)
[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/)
[![npm](https://img.shields.io/npm/l/dotenv-webpack.svg?maxAge=0&style=flat)](https://raw.githubusercontent.com/mrsteele/dotenv-webpack/master/LICENSE)
[![pull requests](https://img.shields.io/badge/pull%20requests-accepting-brightgreen.svg?style=flat)](https://github.com/mrsteele/dotenv-webpack/fork)

### Installation

Include the package locally in your repository.

`npm install dotenv-webpack --save`

### Description

`dotenv-webpack` wraps `dotenv` and `Webpack.DefinePlugin`. As such, it overwrites existing any existing `DefinePlugin` configurations. Also, like `DefinePlugin`, it does a text replace in the resulting bundle for any instances of `process.env`.

Your `.env` files can include sensitive information. Because of this,`dotenv-webpack` will only include defined environment variables in the final bundle.

### Usage

The plugin can be installed with little-to-no configuration needed. Once installed, you can access the variables within your code using `process.env` as you would with `dotenv`.

The example bellow shows a standard use-case.

###### Create a .env file

```
// .env
DB_HOST=127.0.0.1
DB_PASS=foobar
S3_API=mysecretkey

```
###### Add it to your Webpack config file
```javascript
// webpack.config.js
const Dotenv = require('dotenv-webpack');

module.exports = {
  ...
  plugins: [
    new Dotenv({
      path: './.env' // Path to .env file (this is the default)
      safe: true // load .env.example (defaults to "false" which does not use dotenv-safe)
    })
  ]
  ...
};
```

###### Use in your code

```
// file1.js
console.log(process.env.DB_HOST);
// '127.0.0.1'
```

###### Resulting bundle
```
// bundle.js
console.log('127.0.0.1');
```

### How Secure?

Be allowing you to define exactly where you are loading environment variables from, and bundling only included variables in your project you can be sure that only what you need is included and you do not accidentally leak anything sensitive.

###### Recommended

Add `.env` to your `.gitignore` file

### Properties

Use the following properties to configure your instance.

* **path** (`'./.env'`) - The path to your environment variables.
* **safe** (`false`) - If false ignore safe-mode, if true load `'./.env.example'`, if a string load that file as the sample.
* **systemvars** (`false`) - Set to true if you would rather load all system variables as well (useful for CI purposes).

### LICENSE

MIT
