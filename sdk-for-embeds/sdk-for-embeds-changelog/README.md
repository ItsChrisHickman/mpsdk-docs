# SDK for Embeds Changelog

### 22.9.1

**Sep 13, 2022**

If opted into Tags 2.0

* Fixed an issue where [`Tag.allowAction`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tag.html#allowaction) would throw an error if called to early
* Fixed an issue with [`Mattertag.add`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag.html#add) when using a media type of `MediaType.NONE`
* Fixed `media.src` returned in the items of [`Mattertag.data`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag.html#data)

### 22.6.1

**Jun 30, 2022**

* Added [Mattertag.editStem](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag.html#editstem) to control the stem’s length and/or visibility
* Updated [Asset.registerTexture](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/asset.html#registertexture) to now also work when setting the pointer’s texture using [Pointer.editTexture](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/pointer.html#edittexture)
* Updated [Early Access](https://matterport.github.io/showcase-sdk/earlyaccess\_home.html) for Tags 2.0

### 22.5.1

**Jun 7, 2022**

* Added [Label.data](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/label.html#data) collection to receive Labels data
* Added [Tour.currentStep](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tour.html#currentstep), [Tour.transition](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tour.html#transition), and [Tour.state](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tour.html#state) to get information about what the tour is currently doing
* Added [Mode.current](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mode.html#current) and [Mode.transition](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mode.html#transition-1) to get information about the current view mode and any transitions between them taking place
* Added [Asset.registerTexture](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/asset.html#registertexture) to be used as a central place for registering icons like those for Mattertags
* [Early Access](https://matterport.github.io/showcase-sdk/earlyaccess\_home.html) for Tags 2.0

### 22.3.1

**Mar 17, 2022**

The previous Early Access is now closed and all features are now available generally available.

* Updated: [`Pointer`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/pointer.html) now has ways to control the reticle that follows the mouse pointer. [See the tutorial](https://matterport.github.io/showcase-sdk/sdk\_cursor.html).
* Updated: [`Graph`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/graph.html) namespace for pathfinding has improved watch-ability. [See the tutorial](https://matterport.github.io/showcase-sdk/sdk\_pathfinding.html).
* Added: [`Link`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/link.html) namespace to control how links are generated and how links are handled.

### 22.1.24

**Jan 24, 2022**

[Early Access](https://matterport.github.io/showcase-sdk/earlyaccess\_home.html) features that were previously only available in our Bundle SDK are now available in the Embed SDK as well.

* Added: [`Dictionary objects`](https://matterport.github.io/showcase-sdk/docs/earlyaccess/reference/interfaces/dictionary.html#\_symbol\_iterator\_) returned in [`IMapObserver`](https://matterport.github.io/showcase-sdk/docs/earlyaccess/reference/interfaces/imapobserver.html) are now iterable using `for...of` loops.
* Fixed: [Sweep.disable](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/sweep.html#disable) should now work regardless of the `useLegacyIds` param.
* Fixed: [Room.floorInfo](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/room.html#roomdata) should now be populated instead of always being an invalid floor.
* Early Access: [Graph and Pathfinding](https://matterport.github.io/showcase-sdk/earlyaccess\_21.12.1\_pathfinding.html); see the [Reference pages](https://matterport.github.io/showcase-sdk/docs/earlyaccess/reference/modules/graph.html).
* Early Access: [Pointer Reticle Customization](https://matterport.github.io/showcase-sdk/earlyaccess\_21.12.1\_cursor.html); see the [Reference pages](https://matterport.github.io/showcase-sdk/docs/earlyaccess/reference/modules/pointer.html).

### 3.11.1

**Sep 23, 2021**

* Updated: [Mattertag.registerIcon](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag.html#registericon) will now return the result of the fetch. Existing uses (that did not await the result) should not be affected.
* Fixed: [Mattertag.remove](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag.html#remove) can now properly remove an array of tags.
* Fixed: The [Mattertag.IMessenger](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/mattertag.imessenger.html) returned from [Mattertag.injectHTML](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag.html#injecthtml) will no longer see messages coming from the wrong tags.

### 3.11

**Jun 10, 2021**

* Added: [Room.current](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/room.html#current) observable.
* Added: [Typescript type declarations](https://matterport.github.io/showcase-sdk/sdk\_types.html).
* Fixed: `Sweep.Alignment` and `Sweep.Placement` are now properly under the `Sweep` namespace. Previously they were `Mode.Alignment` and `Mode.Placement`
* Removed: An interface version no longer needs to be specified when calling `connect`.

### v3.10

**Apr 1, 2021**

* Added: [Room.data](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/room.html#data) collection.
* Added: [Cylinder sources](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/sensor.html#createsource) for use with Sensors.
* Added: [Box sources](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/sensor.html#createsource) now support orientation.
* Fixed: `Mattertag.add` now properly sets its stem visible when undefined.
* Fixed: `Sweep.current` is more resilient to missing floor info.

### v3.9

**Feb 22, 2021**

* Added: [Sensors](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/sensor.html)
* Fixed: `Mattertag.editPosition` always giving a stem length of 1 meter.

### v3.8

**Jan 19, 2021**

* Added: [Floor.current](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/floor.html#data) observable
* Added: [Sweep.current](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/sweep.html#current) observable
* Added: [Sweep.enable](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/sweep.html#enable) and [Sweep.disable](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/sweep.html#disable)
* Fixed: `options.size` should now work again in [Mattertag.injectHTML](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag.html#injecthtml)

### v3.7

**Dec 21, 2020**

* Fix: Added `enabled`, `stemVisible` and `floorIndex` properties to [ObservableMattertagData](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag.html#observablemattertagdata) for backwards compatibility with `Mattertag.getData`
* Fix: Fixed an issue where observable collections would not return initial data
* Added: [Floor.data](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/floor.html#data) observable collection, deprecate `Floor.getData`
* Added: FloorInfo to `Label` and `SweepData`

### v3.6

**Dec 1, 2020**

* Added: `Mattertag.data` observable collection, deprecate `Mattertag.getData`
* Added: `onCollectionUpdated` to collection observers. `onCollectionUpdated` aggregates changes to a collection for more coarse, but less often updates
* Added: `views` option to `Renderer.takeScreenShot` to hide 360 views
* Fix: Failures to load replace tag icons via `Mattertag.editIcon` will now properly propagate errors
* Fix: Fallback dimensions are now provided for svgs used in `Mattertag.editIcon` – this should help in some cases where Firefox determines the size is 0x0
* Improved: More descriptive error messages around tagIds provided in most Mattertag calls

### v3.5

**Aug 5, 2020**

* Added `Mattertag.injectHTML` which allows embedding of custom HTML and Javascript, with sandboxed iframe limitations.

### v3.4

**June 23, 2020**

* Added `Camera.zoomBy`, `Camera.zoomTo`, and `Camera.zoomReset` to manipulate the zoom level of the camera in Panorama modes.
* Added `Camera.zoom` observable to get the zoom level of the camera while in Panorama mode.
* Added `Mattertag.editOpacity` to control opacity of each Mattertag.
* Added `Mattertag.preventAction` to disable Showcase’s default hover and click handlers allowing for the billboard to be hidden and/or the click to navigate to be suppressed.
* Added `Sweep.data` as a replacement for the `sweeps` property of `Model.getData`.
* Added `IObserver` support to `IObservable` for the more object-oriented programmer.
* Added transitionTime to `Sweep.moveTo` options.
* Fixed an issue with `Camera.setRotation` where certain orientations would rotate in the wrong direction.
* Fixed a race condition between `Mattertag.registerIcon` and `Mattertag.editIcon`.

### v3.3.1

**June 1, 2020**

* Added `Measurements.data` which allows you to detect when measurements are added, removed, and updated.
* Added `Mattertag.registerIcon` and `Mattertag.editIcon` function which allows you to change image used as mattertag discs.
* Added `Mattertag.resetIcon` to undo changes done by `Mattertag.editIcon`.

### v3.3

**May 19, 2020**

* Added `Measurements.mode` which allows you to detect when measurements mode is activated and deactivated.
* Added `Measurements.toggleMode` function which allows you to enable and disable showcase measurement mode.

### v3.2.3

**May 13, 2020**

* Fixed a race condition with `Camera.pose` and `Pointer.intersection` initialization.

### v3.2.2

**May 11, 2020**

* Added optional `floorId` parameter to `Mattertag.add` and `Mattertag.editPosition`.
* Added `floorId` to `Pointer.intersection` observable. This property can be used in with transient mattertags.

### v3.2.1

**Jan 30, 2020**

* Added `Mattertag.LINK_OPEN` event. This event fires when the user has clicked on an external mattertag link. See [Mattertag Events](https://matterport.github.io/showcase-sdk/docs/reference/current/index.html#on)
* Added `Camera.setRotation` function. This function sets the absolute rotation of the camera in inside mode.

### v3.2

**Dec 9, 2019**

* **Transient Mattertags**\
  Support for creating, updating and deleting mattertags. Changes to mattertags disappear once the user leaves showcase. Added `Mattertag.add`, `Mattertag.editColor`, `Mattertag.editBillboard`, `Mattertag.editPosition`, and `Mattertag.remove` See [Tutorials](https://matterport.github.io/showcase-sdk/sdk\_editing\_mattertags.html) section for help on editing transient mattertag content.
* **Synchronous Functions**\
  We are adding support for synchronous functions. These functions compute and return your data immediately, no promise involved. In general, synchronous functions are more performant since they dont directly interact with the showcase. Use them when you can. To start, we have selected a function that is called frequently `Renderer.getScreenPosition()`. This function is now being deprecated, and the new synchronous function is `Renderer.worldToScreen()`. In order to use synchronous functions, you will need to update your sdk client reference to `https://static.matterport.com/showcase-sdk/2.0.0-0-g7edd6b8/sdk.js`
* Added `Mattertag.getDiscPosition` synchronous function.
* Deprecating `window.SHOWCASE_SDK`, use `window.MP_SDK instead`.
* Update your iframe links. We are no longer using `/showcase-beta` in the iframe link, use `/show` e.g. `https://my.matterport.com/show?m=SxQL3iGyoDo&play=1`. See [Installation](https://matterport.github.io/showcase-sdk/sdk\_installation.html#include-the-library-and-add-a-matterport-space)

### v3.1

**Aug 22, 2019**

* Added `Camera.pose` observable property.
* `Camera.getPose()` is now deprecated. It will be removed in a future update.
* Added Pointer namespace and `Pointer.intersection` observable property

### v3.0.12.25

**May 3, 2019**

* Added colors and anchor points `Mattertag.MattertagData`

### v3.0.12.18

**April 25, 2019**

* Added `Measurements.getData()`. You can now access measurements created from Workshop!
* Added `App.getLoadTimes()`. You can now access app phase timing information!
* Added transition type parameter to `Mattertag.navigateToTag()`
* Removed `Mattertag.ActiveMattertagData` type
* Removed `Mattertag.Event.UPDATE`
* Added projection property to `Camera.getPose()`
* Added optional includeHiddenFloors parameter to `Renderer.getWorldPositionData()`
* Added `Renderer.takeEquirectangular()`

### v3.0.3.35

**June 27, 2018**

* New actions on camera, new namespaces for Renderer, and Settings
* [See a list of modified endpoints.](https://matterport.github.io/showcase-sdk/sdk\_upgrading.html#upgrading-from-v30-to-v30335)

### v3.0.0.196

**February 12, 2018**

* Renamed `toggle()` to `setActive()`
* Renamed `MattertagPositionData` to `ActiveMattertagData`
* Removed `HoverState` event, redundant with `Event.HOVER`
* Removed `SelectedState` event, use `Event.CLICK` instead\`
* Renamed `getMattertagData` to `getData`
* Removed `BoardState` enum.
* Added `MattertagData.isActive` property
* Added `TagDescriptionChunkType` enum
* Added `TagMediaType` enum
* Added `LinkType` enum
* Removed `MattertagData.floorIndex` property
* Removed `MattertagData.mode` property
* Removed `MattertagData.color` property
* Removed `MattertagData.anchorPosition` property
* Removed `MattertagData.stemVector` property
* Renamed `SweepInfo.newPano` to `SweepInfo.newSweep`
* Renamed `SweepInfo.oldPano` to `SweepInfo.oldSweep`
* Removed `ModelData.panos` property
* Removed `SweepData.modelSupportsVr` property
* Removed `SweepData.neighbourUUIDs` property
* Removed `SweepData.thumbnail` property
* Renamed `getModelData()` to `getData()`
* Renamed `getModelDetails() to` getDetails()\`
* Renamed `ModelDetails.contact_email` to `ModelDetails.contactEmail`
* Renamed `ModelDetails.contact_name` to `ModelDetails.contactName`
* Renamed `ModelDetails.formatted_address` to `ModelDetails.formattedAddress`
* Renamed `ModelDetails.formatted_contact_phone` to `ModelDetails.formattedContactPhone`
* Renamed `Pose.pano` to `Pose.sweep`
* Removed `rotateInDirection()` function
* Removed `Event.CHANGE` event
* Renamed `Event.PLAYING` to `Event.PHASE_CHANGE`

### v3.0

**December 4, 2017**

* New actions and events on floors, labels, and Mattertag™ Posts.
* New set of reference content that covers all actions and events.
* Version 1.x no longer supported. Version 2.0 skipped.
* [See a list of modified endpoints.](https://matterport.github.io/showcase-sdk/sdk\_upgrading.html#upgrading-from-v11-to-v30)

### v1.1

**August 10, 2017**

* Added `getPose` and `takeScreenShot` actions.
* Added pano thumbnails from the default pose into the metadata.

### v1.0

**February 16, 2017**

* Initial release of SDK. Focus on movement and the user’s location in the space.
