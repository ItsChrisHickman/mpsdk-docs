# Getting Started

**Note:** Usage of the SDK constitutes your agreement with the [Matterport SDK Agreement](https://matterport.com/legal/sdk-agreement/). Email [developer@matterport.com](mailto:developer@matterport.com) with any questions.

### Include the Library and Add a Matterport Space

First, add the 3D Showcase SDK to your web application by including the Javascript library. This line goes in the `<head>` tag with your other includes.

```
  <script src='https://static.matterport.com/showcase-sdk/latest.js'>
```

Next, embed a Matterport Space on your web page with an `<iframe>` tag. [Learn more about embedding](https://support.matterport.com/hc/en-us/articles/115004549347-Embed-a-Space-with-an-iframe-).

Add the **\&play=1** URL parameter to automatically load the `<iframe>` when the page loads for a better user experience.

Add the **applicationKey=\[YOUR SDK\_KEY]** URL parameter to provide your sdk key as part of the url.

Give the `<iframe>` an ID you will use later.

```
<iframe
  width="853"
  height="480"
  src="https://my.matterport.com/show?m=SxQL3iGyoDo&play=1&applicationKey=[YOUR_SDK_KEY_HERE]"
  frameborder="0"
  allow="fullscreen; vr"
  id="showcase-iframe">
</iframe>
```

### Connect to the Matterport Space

Now in the Javascript code for your web application, connect to the Matterport Space.

You’ll want to wait until the `<iframe>` containing the Matterport Space loads. Connecting happens after you’ve included the SDK library.

Replace the **\[YOUR\_SDK\_KEY\_HERE]** string with your sdk key.

```
const iframe = document.getElementById('showcase-iframe');

// connect the sdk; log an error and stop if there were any connection issues
try {
  const mpSdk = await window.MP_SDK.connect(
    iframe, // Obtained earlier
    '[YOUR_SDK_KEY_HERE]', // Your SDK key
    '' // Unused but needs to be a valid string
  );
  onShowcaseConnect(mpSdk);
} catch (e) {
  console.error(e);
}

function onShowcaseConnect(mpSdk) {
  // start making calls on mpSdk as described in the reference docs
}
```

| Parameter         | Description                                                                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `showcase-iframe` | The value you put for the the `id` parameter in the `<iframe>` tag earlier.                                                                    |
| `applicationKey`  | Your SDK key is unique to your website domain. Go to Matterport Account Settings -> Developer Tools to create an SDK key for your application. |

**Note:** Visit [Sandbox vs. Production Access](https://support.matterport.com/hc/en-us/articles/360057506813-Developer-Tools-Pricing-and-Availability#sandbox-vs-production-access-0-0) to learn more about developer tools access restrictions.**Note:** For local development, you’ll need to run your app off a local web server. We recommend using a NodeJS server.

### Control 3D Showcase with Actions

Now you’ll want to make an action for 3D Showcase to execute. In the code for your web application, add this to a Javascript function where desired. Refer to the [reference docs](https://matterport.github.io/showcase-sdk/sdk\_reference\_summary) for a list of all the actions you can do.

```
showcase.<action>(<arguments>).then(successCallback)
.catch(errorCallback);

// ...

// What to do if action was successful
function successCallback(message) { console.log(message); }

// What to do if the action failed
function errorCallback(err) { console.error(err); }
```

| Parameter     | Description                            |
| ------------- | -------------------------------------- |
| `<action>`    | The action you want 3D Showcase to do. |
| `<arguments>` | The arguments for that action.         |

### Listen to Events from 3D Showcase

Listening for events from 3D Showcase is done in a similar way.

```
showcase.on(<event_name>, function (<state_arguments>) {
  // what to do when this event happens
});
```

| Parameter           | Description                                                                                                           |
| ------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `<event_name>`      | Event you’re listening for                                                                                            |
| `<state_arguments>` | Return values related to this event. These tell you about the new state of 3D Showcase after this event has happened. |

### Use the Metadata

Finally, you can grab metadata about the entire Matterport Space by calling `getData()` and `getDetails()` in your web app. For example:

```
mpSdk.Model.getData()
  .then(function(model) {
    // Model data successfully retrieved
    console.log('Model sid:' + model.sid);
  })
  .catch(function(error) {
    // Problem retrieving model data
  });
```

Metadata is only available **after** you have successfully connected to the Matterport Space.
