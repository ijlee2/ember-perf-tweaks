# Speed

## Improving build size and time

### Minification, Gzip/Brotli compression, and Fingerprinting

Make sure your builds are done with `production` flag turned on.

```
ember b -p
# or
ember build --prod
# or
ember build --environment=production
```

First and foremost, every asset that index.html consumes needs to be minified and compressed. In Ember, your app can be configured to do so using the following lines of code:

```
// ember-cli-build.js

module.exports = function(defaults) {
  // ...
  const isProduction = EmberApp.env() === 'production';
    
  let app = new EmberApp(defaults, {
    fingerprint: {
      enabled: isProduction // Enabled in production by default until you override.
    },
    minifyJS: {
      enabled: isProduction // Enabled in production by default until you override.
    },
    minifyCSS: {
      enabled: isProduction // Enabled in production by default until you override.
    }
  });

  // ...

  return app.toTree();
};
```

You don’t have to generally worry about this configuration since Ember takes care of it for you for prod builds.

## Analyze bundle size and optimize asset size

[`ember-cli-bundle-analyzer`](https://github.com/kaliber5/ember-cli-bundle-analyzer) is an Ember CLI addon that analyzes the size and contents of your Ember apps.

It helps you to

- Analyze which individual modules make it into your final bundle
- Find out how big each contained module is in raw, minified, and gzipped formats
- Find unused modules
- Optimize your bundle size

Install this addon using the following command:

```
ember install ember-cli-bundle-analyzer
```

Once done, navigate to [http://localhost:4200/_analyze](http://localhost:4200/_analyz) in your web browser to analyze the output.

## Using dependencies that you only need on boot

When you use the traditional approach (from Ember 2.12 or before) of `app.import('node_modules/package/src.js');` in your ember-cli-build.js, any npm package that you install leads to an increased vendor.js file size. This is problematic if your Ember app has large packages like lodash-es but you only need _some_ of the lodash methods.

With [`ember-auto-import`](https://github.com/ef4/ember-auto-import), you can dynamically import these dependencies code at run time.

Before we go in depth, let's see our `vendor.js` of the current sample app:

TODO: Which sample app are we looking at? Is it always the new Ember app?

![TODO: Provide description if possible](Speed/Untitled.png)

It is at 591KB.

To get started with ember-auto-import:

```
npm install --save-dev lodash-es # Adds lodash-es for example to your dependencies

ember install ember-auto-import
```

Try importing capitalize in one of your components or controllers.

```
import { capitalize } from 'lodash-es';
```

vendor.js just increased by ~175KB! 😱

![TODO: Provide description if possible](Speed/Untitled%201.png)

Didn't we say we wanted to reduce the vendor.js size? Yes, for which you need to do a little bit more:

### Welcome Dynamic Import!

Dynamic import is currently a Stage 3 ECMA feature, so to use it there are a few extra setup steps:

1. Install babel-eslint

```
npm install --save-dev babel-eslint
```

2. In your .eslintrc.js file, add

```
parser: 'babel-eslint'
```

3. In your ember-cli-build.js file, enable the Babel plugin provided by ember-auto-import:

```
let app = new EmberApp(defaults, {
  babel: {
    plugins: [ require.resolve('ember-auto-import/babel-plugin') ]
  }
});
```

4. Finally, dynamically import the dependency. For example,

```
import Route from '@ember/routing/route';

export default class SampleInnerRoute extends Route {
  model() { // This will be render-blocking, you can also move this to your controller' or component' JS file
    return import('lodash-es').then(({ capitalize }) => {
      return capitalize('Sample App');
    });
  }
}
```

    ![TODO: Provide description if possible](Speed/Untitled%202.png)

    Moving to dynamic imports brought the size of vendor.js back down to 592KB.

## Measure Rendering Performance

Ember's ecosystem comes with a Google Chrome Extension and Mozilla Firefox Addon called "Ember Inspector". One of the important features of the Ember Inspector is "Render Performance". To read more about measuring rendering performance of your Ember apps, check out the [Ember.js Guides](https://guides.emberjs.com/release/ember-inspector/render-performance/).
