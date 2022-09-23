# Model API FAQs

<details>

<summary>The Showcase SDK and Model API coordinates don't seem to match - how do I use both? </summary>

This is a bit confusing, but is expected behavior. The Showcase SDK is designed to work from the perspective of the camera, so its coordinate system rotates to determine the Y axis (height) and Z axis (depth). If you were to download a MatterPak, you would find all of the coordinate information with Z-up. The SDK hides this by only exposing certain pieces of information.&#x20;

​![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FSYkkaUU45Ac8CYeWIAC1%2Fuploads%2FGjwgtytk0V1GDwTruAm9%2Fright.png?alt=media\&token=fed57cbe-515f-4b15-87cb-bc4fb1094936)

The pseudo-code for doing the translation is as follows:&#x20;

```
def fromSdkToApi(x, y, z) = { x, -z, y }

def fromApiToSdk(x, y, z) = { x, z, -y }
```

Note that the translation above may seem odd because the Z and Y coordinates are both flipped, and one is inverted.&#x20;

</details>

<details>

<summary>I can't see the changes I am doing with the Model API right away - what should I do? </summary>

This happens because of caching in our CDN. An edit/publish flow will fully flush the CDN cache, though we don't currently do that for every edit at the API layer.&#x20;

One way to verify that you're experiencing a CDN cache issue is to look at the model in a private or incognito window. Authenticated users will bypass the cache but anonymous viewers will not. If this is the case, changes should be visible to everyone within an hour.&#x20;

</details>

<details>

<summary>Can I manipulate a 3D mesh of a model with the API?</summary>

No, the API can only currently get and set model details, assets, Mattertags, labels, and bundles.

</details>

<details>

<summary>How do I query all models with Python using requests? </summary>

Use the query below:&#x20;

```
import requests 

token = 'Your API token' 
secret = 'Your secret API token' 
endpoint = 'https://api.matterport.com/api/models/graph'
query = { 'query' :
    '''
    query {
      models(query: "*"){
        totalResults
        results{ id }
      }
    }
    '''
}
auth = (token, secret)
headers = {'content-type': 'application/json', 'accept':'gzip'}
r = requests.post(endpoint, json=query, auth=auth, headers=headers) 

if(r.ok):
    print(r.json())
else: 
    print(r.status_code)
```

</details>

<details>

<summary>How do I query all models with Node.js using fetch?</summary>

<pre><code><strong>const { default: fetch } = require("node-fetch");
</strong>
const token = "Your API token";
const secret = "Your secret API token";

const auth = Buffer.from(token + ':' + secret).toString('base64');

const endpoint = "https://api.matterport.com/api/models/graph";

const body = JSON.stringify({
  query: `
    query {
      models(query: "*"){
        totalResults
        results{ id }
      }
    }
  `
});

fetch(endpoint, {
  method: 'POST',
  headers: {
    'Authorization': `Basic ${auth}`,
    'Content-type': 'application/json'
  },
  body: body,
})
.then(res => res.json())
.then(data => console.log(data))</code></pre>

</details>

<details>

<summary>I'm a collaborator with Admin editing privileges for an organization - why can't I query any models on the account? </summary>

If you are set as a collaborator (as opposed to an admin), you cannot access models through the API. If you need access, you have two options:&#x20;

1. Request that an account admin transfers the space to you.
2. Have the admin of the account share their API tokens with you.
   * An API token will give you access to every model that belongs to the admin's account.&#x20;

</details>

<details>

<summary>Why can't I access my MatterPak™ bundle after unlocking it?</summary>

MatterPaks™ require a few minutes to be generated for a space. Once the unlock is requested, please allow up to **15 minutes** before querying for the MatterPak™ Bundle.

</details>

<details>

<summary>How do I update embedded media within a Mattertag?</summary>

To add or update rich media content, you have to use the updateMattertagMediaUrl() mutation. If you want to remove rich media content, you must use the removeMattertagMedia() mutation. \
\
The GraphQL Schema does show that addMattertag() and patchMattertag() can update "media" and "mediaType." However, at this time, it's not possible to directly update these values if you're using rich media content.&#x20;

</details>
