# Home

{% hint style="info" %}
**Important:**  Tags 2.0 will become the new default soon, replacing Mattertags.

We will continue to support Mattertags (Tags 1.0) until March 1, 2023, after which Tags 2.0 will become the only available implementation.  Until that date, by including an `&applicationKey` URL parameter, the default Tag implementation will remain Mattertags.

This mostly only affects visuals. All SDK functionality provided by the `Mattertag` namespace will continue to work as is with Tags 2.0\

{% endhint %}

### Latest Version

**SDK Bundle**

| SDK Release  | [3.1.64.4-0-gea16b080c2](https://static.matterport.com/showcase-sdk/bundle/3.1.64.4-0-gea16b080c2/showcase-bundle.zip) |
| ------------ | ---------------------------------------------------------------------------------------------------------------------- |
| Last Updated | **Apr 11, 2022**                                                                                                       |

**Early Access**

| SDK Early Access | [3.1.75.3-0-gba9de22f6d](https://static.matterport.com/showcase-sdk/bundle/3.1.75.3-0-gba9de22f6d/showcase-bundle.zip) |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Last Updated     | **Sep 13, 2022**                                                                                                       |

### What is the SDK Bundle?

It is an extension of the SDK for Embeds and provides a framework for deep third-party integration with Matterport models. You get direct access to the 3d engine, renderer, scene graph and more.

### How do I obtain an SDK key?

Our developer tools are now out of beta and all accounts are now enabled to generate sandboxed SDK keys. You can find your key management by navigating to your [Account Settings -> Developer Tools](https://my.matterport.com/settings/account/devtools). To learn more about our developer tools, please visit the [Matterport Developer Tools and Pricing](https://support.matterport.com/hc/en-us/articles/360057506813-Matterport-Developer-Tools-Pricing-and-Availability)

&#x20;**Note:** Code snippets in the SDK Bundle pages are in typescript. Visit [https://www.typescriptlang.org](https://www.typescriptlang.org/) to learn more about typescript.

#### 8-4-2022

* A new [Early Access](early-access-releases/) build that requires manually opting into Tags 2.0 is now available.

#### 6-30-2022

* Updated [Early Access](broken-reference) with bug fixes and new Tags 2.0 features

#### 6-7-2022

* A new [Early Access](early-access-releases/) build with a focus on Tags 2.0 is now available

#### 4-11-2022

* Fixed an issue with deep links not taking you to the correct pose in Tags
* Download [SDK Bundle version: 3.1.64.4-0-gea16b080c2](https://static.matterport.com/showcase-sdk/bundle/3.1.64.4-0-gea16b080c2/showcase-bundle.zip)

#### 3-15-2022

* Fixed some issues with Space Search
* Download [SDK Bundle version: 3.1.63.0-125-g1fd7fd3bed](https://static.matterport.com/showcase-sdk/bundle/3.1.63.0-125-g1fd7fd3bed/showcase-bundle.zip)

#### 3-11-2022

* Added iterability to [`Dictionary`](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/dictionary.html#\_symbol\_iterator\_) returned in [`IMapObserver`](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/imapobserver.html)
* Added pathfinding support
  * Added the [`Graph`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/graph.html) namespace for creating connectivity graphs and traversing them using A\*
  * Added the ability to create [Sweep graphs](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/sweep.html#creategraph)
  * See [Pathfinding](https://matterport.github.io/showcase-sdk/sdkbundle\_pathfinding.html) for more info
* Added the [Link](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/link.html) namespace
  * Added the ability to create share links through [Link.createLink](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/link.html#createlink) and [Link.createDeepLink](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/link.html#createdeeplink)
  * Added the ability to change the link in the share dialog through [Link.setShareLinkPolicy](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/link.html#setsharelinkpolicy)
  * Added the ability to change the click handler for different link types through [policies](https://matterport.github.io/showcase-sdk/docs/reference/current/enums/link.openpolicy.html) for example [Link.setModelLinkPolicy](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/link.html#setmodellinkpolicy)
* Fixed some missing and inconsistent types
  * Added type [PredefinedOutputs](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/scene.html#predefinedoutputs) for component output intersection types
  * Added the [InteractionEvent](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/scene.html#interactionevent) type for the mesh interaction callback payload.
  * [INode.bind](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.icomponent.html#bind) now has the correct type. This function is deprecated.
* Added [componentIterator](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.inode.html#componentiterator) method to `INode`
* Added [componentType](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.icomponent.html#componenttype) property to `IComponent`
* Added [nodeIterator](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.iobject.html#nodeiterator) to `IObject`
* Download [SDK Bundle version: 3.1.63.0-123-g4739265d9f](https://static.matterport.com/showcase-sdk/bundle/3.1.63.0-123-g4739265d9f/showcase-bundle.zip)

#### 12-6-2021

* Added [OAuth support](https://matterport.github.io/showcase-sdk/sdkbundle\_tutorials\_using\_oauth.html). Contact [Developer Support](mailto:developer@matterport.com) to enable OAuth for your application.
* Fixed an issue where `Mattertag.remove` would not remove an array of mattertags.
* Fixed an issue where `Mattertag.registerIcon` would not throw exceptions after an error occurred.
* Fixed an issue where an interrupted inside mode navigation would display the model correctly.
* Fixed an issue where a user could not navigate to a floor under a hidden floor.
* Fixed an issue where `Pointer.intersection` would not return the correct type for a mattertag.
* Download [SDK Bundle version: 3.1.51.7-84-g0dcbe0591](https://static.matterport.com/showcase-sdk/bundle/3.1.51.7-84-g0dcbe0591/showcase-bundle.zip)

#### 8-25-2021

* Update threejs transform controls to version 129.
* Fix an issue where Sweep.moveTo would ignore the transitionTime option.
* Download [SDK Bundle version: 3.1.46.18-6-gbc4c5114b](https://static.matterport.com/showcase-sdk/bundle/3.1.46.18-6-gbc4c5114b/showcase-bundle.zip)

#### 8-5-2021

* Fixed an issue where a share link would not link to matterport.com
* Fixed an issue where `Scene.serialize` would return undefined
* Fixed an issue preventing the use of the my.matterportvr.cn api domain.
* Fixed an issue where model loader components would not remove meshes from the scene when stopped.
* Mobile redirects were removed. You can re-enable redirects by setting `disableMobileRedirect` to false in your app config.
* Added the Scene namespace to the sdk type definitions.
* Added scene objects. See [Using scene objects](https://matterport.github.io/showcase-sdk/sdkbundle\_tutorials\_using\_scene\_objects.html) and [Scene.createobjects](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/scene.html#createobjects)
* [Scene.serialize](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/scene.html#serialize) now serializes to version 2. [Scene.deserialize](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/scene.html#deserialize) takes both version 1 and 2 scene files.
* Updated embedded three.js to version r128
* Download [SDK Bundle version: 3.1.46.18-2-g2386aca5f](https://static.matterport.com/showcase-sdk/bundle/3.1.46.18-2-g2386aca5f/showcase-bundle.zip)

#### 6-17-2021

* Fixed missing `App` namespace enums
* Download [SDK Bundle version: 3.1.42.14-24-gb057e5145](https://static.matterport.com/showcase-sdk/bundle/3.1.42.14-24-gb057e5145/showcase-bundle.zip)

#### 6-16-2021

* Added `Room.current` observable\

* Maintenance bug fixes and improvements.
* Download [SDK Bundle version: 3.1.42.14-22-g7fd9ebd24](https://static.matterport.com/showcase-sdk/bundle/3.1.42.14-22-g7fd9ebd24/showcase-bundle.zip)

#### 5-27-2021

* Maintenance bug fixes and improvements.
* Download [SDK Bundle version: 3.1.41.5-19-g5133fdd3e](https://static.matterport.com/showcase-sdk/bundle/3.1.41.5-19-g5133fdd3e/showcase-bundle.zip)

#### 4-21-2021

* Fixed a CORS issue when using the bundle on a custom domain.
* Download [SDK Bundle version: 3.1.38.10-15-g5a5323ef0](https://static.matterport.com/showcase-sdk/bundle/3.1.38.10-15-g5a5323ef0/showcase-bundle.zip)

#### 4-16-2021

* Interface version updated to 3.10
* Added scene parameter to ‘Scene.configure’ callback.
* Added ‘INTERACTION.DRAG\_BEGIN’ and ‘INTERACTION.DRAG\_END’ events to scene node colliders.
* Added ‘colliderEnabled\` boolean to the gltf, fbx, dae and obj model loaders.
* Download [SDK Bundle version: 3.1.38.10-14-gaf0ef87a5](https://static.matterport.com/showcase-sdk/bundle/3.1.38.10-14-gaf0ef87a5/showcase-bundle.zip)

#### 3-2-2021

* Fixed an issue with Mattertag.injectHTML
* Download: [SDK Bundle version: 3.1.35.16-9-g01b2a7b60](https://static.matterport.com/showcase-sdk/bundle/3.1.35.16-9-g01b2a7b60/showcase-bundle.zip)

#### 2-24-2021

* Interface version updated to 3.9
* Added [Sensor](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/sensor.html) namespace.
* Download: [SDK Bundle version: 3.1.35.16-8-ga7993a5c3](https://static.matterport.com/showcase-sdk/bundle/3.1.35.16-8-ga7993a5c3/showcase-bundle.zip)

#### 2-16-2021

* Updated embedded three.js to version r124
* Fixed an issue with disabling measurement mode.
* Fixed an issue with password submission on password protected spaces.
* Fixed an issue with drag gesture ending prior to pointer release(improves transform control and mesh dragging).
* Added optional effect composer. You must set useEffectComposer: true in the application config object in showcase.html.
* Added [Scene.configure](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/scene.html#configure) function.
* Download: [SDK Bundle version: 3.1.33.13-14-gb10ecafc1](https://static.matterport.com/showcase-sdk/bundle/3.1.33.13-14-gb10ecafc1/showcase-bundle.zip)

#### 2-3-2021

* Interface version updated to 3.8.
* Added input data to mesh CLICK, HOVER, and DRAG interactions.
* Fixed an issue with the appearance of password protected spaces.
* Fixed an issue with toggling measurement mode.
* Download: [SDK Bundle version: 3.1.28.5-4-g911543b43](https://static.matterport.com/showcase-sdk/bundle/3.1.28.5-4-g911543b43/showcase-bundle.zip)

#### 12-11-2020 General Availability&#x20;

* Components: Added `unfiltered` property to [mp.input](https://matterport.github.io/showcase-sdk/sdkbundle\_components\_input.html) component.
* Additional setup instructions for application keys required for CORS, see [Set your application key](https://matterport.github.io/showcase-sdk/sdkbundle\_tutorials\_setup.html#set-your-application-key.html)
* Fixed an issue with where Sweep.data would return no sweeps.
* Download: [SDK Bundle version: 3.1.16.9-17-gacf9fb85e](https://static.matterport.com/showcase-sdk/bundle/3.1.16.9-17-gacf9fb85e/showcase-bundle.zip)

#### 11-6-2020

* Scene: Added support for creating arrays of components and nodes. See [Scene.registerComponents](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/scene.html#registercomponents) and [Scene.createNodes](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/scene.html#createnodes).
* Components: Fixed an issue where mp.input would not dispatch a models `INTERACTION.CLICK` event.
* General: Fixed an sdk connection issue on the oculus browser. You can now connect to the sdk while in xr immersive mode. See [Using xr](https://matterport.github.io/showcase-sdk/sdkbundle\_tutorials\_using\_xr.html)
* Added the `mp.xr` component which provides an XRSession. See [mp.xr](https://matterport.github.io/showcase-sdk/sdkbundle\_components\_xr.html)
* Download: [SDK Bundle version: 3.1.10.3-30-g034a60845](https://static.matterport.com/showcase-sdk/bundle/3.1.10.3-30-g034a60845/showcase-bundle.zip)

#### 9-25-2020

* General: Added support for a custom embedly key. Mattertag videos and images can now be viewed with bundle applications. See [Setting up Embedly](https://matterport.github.io/showcase-sdk/sdkbundle\_tutorials\_setting\_up\_embedly.html)
* Conversion: Fixed an issue where Conversion.worldToScreen returned stale screen coordinates.
* Components: Added support for arrays as inputs.
* Added `showX`, `showY`, `showZ` and `size` to [mp.transformControls](https://matterport.github.io/showcase-sdk/sdkbundle\_components\_transformcontrols.html) inputs.
* Download: [SDK Bundle version: 3.1.8.2-12-g86e1cdce6](https://static.matterport.com/showcase-sdk/bundle/3.1.8.2-12-g86e1cdce6/showcase-bundle.zip)

#### 8-13-2020

* Added [mp.input](https://matterport.github.io/showcase-sdk/sdkbundle\_components\_input.html), [mp.camera](https://matterport.github.io/showcase-sdk/sdkbundle\_components\_camera.html), and [mp.transformControls](https://matterport.github.io/showcase-sdk/sdkbundle\_components\_transformcontrols.html) components.
* Inspector: added component list panel, 6DOF camera controls. Source code updated.
* General: Includes SDK for embeds v3.5 features and bug fixes.
* General: Fixed an issue where mattertags and labels were being loaded from localhost.
* General: Fixed an issue where textures were not properly loaded on safari.
* Download: [SDK Bundle version: 3.1.6.1-15-ged398ca2e](https://static.matterport.com/showcase-sdk/bundle/3.1.6.1-15-ged398ca2e/showcase-bundle.zip)

#### 7-31-2020

* Models: Fixed an issue with loading OBJ models with a material.
* Scenes: Fixed an issue with orphaned colliders from deleted scene nodes.
* Download: [SDK Bundle version: 3.1.4.1-6-gac2d8cfea](https://static.matterport.com/misc/bundle/showcase/3.1.4.1-6-gac2d8cfea/showcase-bundle.zip)

#### 6-23-2020

* Maintenance update includes SDK for embeds v3.4 features and bug fixes.
* Download: [SDK Bundle version: 3.1.1.8-0-g023d0d5c6](https://static.matterport.com/misc/bundle/showcase/3.1.1.8-0-g023d0d5c6/showcase-bundle.zip)

#### 5-13-2020

* Added event spies to components. See [Event Spies Overview](https://matterport.github.io/showcase-sdk/sdkbundle\_architecture.html#event-spies) and [Event Spies Reference](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.icomponent.html#spyonevent).
* Internal Three.js version upgraded to 0.115.0
* Download: [SDK Bundle version: 3.0.35.31-25-g9563c7a6c](https://static.matterport.com/misc/bundle/showcase/3.0.35.31-25-g9563c7a6c/showcase-bundle.zip)

#### 4-10-2020

* Models: Web workers load textures in the background.
* Models: Added `loadingState` property to the output of the gltf, dae, fbx, and obj loaders.
* Models: Fixed an issue where reloading models would not release resources.
* Scenes: Scene files support property and event bindings.
* Scenes: Scene files support multiple components per node.
* Components: Added most of the three/js/examples to the component context.
* Fixed a startup race condition with createNode.

#### 2-6-2020

* Fixed an issue where transform controls interrupted camera motion.

#### 1-30-2020

* Added light objects: `mp.ambientLight`, `mp.directionalLight`, and `mp.pointLight`.
* Added support for objects as component inputs.
* Fixed an issue where `onInteraction` would not fire if the collider was a Mesh object.
* Fixed a bug with the github showcase-sdk-tutorial repo where the app would load the bundle twice. [github showcase-sdk-tutorial link](https://github.com/matterport/showcase-sdk-tutorial).

#### 12-20-2019

* First release

\
