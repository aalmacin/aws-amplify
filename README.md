# Create AWS Amplify App

## Create project files
```sh
mkdir src
touch src/app.js
npm init -f
```

Add scripts in `package.json`

```json
{
  // ...
    "start": "webpack && webpack-dev-server --mode development",
    "build": "webpack"
  // ...
}
```

Add dependencies
```sh
npm i -D webpack webpack-cli copy-webpack-plugin webpack-dev-server
```

* `copy-webpack-plugin` will be used to copy `index.html`

Create `index.html`
```html
<!DOCTYPE html>
<html lang="en">

    <head>
        <meta charset="UTF-8">
        <title>AWS amplify</title>
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <style>
            html, body { font-family: "Amazon Ember", "Helvetica", "sans-serif"; margin: 0; }
            a { color: #FF9900; }
            h1 { font-weight: 300; }
            .app { width: 100%; }
            .app-header { color: white; text-align: center; background: linear-gradient(30deg, #f90 55%, #FFC300); width: 100%; margin: 0 0 1em 0; padding: 3em 0 3em 0; box-shadow: 1px 2px 4px rgba(0, 0, 0, .3); }
            .app-logo { width: 126px; margin: 0 auto; }
            .app-body { width: 400px; margin: 0 auto; text-align: center; }
            .app-body button { background-color: #FF9900; font-size: 14px; color: white; text-transform: uppercase; padding: 1em; border: none; }
            .app-body button:hover { opacity: 0.8; }
        </style>
    </head>

    <body>
        <div class="app">
            <div class="app-header">
                <div class="app-logo">
                    <img src="https://aws-amplify.github.io/images/Logos/Amplify-Logo-White.svg" alt="AWS Amplify" />
                </div>
                <h1>Welcome to AWS Amplify</h1>
            </div>
            <div class="app-body">
                <button id="AnalyticsEventButton">Generate Analytics Event</button>
                <div id="AnalyticsResult"></div>
            </div>
        </div>
        <script src="main.bundle.js"></script>
    </body>

</html>
```

Create webpack config (`webpack.config.js`)
```javascript
const CopyWebpackPlugin = require('copy-webpack-plugin');
const webpack = require('webpack');
const path = require('path');

module.exports = {
    mode: 'development',
    entry: './src/app.js',
    output: {
        filename: '[name].bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/
            }
        ]
    },
    devServer: {
        contentBase: './dist',
        overlay: true,
        hot: true
    },
    plugins: [
        new CopyWebpackPlugin(['index.html']),
        new webpack.HotModuleReplacementPlugin()
    ]
};
```

Install amplify for the project

```sh
npm i aws-amplify
```

Setup AWS

```sh
amplify init
```
