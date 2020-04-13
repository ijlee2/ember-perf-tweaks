# Creating Progressive Web Apps in Ember

To make your Ember app a Progressive Web App (PWA), you can use an addon called [`ember-web-app`](https://zonkyio.github.io/ember-web-app/).

## Installation

Let's create a new Ember app and add this addon.

```
ember new ember-app

ember install ember-web-app
```

The second command should have installed ember-web-app addon and added config/manifest.js file. You would also see your index.html file modified with these lines

![TODO: Provide description if possible](Creating%20installable%20Ember%20apps/Untitled.png)

Navigate to `config/manifest.js` and you should see a predefined set of values:

![TODO: Provide description if possible](Creating%20installable%20Ember%20apps/Untitled%201.png)

For a list of properties you can use, [check out the documentation](https://zonkyio.github.io/ember-web-app/docs/manifest/available-properties).

Let's run PWA on Lighthouse and see the results. The following is what you would see.

![TODO: Provide description if possible](Creating%20installable%20Ember%20apps/Untitled%202.png)

## Let's fix the offline pointer.

TODO: Describe what offline pointer is (you seem to be referring to the 2 suggestions under "Fast and reliable") before mentioning service workers. Surround "Caching assets using service workers" with a link to "## Asset Caching".

This is pretty straightforward as stated in "Caching assets using service workers" segment.

```
ember install ember-service-worker

ember install ember-service-worker-asset-cache

ember install ember-service-worker-index
```

Let's check the Lighthouse measurements again.

![TODO: Provide description if possible](Creating%20installable%20Ember%20apps/Untitled%203.png)

## More fixes

1. In order to fix "Does not provide fallback content when JavaScript is not available", let's add and that should be green.

TODO: To which file and between which lines does this code go?

```
<noscript>Some content here for your page without JavaScript</noscript>
```

2. To fix the PNG icon, you can just add an image in your config/manifest.js and it should be resolved. This is the config that I have added to the config/manifest.js. Make sure to replace the images with your Ember app's.

```
// config/manifest.js
'use strict';

module.exports = function(/* environment, appConfig */) {
  // See https://zonkyio.github.io/ember-web-app for a list of
  // supported properties

  return {
    name: "ember-app",
    short_name: "ember-app",
    description: "",
    start_url: "/",
    display: "standalone",
    background_color: "#fff",
    theme_color: "#fff",
    icons: [{
      src: 'ember-welcome-page/images/construction.png',
      sizes: '192x192'
    }, {
      src: 'ember-welcome-page/images/construction.png',
      sizes: '280x280',
      targets: ['apple']
    }, {
      src: 'ember-welcome-page/images/construction.png',
      sizes: '512x512'
    }],
    ms: {
      tileColor: '#fff'
    }
  };
}
```

By making these two fixes, you should have green checkmarks for all but one: HTTPS redirection.

![TODO: Provide description if possible](Creating%20installable%20Ember%20apps/Untitled%204.png)
