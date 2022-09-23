# SDK for Embeds Quick Start

{% hint style="info" %}
**Note:** Usage of the SDK constitutes your agreement with the [Matterport SDK Agreement](https://matterport.com/legal/sdk-agreement/). Email [developer@matterport.com](mailto:developer@matterport.com) with any questions.
{% endhint %}

### A Complete Example to Get Started

This sample HTML creates an iframe containing a Matteport model. It then connects the Embed SDK, retrieves data about the model, and finally logs the model’s id.

You only need to replace the **two** `[YOUR_SDK_KEY_HERE]` strings with your own key (without the square brackets “\[”, “]”).

```html
<html>
  <head>
    <script src='https://static.matterport.com/showcase-sdk/latest.js'></script>
  </head>
  <body>
    <iframe
      width="853"
      height="480"
      src="https://my.matterport.com/show?m=SxQL3iGyoDo&play=1&applicationKey=[YOUR_SDK_KEY_HERE]"
      frameborder="0"
      allow="fullscreen; vr"
      id="showcase-iframe">
    </iframe>

    <script>
      (async function connectSdk() {
        const sdkKey = '[YOUR_SDK_KEY_HERE]'; // TODO: replace with your sdk key
        const iframe = document.getElementById('showcase-iframe');
        // connect the sdk; log an error and stop if there were any connection issues
        try {
          const mpSdk = await window.MP_SDK.connect(
            iframe, // Obtained earlier
            sdkKey, // Your SDK key
            '' // Unused but needs to be a valid string
          );
          onShowcaseConnect(mpSdk);
        } catch (e) {
          console.error(e);
        }
      })();

      async function onShowcaseConnect(mpSdk) {
        // try retrieving the model data and log the model's sid
        try {
          const modelData = await mpSdk.Model.getData();
          console.log('Model sid:' + modelData.sid);
        } catch (e) {
          console.error(e);
        }
      }
    </script>
  <body>
</html>
```
