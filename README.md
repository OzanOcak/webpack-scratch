## building a react project from scratch

create a project folder and initialize npm that will create package.json file

```console
npx init -y
```

then create folders and files

```console
mkdir src public
touch src/index.js public/index.html webpackconfig.js README.md .gitignore .babelrc
```

open index.html and place the below code, id="root" is where the js/jsx code will be injected in html.

```html
<div id=“root”></div>
<script src=“../dist/bundle.js”></script>
```

in order to write ES6 syntax and add support to jsx syntax

```console
npm install —-save-dev @babel/core @babel/cli @babel/preset-env @babel/preset-react
```

what presets and plugins need to transpile/compile the jsx, open .babelrc and define json object; _@babel/preset-env_ is for ES6 and _@babel/preset-react_ is for Jsx

```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

### setting up webpack

```console
npm install —-save-dev webpack webpack-cli webpack-dev-server style-loader css-loader babel-loader
```

**webpackconfig.js**

```javascript
const path = require("path");
const webpack = require("webpack");

module.exports = {
  entry: "./src/index.js",
  mode: "development",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /(node_modules)/,
        loader: "babel-loader",
        options: { presets: ["@babel/env"] },
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"],
      },
    ],
  },
  resolve: { extensions: ["*", ".js", ".jsx"] },
  output: {
    path: path.resolve(__dirname, "dist/"),
    publicPath: "/dist/",
    filename: "bundle.js",
  },
  devServer: {
    contentBase: path.join(__dirname, "public/"),
    port: 3000,
    publicPath: "http://localhost:3000/dist/",
    hotOnly: true,
  },
  plugins: [new webpack.HotModuleReplacementPlugin()],
};
```

Lastly open package.json and inser below code in script

````json
"dev": "npx webpack-dev-server --mode=development",
```

Now we can run any react app with

```console
npm run dev
````
