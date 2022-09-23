# SDK Client Changelog

Updates to the client functionality are automatic as long as you include the latest sdk client script on your page. See [Vocabulary - SDK Client](../getting-started/vocabulary.md)

### v2.0.1

**July 15, 2020**

* Added `waitUntil` function to current and future observable properties, e.g. `App.state.waitUntil`, `Camera.pose.waitUntil`, and `Camera.zoom.waitUntil`. See [Observable waitUntil](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/iobservable.html#waituntil).

**Feb 5, 2020**

* Fixed a bug where reconnecting to the sdk would fail. Update your sdk client file to `https://static.matterport.com/showcase-sdk/2.0.1-0-g64e7e88/sdk.js`

### v2.0.0

**Dev 19, 2020**

* In order to use synchronous functions, you will need to update your sdk client reference to `https://static.matterport.com/showcase-sdk/2.0.0-0-g7edd6b8/sdk.js`

### v1.2.0-31

**Aug 22, 2019**

* Updated to `https://static.matterport.com/showcase-sdk/1.2.0-31-g16b6637/sdk.js`

### v1.2.0-0

**June 27, 2018**

* Updated to: `https://static.matterport.com/showcase-sdk/1.2.0-0-g1d0799d/sdk.js`
