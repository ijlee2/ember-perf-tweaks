# SEO friendly pages

SEO friendly pages help rank better in search engine results. When you create a new Ember app and run Lighthouse, you should see the score of 90.

![TODO: Provide description if possible](SEO%20friendly%20pages/Untitled.png)

A few reasons that you get a high score by default are:

1. Ember CLI's ember new command adds `<meta name="viewport">` tag with the required set of values.
2. The index.html file created a proper `<title>` tag with your application's name.
3. `robots.txt` file is added by default to your `dist/` path. Once you host your app, it is ready for Search engines to start crawling.

However, you may have noticed that your page does not have:

1. a proper `lang` attribute on the `<html>` tag.
2. a proper description in the `<meta name="description" content="">` tag.

Go ahead and add both. Once you complete these steps, you should see

![TODO: Provide description if possible](SEO%20friendly%20pages/Untitled%201.png)

## Dynamic title

When you build content-driven applications like blogs, which need to be SEO friendly, the document title needs to change per page.

In order to get this up and running, you can use an addon called [`ember-page-title`](https://github.com/adopted-ember-addons/ember-page-title):

```
ember install ember-page-title
```

Then, all you need to do is,

TODO: Where does this code go?

```
{{title "Ember app"}}
```

You should see this `<title>` tag in your DOM now.

![TODO: Provide description if possible](SEO%20friendly%20pages/Untitled%202.png)

## Server side rendering

Server Side Rendering (SSR) in Ember is achieved using [Fastboot](https://ember-fastboot.com/). This addon performs initial render in the server and makes your Ember apps accessible to Search Engines. Users see content rendered fast and as if your app worked without Javascript.

Fastboot uses Node in the background to execute your Ember apps within it. 

Before we install and run Fastboot for your ember app, here's what your page source would be for a bare minimal Ember app.

Let's create a new Ember app using:

```
ember new ember-app
```

You can notice that the `<body>` tag only contains the 3 script tags

![TODO: Provide description if possible](SEO%20friendly%20pages/Untitled%203.png)

To get started with `ember-cli-fastboot`, run the following command:

```
ember install ember-cli-fastboot
```

This should install the addon and list it in your package.json file. To start your Fastboot server, you can still continue to use

```
ember serve
```

Now you should see the HTML content (doing a "View page source") inlined. Note, the DOM content comes from  `<WelcomePage />` component that was added to your `application.hbs` when you ran the command `ember new ember-app`.

![TODO: Provide description if possible](SEO%20friendly%20pages/Untitled%204.png)

### Pro Tips

You could also try [empress-blog](https://github.com/empress/empress-blog) if you want to build a blog engine.