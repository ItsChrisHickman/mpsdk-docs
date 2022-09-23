# Sample Queries

This library of sample queries and mutations provide are ready-to-use GraphQL queries that can be tested in our interactive console and integrated into your applications.

If you are needing assistance with building queries, contact us at [developer@matterport.com](mailto:developer@matterport.com)

Model API has two queries -- models and model. &#x20;

<details>

<summary>Search for your models</summary>

```graphql
query {
models(query: "*") {
    totalResults
     results {
      id
      name
      description
    }
  }
}
```

[Try this query in our interactive console](https://api.matterport.com/api/graphiql/?query=query%20%7B%0Amodels\(query%3A%20%22\*%22\)%20%7B%0A%20%20%20%20totalResults%0A%20%20%20%20%20results%20%7B%0A%20%20%20%20%20%20id%0A%20%20%20%20%20%20name%0A%20%20%20%20%20%20description%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A)

Sample Response

```json
{
  "data": {
    "models": {
      "totalResults": 1,
      "results": [
        {
          "id": "MODEL_ID",
          "name": "352 E Java Dr",
          "description": ""
        }
      ]
    }
  }
}
```

</details>

<details>

<summary>Buy a Matterpak</summary>

Use the timed URL from the response to download the MatterPak

```graphql
mutation buyMatterpak($modelId: ID!){
  unlockModelBundle(
    id: $modelId, 
    bundleId: "mp:matterpak"
  ) {
    id
	name
	description
	availability
	assets { url }
  }
}
```

[Try this query in our interactive console.](https://api.matterport.com/api/graphiql/?query=mutation%20buyMatterpak\(%24modelId%3A%20ID!\)%7B%0A%20%20unlockModelBundle\(%0A%20%20%20%20id%3A%20%24modelId%2C%20%0A%20%20%20%20bundleId%3A%20%22mp%3Amatterpak%22%0A%20%20\)%20%7B%0A%20%20%20%20id%0A%09name%0A%09description%0A%09availability%0A%09assets%20%7B%20url%20%7D%0A%20%20%7D%0A%7D%0A\&variables=%7B%0A%20%20%22modelId%22%3A%20%22%22%0A%7D\&operationName=buyMatterpak)

Sample Response:

```json
{
  "data": {
   "unlockModelBundle": {
      "id": "mp:matterpak",
      "name": "Matterpak",
      "description": "Order high resolution assets associated with the model.",
      "availability": "unlocked",
      "assets": [
         {
"url": "https://qa-cdn-1.matterport.com/models/group_77/job_62927cc2-7552-4aad-8330-3904c5198354/wf_39d3f0f8baae4fc9aaeb6326edf55d8f/mesh/1.1.466.14860/2016-11-09_0240.05/62927cc275524aad83303904c5198354.zip?t=2-b3da2c89760c80f1671bc260d678d949f29bd8a8-1573485841-1"

         }
      ]
    }
  }
}
```

</details>

<details>

<summary>Get all Sweep Locations and Panoramic Images</summary>

Panoramic images are currently only available as **skyboxes.**&#x20;

A skybox is made out of six images - each image individually projected onto the shape of a cube - that is: **top**, **bottom**, **left**, **right**, **front** and **back** sides. Skyboxes are abailable in 2K and come bundled with position and rotation data.&#x20;

```graphql
fragment panoFragment on PanoramicImageLocation{
  id
  skybox {
    id
    status
    format
    children
  }
}

query getSweeps($modelId: ID!){
    model(id: $modelId) {
      locations {
        id
        model { id }
        position { x, y, z }
        floor { id }
        room { id }
        panos { ...panoFragment }
            
    }
  }
}

```

[Try this query in our interactive console](https://api.matterport.com/api/graphiql/?query=fragment%20panoFragment%20on%20PanoramicImageLocation%7B%0A%20%20id%0A%20%20skybox%20%7B%0A%20%20%20%20id%0A%20%20%20%20status%0A%20%20%20%20format%0A%20%20%20%20children%0A%20%20%7D%0A%7D%0A%0Aquery%20getSweeps\(%24modelId%3A%20ID!\)%7B%0A%20%20%20%20model\(id%3A%20%24modelId\)%20%7B%0A%20%20%20%20%20%20locations%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20model%20%7B%20id%20%7D%0A%20%20%20%20%20%20%20%20position%20%7B%20x%2C%20y%2C%20z%20%7D%0A%20%20%20%20%20%20%20%20floor%20%7B%20id%20%7D%0A%20%20%20%20%20%20%20%20room%20%7B%20id%20%7D%0A%20%20%20%20%20%20%20%20panos%20%7B%20...panoFragment%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A\&variables=%7B%0A%20%20%22modelId%22%3A%20%22%22%0A%7D\&operationName=getSweeps)

Sample Response:

```
{
  "data": {
    "model": {
      "locations": [
        {
          "id": "a0723324-ab3e-4500-bdee-8fec13d3ae9d",
          "model": {
            "id": "MODEL_ID"
          },
          "position": {
            "x": 0,
            "y": 0,
            "z": 0
          },
          "panos": [
            {
              "id": "a0723324-ab3e-4500-bdee-8fec13d3ae9d",
              "skybox": {
                "id": "a0723324-ab3e-4500-bdee-8fec13d3ae9d",
                "status": "available",
                "format": "skybox",
                "children": [
                  "https://qa-cdn-1.matterport.com/models/1a56eedeff7d4a7481b961c009ae9236/assets/pan/~/high/a0723324ab3e4500bdee8fec13d3ae9d_skybox0.jpg?t=2-c81c9af53e390d7c5d9946f73a74665f0e06757c-1573701898-1",
                  "https://qa-cdn-1.matterport.com/models/1a56eedeff7d4a7481b961c009ae9236/assets/pan/~/high/a0723324ab3e4500bdee8fec13d3ae9d_skybox1.jpg?t=2-c81c9af53e390d7c5d9946f73a74665f0e06757c-1573701898-1",
                  "https://qa-cdn-1.matterport.com/models/1a56eedeff7d4a7481b961c009ae9236/assets/pan/~/high/a0723324ab3e4500bdee8fec13d3ae9d_skybox2.jpg?t=2-c81c9af53e390d7c5d9946f73a74665f0e06757c-1573701898-1",
                  "https://qa-cdn-1.matterport.com/models/1a56eedeff7d4a7481b961c009ae9236/assets/pan/~/high/a0723324ab3e4500bdee8fec13d3ae9d_skybox3.jpg?t=2-c81c9af53e390d7c5d9946f73a74665f0e06757c-1573701898-1",
                  "https://qa-cdn-1.matterport.com/models/1a56eedeff7d4a7481b961c009ae9236/assets/pan/~/high/a0723324ab3e4500bdee8fec13d3ae9d_skybox4.jpg?t=2-c81c9af53e390d7c5d9946f73a74665f0e06757c-1573701898-1",
                  "https://qa-cdn-1.matterport.com/models/1a56eedeff7d4a7481b961c009ae9236/assets/pan/~/high/a0723324ab3e4500bdee8fec13d3ae9d_skybox5.jpg?t=2-c81c9af53e390d7c5d9946f73a74665f0e06757c-1573701898-1"
                ]
              }
            }
          ]
        },
        {
…
```

</details>

<details>

<summary>Get all Mattertags and Locations</summary>

```graphql
query getMattertags($modelId: ID!){
    model(id: $modelId) {
      mattertags {
          id 
          label
          description
          media
          position {x, y, z}
      }
  }
}
```

[Try this query in our interactive console](https://api.matterport.com/api/graphiql/?query=query%20getMattertags\(%24modelId%3A%20ID!\)%7B%0A%20%20%20%20model\(id%3A%20%24modelId\)%20%7B%0A%20%20%20%20%20%20mattertags%20%7B%0A%20%20%20%20%20%20%20%20%20%20id%20%0A%20%20%20%20%20%20%20%20%20%20label%0A%20%20%20%20%20%20%20%20%20%20description%0A%20%20%20%20%20%20%20%20%20%20media%0A%20%20%20%20%20%20%20%20%20%20position%20%7Bx%2C%20y%2C%20z%7D%0A%20%20%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A\&variables=%7B%0A%20%20%22modelId%22%3A%20%22%22%0A%7D\&operationName=getMattertags)

Sample Response

```
{
  "data": {
    "model": {
      "mattertags": [
        {
          "id": $modelId,
          "label": "Nest Thermostat",
          "description": "",
          "media": "https://www.youtube.com/watch?v=vgowFxYI8PI",
          "position": {
            "x": -1.20415628,
            "y": -5.35434341,
            "z": 3.1942153
          }
        },
        {…
```

</details>

<details>

<summary>Ordering and Retrieving Schematic Floor Plans</summary>

Floor plan assets won't be available until our floor plan team returns it (normal speed is about 2 days).

```graphql
mutation buyFloorplan($modelId: ID!){
  unlockModelBundle(
    id: $modelId,
    bundleId: "cubicasa:floorplan",
    options: { deliverySpeed: normal }
  ){
    id
    name
    description
    availability
    assets { url }
  }
}
```

[Try this mutation in our interactive console](https://api.matterport.com/api/graphiql/?query=mutation%20buyFloorplan\(%24modelId%3A%20ID!\)%7B%0A%20%20unlockModelBundle\(%0A%20%20%20%20id%3A%20%24modelId%2C%0A%20%20%20%20bundleId%3A%20%22cubicasa%3Afloorplan%22%2C%0A%20%20%20%20options%3A%20%7B%20deliverySpeed%3A%20normal%20%7D%0A%20%20\)%7B%0A%20%20%20%20id%0A%20%20%20%20name%0A%20%20%20%20description%0A%20%20%20%20availability%0A%20%20%20%20assets%20%7B%20url%20%7D%0A%20%20%7D%0A%7D%0A\&variables=%7B%0A%20%20%22modelId%22%3A%20%22%22%0A%7D\&operationName=buyFloorplan)

#### Find the Available Delivery Speeds for Ordering Schematic Floorplan

```
query getSupportedFloorplanDeliverySpeeds($modelId: ID!) {
   model(id: $modelId) {
  	bundle(id: "cubicasa:floorplan") {
     	supportedOptions { deliverySpeeds }
  	}
   }
}
```

[Try this query in our interactive console](https://api.matterport.com/api/graphiql/?query=query%20getSupportedFloorplanDeliverySpeeds\(%24modelId%3A%20ID!\)%20%7B%0A%20%20%20model\(id%3A%20%24modelId\)%20%7B%0A%20%20%09bundle\(id%3A%20%22cubicasa%3Afloorplan%22\)%20%7B%0A%20%20%20%20%20%09supportedOptions%20%7B%20deliverySpeeds%20%7D%0A%20%20%09%7D%0A%20%20%20%7D%0A%7D%0A\&variables=%7B%0A%20%20%22modelId%22%3A%20%22%22%0A%7D\&operationName=getSupportedFloorplanDeliverySpeeds)

```
fragment asset on Asset{
  id
  url
  validUntil
  format
  filename
  status
}

query getBundleAssets($modelId: ID!){
  model(id: $modelId) {
    bundles {
      id
      availability
      name
      description
      assets { ...asset }
      supportedOptions {
        deliverySpeeds
      }
    }
  }
}
```

[Try this query in our interactive console](https://api.matterport.com/api/graphiql/?query=fragment%20asset%20on%20Asset%7B%0A%20%20id%0A%20%20url%0A%20%20validUntil%0A%20%20format%0A%20%20filename%0A%20%20status%0A%7D%0A%0Aquery%20getBundleAssets\(%24modelId%3A%20ID!\)%7B%0A%20%20model\(id%3A%20%24modelId\)%20%7B%0A%20%20%20%20bundles%20%7B%0A%20%20%20%20%20%20id%0A%20%20%20%20%20%20availability%0A%20%20%20%20%20%20name%0A%20%20%20%20%20%20description%0A%20%20%20%20%20%20assets%20%7B%20...asset%20%7D%0A%20%20%20%20%20%20supportedOptions%20%7B%0A%20%20%20%20%20%20%20%20deliverySpeeds%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A\&variables=%7B%0A%20%20%22modelId%22%3A%20%22%22%0A%7D\&operationName=getBundleAssets)

#### **Retrieve the assets**

```
query getFloorplan($modelId: ID!) {
  model(id: $modelId) {
    bundle(id: "cubicasa:floorplan") {
      assets { url }
    }
  }
}
```

[Try this query in our interactive console](https://api.matterport.com/api/graphiql/?query=query%20getFloorplan\(%24modelId%3A%20ID!\)%20%7B%0A%20%20model\(id%3A%20%24modelId\)%20%7B%0A%20%20%20%20bundle\(id%3A%20%22cubicasa%3Afloorplan%22\)%20%7B%0A%20%20%20%20%20%20assets%20%7B%20url%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A\&variables=%7B%0A%20%20%22modelId%22%3A%20%22%22%0A%7D\&operationName=getFloorplan)

</details>

<details>

<summary>Find the Different Purchase Options for Any Bundle</summary>

```graphql
query getSupportedOptions($modelId: ID!) {
   model(id: $modelId) {
      bundles {
         supportedOptions { 
         measurementUnits
         deliverySpeeds 
         }
      }
   }
}
```

[Try this query in our interactive console](https://api.matterport.com/api/graphiql/?query=query%20getSupportedOptions\(%24modelId%3A%20ID!\)%20%7B%0A%20%20%20model\(id%3A%20%24modelId\)%20%7B%0A%20%20%09bundles%20%7B%0A%20%20%20%20%20%09supportedOptions%20%7B%20%0A%20%20%20%20%20%20%20%20measurementUnits%0A%20%20%20%20%20%20%20%20deliverySpeeds%20%0A%20%20%20%20%20%20%7D%0A%20%20%09%7D%0A%20%20%20%7D%0A%7D%0A\&variables=%7B%0A%20%20%22modelId%22%3A%20%22%22%0A%7D\&operationName=getSupportedOptions)

</details>

<details>

<summary>Get the Colored Rooms Floorplan URL</summary>

```graphql
query getColoredRooms($modelId: ID!){
 model(id: $modelId) {
    assets {
      floorplans(provider: "matterport", flags: [colored_rooms]) {
        provider
        format
        flags
        id
        url
      }
    }
  }
}
```

[Try this query in our interactive console](https://api.matterport.com/api/graphiql/?query=query%20getColoredRooms\(%24modelId%3A%20ID!\)%7B%0A%20model\(id%3A%20%24modelId\)%20%7B%0A%20%20%20%20assets%20%7B%0A%20%20%20%20%20%20floorplans\(provider%3A%20%22matterport%22%2C%20flags%3A%20%5Bcolored\_rooms%5D\)%20%7B%0A%20%20%20%20%20%20%20%20provider%0A%20%20%20%20%20%20%20%20format%0A%20%20%20%20%20%20%20%20flags%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20url%0A%20%20%20%20%20%20%7D%0A%20%20%09%7D%0A%09%7D%0A%7D%0A\&variables=%7B%0A%20%20%22modelId%22%3A%20%22%22%0A%7D\&operationName=getColoredRooms)

</details>

<details>

<summary>Toggle Model Visibility</summary>

```graphql
mutation toggleModelVisibility($modelId: ID!, $visibility: ModelVisibility!){
  updateModelVisibility(
    id: $modelId,
    visibility: $visibility
  ){
    id
  }
}
```

[Try this mutation in our interactive console](https://api.matterport.com/api/graphiql/?query=mutation%20toggleModelVisibility\(%24modelId%3A%20ID!%2C%20%24visibility%3A%20ModelVisibility!\)%7B%0A%20%20updateModelVisibility\(%0A%20%20%20%20id%3A%20%24modelId%2C%0A%20%20%20%20visibility%3A%20%24visibility%0A%20%20\)%7B%0A%20%20%20%20id%0A%20%20%7D%0A%7D%0A%0A\&variables=%7B%0A%20%20%22modelId%22%3A%20%22%22%2C%0A%20%20%22visibility%22%3A%20%22private%22%0A%7D\&operationName=toggleModelVisibility)

</details>

<details>

<summary>Toggle Model Activation (archive / activate)</summary>

```graphql
mutation toggleModelActivation($modelId: ID!, $state: ModelStateChange!){
  updateModelState(
    id: $modelId,
    state: $state
  ){
    id
  }
}
```

[Try this mutation in our interactive console](https://api.matterport.com/api/graphiql/?query=mutation%20toggleModelActivation\(%24modelId%3A%20ID!%2C%20%24state%3A%20ModelStateChange!\)%7B%0A%20%20updateModelState\(%0A%20%20%20%20id%3A%20%24modelId%2C%0A%20%20%20%20state%3A%20%24state%0A%20%20\)%7B%0A%20%20%20%20id%0A%20%20%7D%0A%0A%7D%0A\&variables=%7B%0A%20%20%22modelId%22%3A%20%22%22%2C%0A%20%20%22state%22%3A%20%22inactive%22%0A%7D\&operationName=toggleModelActivation)

</details>
