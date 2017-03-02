# Webpack

You can use Webpack to include and bundle UIkit's JavaScript in your project.

***

## Project setup

For the basic project setup, we will create the following files:

```html
app/
    index.js
index.html
package.json
```

The following commands will create and fill the file `package.json`. It contains the dependencies for Npm. We include UIkit, jQuery and Webpack.

```sh
mkdir uikit-webpack && cd uikit-webpack
npm init -y
npm install --save uikit jquery
npm install --save-dev webpack
```

As an entry file for the projects JavaScript, create a file `app/index.js` with the following content.

```js
import UIkit from 'uikit';
import $ from 'jquery';

// components can be called from the imported UIkit reference
UIkit.notification('Hello world.');
```

This way you have references to UIkit and jQuery available without having to include their JavaScript files in your HTML. Instead, we can include the full bundle that will be created by Webpack. Create the main HTML file `index.html` with the following content.

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title></title>
        <link rel="stylesheet" href="node_modules/uikit/dist/css/uikit.min.css">
    </head>
    <body>

        <div class="uk-container">
            <div class="uk-card uk-card-body uk-card-primary">
                <h3 class="uk-card-title">Example headline</h3>

                <button class="uk-button uk-button-default" title="Hello World" uk-tooltip>Hover</button>
            </div>
        </div>

        <script src="dist/bundle.js"></script>
    </body>
</html>
```

**Note** For simplicity reasons, we have included the pre-built CSS. In a real project, you probably want to build the [Less](less.md) files and included the compiled CSS instead.

To configure Webpack to compile `app/index.js` into `dist/bundle.js`, create the file `webpack.config.js` with the following content.

```js
module.exports = {
    entry: './app/index.js',
    output: {
        filename: 'bundle.js',
        path: './dist'
    }
};
```

Now, run Webpack in your project's main directory.

```sh
./node_modules/.bin/webpack # Run webpack from local project installation
webpack # If you installed webpack globally
```

This completes the basic setup of your project. Navigate to `index.html` in your browser and confirm that the basic UIkit styling is applied to your page. If the bundling was successful, a notification should pop up at the top of your page and the button should display a message on hover.