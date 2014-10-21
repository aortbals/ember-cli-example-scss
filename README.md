# Ember-cli-example-scss

An example application managing SCSS and CSS dependencies.

1. [SCSS Support](https://github.com/aortbals/ember-cli-example-scss/commit/efd51a823dbf774fe812d860b325e7cec439f5ae)

```shell
npm install --save-dev broccoli-sass
```

2. [Add a traditional CSS dependency](https://github.com/aortbals/ember-cli-example-scss/commit/7ce89521b2c974d442dbd34807c996447511205b)

```shell
bower install --save normalize-css
```

`Brocfile.js`

```js
app.import('bower_components/normalize-css/normalize.css');
```

3. [Add Bourbon & Bourbon Neat](https://github.com/aortbals/ember-cli-example-scss/commit/b059b2c15d3a871da698a1e3c18f3b0bc00f9771)

Bourbon and Neat must be [`@import`](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#import)'d in your `app.scss` file so that you can properly use the mixins, etc. In order to do this, they must be merged into the app `styles` broccoli tree. Unlike a traditional CSS dependency, these two dependencies cannot use `app.import` in `Brocfile.js`.

```shell
npm install --save-dev broccoli-merge-trees
bower install --save bourbon#3.2.3 neat#1.5.1
```

`Brocfile.js`

```js
...
var mergeTrees = require('broccoli-merge-trees');

var app = new EmberApp({
  trees: {
    styles: mergeTrees([
      'bower_components/bourbon/dist',
      'bower_components/neat/app/assets/stylesheets',
      'app/styles'
    ],
    { overwrite: true })
  }
});
...
```
