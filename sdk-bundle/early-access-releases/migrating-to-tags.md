# Migrating to Tags

Tags (2.0), is the successor to Mattertags.

Most operations that are available in the `Mattertag` namespace have an equivalent operation in the `Tag` namespace. Some have slight syntactic changes. Some are now more robust and require more than a single step to use.

### Why the migration?

Traditional Mattertags allow for the viewing of embedded content and information about particular locations within a Matterport space. However, the Mattertag interface and architecture doesn’t directly support future extended capabilities, such as hosted content. Rather than shoehorning a new interface on top of an existing namespace, Tags 2.0 (Tags) seek to provide the foundation for more powerful tag-based capabilities in the future.

The `Mattertag` namespace should continue to work whether or not the application is using Tags 2.0. After the full release, the `Mattertag` namespace will be considered deprecated, but still functional. However, any future Tag capabilities will be added to the `Tag` namespace.

### A brief summary of the major changes

| Existing Functionality               | New Equivalent                                                        |
| ------------------------------------ | --------------------------------------------------------------------- |
| `Mattertag.registerIcon`             | `Asset.registerTexture`                                               |
| `Mattertag.preventAction`            | `Tag.allowAction`                                                     |
| `Mattertag.injectHTML`               | `Tag.addSandbox`                                                      |
| “media” in `Mattertag.add`           | <p><code>Tag.registerAttachment</code><br><code>Tag.attach</code></p> |
| “media” in `Mattertag.editBillboard` | <p><code>Tag.registerAttachment</code><br><code>Tag.attach</code></p> |
| `Mattertag.navigateTo`               | (no equivalent)                                                       |
| `Mattertag.Event`                    | (no equivalent)                                                       |

#### Registering and Using Icons

`Mattertag.registerIcon` should be migrated from `Mattertag.registerIcon` to `Asset.registerTexture`.

We have moved to a unified texture registry for icons and other visuals. The `Tag` namespace does not have a `registerIcon` function like the `Mattertag` namespace does. Instead, `Asset.registerTexture` should be used. Eventually, this will also be the case for `Pointer.editTexture`.

#### Adding Attachments (Media) to Tags

Providing media in `Mattertag.add` or `Mattertag.editBillboard` should be migrated to use `Tag.registerAttachment` and `Tag.attach`.

Tags now support multiple media (or attachments) per tag.

#### Adding Custom HTML Widgets

Adding custom HTML (or code sandbox) to a tag should be migrated from `Mattertag.injectHTML` to `Tag.addSandbox`.

Tags have unified file uploads, external media attachments through OEmbed, and custom HTML Sandboxes under attachments.

#### Preventing Mouse Actions

In order to prevent actions on tags, migrate from `Mattertag.preventAction` to `Tag.allowAction`

We identified that `preventAction` had a confusing double negative where a `false` equated to the action being allowed (`!prevented`). `Tag.allowAction` accepts the actions that are allowed so that `false` is `false` and `true` is `true`.

#### Navigating to View a Tag

There is currently no functionality in the `Tag` namespace to navigate to a tag. Continue to use `Mattertag.navigateToTag`.

Note, we are looking into providing general “look at” functionality as well as the ability to open, close, and dock tags programmatically.

#### Events

There are currently no events in the `Tag` namespace for things like clicking or hovering tags. Continue to use the existing `Mattertag` events.

Note that we are looking into providing observable state for things like hover states, open tags, docked tags, etc.

### Minor Changes

There are a number of other smaller changes between the current `Mattertag` namespace and the new `Tag` namespace.

#### Preferring Rooms over Floors

Each tag’s associated data now prefers room information over floors info. Floors can be derived from the room.

`Tag.add` and `Tag.editPosition` no longer accept a floor, nor do they accept a room. Instead, floor and room information is automatically inferred by the position specified. A side-effect of this is that when adding tags, any floor information (id) provided to `Mattertag.add` and `Mattertag.editPosition` will be ignored.
