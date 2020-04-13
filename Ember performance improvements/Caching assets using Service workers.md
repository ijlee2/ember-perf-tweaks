# Caching assets using Service workers

Service workers have magical powers. To know more, [read here](https://web.dev/service-workers-cache-storage/).

If you are building Ember apps for mobile users, keep in mind that they have extremely slow network connections on the move. Service workers can be an effective strategy for loading your apps faster. [`ember-service-worker`](https://github.com/DockYard/ember-service-worker) is an Ember addon that takes care of service worker registrations, asset caching, etc.

## Installation

To install `ember-service-worker` in your Ember apps, go ahead and perform the following command:

```
ember install ember-service-worker
```

Restart your Ember app to see that your app has registered a service-worker.

![TODO: Provide description if possible](Caching%20assets%20using%20Service%20workers/Untitled.png)

Notice the `sw-registration.js` file? You should also notice the following message that says “Service worker registration succeeded”.

![TODO: Provide description if possible](Caching%20assets%20using%20Service%20workers/Untitled_1.png)

## Asset Caching

In order to start asset caching, you need to install an `ember-service-worker` plugin called [`ember-service-worker-asset-cache`](https://github.com/DockYard/ember-service-worker-asset-cache).

```
ember install ember-service-worker-asset-cache
```

Once this addon is installed, inspect the Network tab on Chrome. You should see that the assets (CSS and JS) are served from “ServiceWorker”.

![TODO: Provide description if possible](Caching%20assets%20using%20Service%20workers/Untitled_2.png)

Notice, [localhost](http://localhost/) (index.html) file is not cached. Don’t worry, another `ember-service-worker` plugin called [`ember-service-worker-index`](https://github.com/DockYard/ember-service-worker-index) has got you covered.

```
ember install ember-service-worker-index
```

![TODO: Provide description if possible](Caching%20assets%20using%20Service%20workers/Untitled_3.png)

Well, you can now turn off your “Internet” and refresh the page. Your app will still load and is now “Offline first”.

Now that your assets and index.html files are cached, they should be faster on mobile networks that are slow.

---

### Pro Tips

1. If you followed the steps above, you might have seen something different from the screenshots. This is likely because the service workers and caching plugins cached your assets. In Google Chrome, you can check the “Update on Reload” setting from the “Application” tab of Developer tools. Another way is to find your service worker from “Application” tab of Developer tools, click “Unregister”, then reload the page. The reload should resolve the issue.

    ![TODO: Provide description if possible](Caching%20assets%20using%20Service%20workers/Untitled_4.png)

2. Do not fingerprint service-worker files. By default, `sw-registration.js` file is not fingerprinted. This is to make sure your app’s service worker registration and asset cache are not lost on rebuild and reload.
