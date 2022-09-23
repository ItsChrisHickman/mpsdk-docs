# Early Access Releases

{% hint style="info" %}
**Important:**  Tags 2.0 will become the new default soon, replacing Mattertags.

We will continue to support Mattertags (Tags 1.0) until March 1, 2023, after which Tags 2.0 will become the only available implementation.  Until that date, by including an `&applicationKey` URL parameter, the default Tag implementation will remain Mattertags.

If you are an Early Access Bundle SDK user and want the older tags as the default, update to the latest Early Access version.  This mostly only affects visuals. All SDK functionality provided by the `Mattertag` namespace will continue to work as is with Tags 2.0
{% endhint %}

### What are Early Access Builds?

Early access builds allow developers to prepare for the next SDK release by providing upcoming, sometimes experimental features and bug fixes prior to general availability.

### Early Access Features

This Early Access release is focused on our Tags 2.0 (formerly Mattertags) beta.

&#x20;**Note:** To try Tags 2.0, add the \&newtags=1 URL parameter to the Showcase’s iframe

#### How To / Migration Guides

* [Migrating from Mattertags to Tags](migrating-to-tags.md)
* [Using HTML Code Sandboxes](using-code-sandboxes.md)

### Get the Early Access Bundle SDK

Build - [3.1.75.3-0-gba9de22f6d](https://static.matterport.com/showcase-sdk/bundle/3.1.75.3-0-gba9de22f6d/showcase-bundle.zip)

### Reference Pages and Types

[View the Tag reference](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tag.html)

[View the full Docs](https://matterport.github.io/showcase-sdk/docs/reference/current/index.html)

[Get types for the Embed SDK](../../sdk-for-embeds/getting-started/typescript-definitions.md)

### Known Issues

No issues logged at this time.

### Changelog

**Sep 13, 2022**

* Fixed an issue where [`Tag.allowAction`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tag.html#allowaction) would throw an error if called to early
* Fixed an issue with [`Mattertag.add`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag.html#add) when using a media type of `MediaType.NONE`
* Fixed `media.src` returned in the items of [`Mattertag.data`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag.html#data)

**Aug 24, 2022**

* Fixed issues with [`Tag.allowAction`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tag.html#allowaction) as well as backward compatibility with [`Mattetag.preventAction`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag.html#preventaction) when using Tags 2.0
* The tag billboard and/or dock now close when the tag is removed
* Editing a tag now displays the changes immediately; no need to close and re-open the tag to display the new contents
* Events from the `Mattertag` namespace now properly fire when using Tags 2.0

**Aug 4, 2022**

* The default Mattertag/Tag implementation is “classic” Mattertags ignoring any external feature policies overrides. To use Tags 2.0, a manual opt-in is necessary using the `newtags=1` URL parameter on Showcase’s iframe.

**July 21, 2022**

* Split [`IObject.addPath`](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.iobject.html#addpath) into individual functions to reduce boilerplate
  * use [`IObject.addInputPath`](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.iobject.html#addinputpath) for inputs
  * use [`IObject.addOutputPath`](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.iobject.html#addoutputpath) for outputs
  * use [`IObject.addEventPath`](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.iobject.html#addeventpath) for events
  * use [`IObject.addEmitPath`](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.iobject.html#addemitpath) for emits
* In an effort to streamline the interfaces of Scene objects ([`IObject`](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.iobject.html), [`INode`](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.inode.html), [`IComponent`](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.icomponent.html)), numerous properties and functions have been removed
* Similarly, the `renderer` returned in callbacks to [`Scene.configure`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/scene.html#configure) or that exists on [`ISceneComponent.context`](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/scene.icomponentcontext.html) has a limited `canvas` object that no longer grants access to the DOM and numerous other functions

**June 30, 2022**

* Added [`Tag.detach`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tag.html#detach) to remove attachments from a tag
* Removed the need to specify the `type` when calling [`Tag.registerAttachment`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tag.html#registerattachment)
* Added [`Tag.registerSandbox`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tag.html#registersandbox) which should be used as a replacement for [`Tag.addSandbox`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tag.html#addsandbox)
* Added [`Tag.editStem`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tag.html#editstem) and [`Mattertag.editStem`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag.html#editstem) to control the stem’s length and/or visibility
* [`Asset.registerTexture`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/asset.html#registertexture) should now be used in place [Pointer.registerTexture](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/pointer.html#registertexture). Assets from `Asset.registerTexture` can be used in [`Pointer.editTexture`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/pointer.html#edittexture), [Mattertag.editIcon](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag.html#editicon), and [`Tag.editIcon`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tag.html#editicon)
* Fixed an issue where [Embed.ly key overrides](https://matterport.github.io/showcase-sdk/sdkbundle\_tutorials\_setting\_up\_embedly) were not respected

**June 7, 2022**

* Added the [Tag](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tag.html) namespace.
* Added [`Label.data`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/label.html#data) collection to receive Labels data
* Added [`Tour.currentStep`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tour.html#currentstep), [`Tour.transition`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tour.html#transition), and [Tour.state](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/tour.html#state) to get information about what the tour is currently doing
* Added [Mode.current](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mode.html#current) and [`Mode.transition`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mode.html#transition-1) to get information about the current view mode and any transitions between them taking place
* Added [`Asset.registerTexture`](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/asset.html#registertexture) to be used a central place for registering icons like those for Tags or Mattertags
* Updated internal Three.js from r136 to r139
