# Using Collections

The SDK provides access to collections of state objects through [ObservableMaps](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/iobservablemap.html) or colloquially as "Collections". MapObservers ("Observers") can subscribe to Collections to watch and receive updates of the items within a state collection.

Collections are an extension of our standard \[Observables]\(sdkbundle\_tutorials\_observables.html); therefore, there are a lot of similarities to the way the SDK provides other state through Observables. As such, some of this document may be redundant to with the documentation for Observables.

### Receiving State from a Collection

The state of a collection is provided by subscribing to a Collection.

Collections always provide an up-to-date view of its state to all of its subscribed Observers.

Observers support the following four callbacks that map to the four operations that describe how a Collection has changed.

* \`onAdded\`: when an item is added
* \`onRemoved\`: when an item is removed
* \`onUpdated\`: when an item is updated
* \`onCollectionUpdated\`: when the collection has changed in some way (an aggregate of the previous three operations)

Each of these callbacks are optional for each Observer to implement.

With our Observable Collection implementation:

* when first subscribing an Observer to a Collection, the Observer will always be called back through its \`onAdded\` with all existing items in the Collection and its \`onCollectionUpdated\` with the full collection of items
* all subscribed Observers will be called back when there are any changes to the items in the collection
* subscribing multiple Observers to a single Collection does not increase the complexity of calculating the state of the Collection
* the Collection state used in the Observers' callbacks is cached and shared between all Observers

### Observing How a Collection has Changed

An Observer can have up to four callbacks that match the available operations supported by the Collection. All callbacks are optional. An Observer can have any of \`onAdded\`, \`onRemoved\`, \`onUpdated\`, \`onCollectionUpdated\` callbacks.

An Observer that supports all four operations and watches the Mattetag state will look something like this:

```typescript
type MattertagItem = MpSdk.Mattertag.ObservableMattertagData;
class MattertagObserver implements MpSdk.IObservableMap<MattertagItem> {
  onAdded(index: string, tag: MattertagItem, collection: MpSdk.Dictionary<MattertagItem>) {
    console.log(`an item at index ${index} was added`);
  }
  onRemoved(index: string, tag: MattertagItem, collection: MpSdk.Dictionary<MattertagItem>) {
    console.log(`an item at index ${index} was removed`);
  }
  onUpdated(index: string, tag: MattertagItem, collection: MpSdk.Dictionary<MattertagItem>) {
    console.log(`an item at index ${index} was updated`);
  }
  onCollectionUpdated(collection: MpSdk.Dictionary<MattertagItem>) {
    console.log(`the collection has changed in some way`);
  }
}
mpSdk.Mattertag.data.subscribe(new MattertagObserver());
```

### Observing When the Collection has Changed

If the individual changes aren't important and all that's needed is an up-to-date view of the Collection, only the \`onCollectionUpdated\` needs implementing.

```typescript
type MattertagItem = MpSdk.Mattertag.ObservableMattertagData;
class MattertagObserver implements MpSdk.IObservableMap<MattertagItem> {
  onCollectionUpdated(collection: MpSdk.Dictionary<MattertagItem>) {
    console.log(`the full collection is now`, collection);
  }
}
mpSdk.Mattertag.data.subscribe(new MattertagObserver());

```

### Using Multiple Observers

One of the most important topics to understand about Collections is how Observers are notified of changes within the Collection.

When an Observer has been created but not yet subscribed to the Collection, it's "current view" of the state is undefined. It doesn't know anything about what it's observing yet.

When first subscribed, all items that are in the Collection have not been observed yet so it will trigger its \`onAdded\` callback for each item that it now sees.

Once the Observer has seen all the "new" items, it triggers its \`onCollectionUpdated\` callback to signify that the collection has updated in some way.

Now as things are added, removed, or updated in the Collection, the Observer will observe those changes, update its internal view to reflect what it sees happening in the Collection, and trigger the appropriate \`onAdded\`, \`onRemoved\`, and \`onUpdated\` callbacks, followed by an \`onCollectionUpdated\` call.

When a second Observer is created, it also starts with an undefined "current view" of the state. When it subscribes to the Collection, all items in the Collection are "new" to the Observer and will trigger an \`onAdded\` callback for each item it now sees. Afterward, it follows the same path for adding, removing, and updating items in its internal view separate from other Observers.

As an example of getting and observing when Mattertags are added to the Mattertag Collection:

```typescript
type MattertagItem = MpSdk.Mattertag.ObservableMattertagData;
class MattertagObserver implements MpSdk.IObservableMap<MattertagItem> {
  onAdded(index: string, tag: MattertagItem, collection: MpSdk.Dictionary<MattertagItem>) {
    console.log(`an item at index ${index} was added`);
  }
}
// subscribing a new Observer will trigger its `onAdded` for each Mattertag 
// in the Collection
mpSdk.Mattertag.data.subscribe(new MattertagObserver());
// subscribing a second Observer will ALSO trigger its `onAdded` for each Mattertag 
// in the Collection
mpSdk.Mattertag.data.subscribe(new MattertagObserver());
```

#### Shutting down an Observer

When updates to state are no longer required, Observers should be removed from the Observable. When subscribing to an Observable, an [ISubscription](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/isubscription.html) object is returned. The \`ISubscription\` object is the object used to remove the subscribed Observer and stop any callback it would have received.

```typescript
const mattertagSubscription = mpSdk.Mattertag.data.subscribe({
  onAdded(index, item, collection) { },
});
// ... some time later
mattertagSubscription.cancel();
// from here on, the Observer's associated with `mattertagSubscription` will no
// longer be called back
```

#### Cloning an Observer's View of the Collection

Because the items passed to the Observer's callbacks are shared references to the item in the collection, and the collection argument is also a shared reference to the cache, any mutations done to either object will be seen by all Observers and can potentially be blown away by updates to the Collection or its data.

If a snapshot of the Collection or its items is needed, cloning one or both objects is necessary, making sure to clone the item's nested arrays and objects, and possibly slicing its strings.

```typescript
type MattertagItem = MpSdk.Mattertag.ObservableMattertagData;
const mattertagView: Record<string, MattertagItem> = {};
mpSdk.Mattertag.data.subscribe({
  onAdded(index, tag, collection) {
    mattertagView[index] = {
      ...tag,
      anchorPosition: { ...tag.anchorPosition },
      color: { ...tag.color },
      description: tag.description.slice(),
      floorInfo: {
        ...tag.floorInfo,
        id: tag.floorInfo.id.slice(),
      },
      label: tag.label.slice(),
      media: {
        ...tag.media,
        src: tag.media.src.slice(),
      },
      sid: tag.sid.slice(),
      stemVector: { ...tag.stemVector },
    }
  }
});
```

### Benefits of Observable Collections

Like standard Observables, Collections provide many of the same benefits over our previous implementations of state.

#### Less Boilerplate

Before Collections, events (\`on\`) could be used to watch for some collections of state. However, events can be missed. Getting the state of infrequently changing data required polling the data using something like \`getData\` to seed the data if the event is missed.

\*\*DON'T\*\*:

```typescript
let labels: MpSdk.Label.Label[];
mpSdk.on(mpSdk.Label.POSITION_UPDATED, function (updatedLabels) {
  labels = updatedLabels;
});
labels = await mpSdk.Label.getData();
```

\*\*DO\*\*: Use a Collection to reduce the above example to only one call: its \`subscribe\` function.

```typescript
let mattertags: MpSdk.Dictionary<MpSdk.Mattertag.ObservableMattertagData>;
mpSdk.Mattertag.data.subscribe({
  // NOTE: this is only saving the reference to the shared `collection`...
  // ...It will update as the collection changes
  onCollectionUpdated(collection) {
    mattertags = collection;
   }
});
```

#### More Granular and Descriptive Updates

Collections express the extent of their changes to Observers.

#### Better Efficiency

Collections are a more efficient way to&#x20;
