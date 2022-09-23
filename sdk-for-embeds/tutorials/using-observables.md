# Using Observables

The SDK provides access to state through [Observables](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/iobservable.html). Observers can subscribe to Observables to watch and receive updates of the state.

### Receiving State from an Observable

State is provided by subscribing to an Observable. Two types of Observers are supported: functional, and object-oriented.

Observables always give an up-to-date view of its state to all of its subscribed Observers. In a sense, Observables and Observers are very similar to Events and Event Handlers.

With our Observable implementation

* when first subscribing an Observer to an Observable, the Observer will always be called back as soon as the state is available -- similar in functionality to a "getData" call
* all subscribed Observers will be called back for all subsequent updates to the observed state -- similar in functionality to an event handler
* subscribing multiple Observers to a single Observable does not increase the complexity of calculating the state of the Observable
* the Observable state used in the Observers' callbacks is cached and shared between all Observers

### Using a Functional Observer

Functional Observers are merely callback functions that accept the state as their argument.

For example, to subscribe to the current camera pose:

```typescript
function poseObserver(pose: MpSdk.Camera.Pose) {
  // use the current pose of the camera
  console.log(pose);
}
mpSdk.Camera.pose.subscribe(poseObserver);
```

### Using an Object-Oriented Observer

Object-Orieneted Observers are objects that conform to the [IObserver](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/iobserver.html) interface, or implement a member \`onChanged\` function.

For example, to subscribe to the current camera pose:

```typescript
class PoseObserver implements MpSdk.IObserver<MpSdk.Camera.Pose> {
  onChanged(pose: MpSdk.Camera.Pose) {
    // use the current pose of the camera
    console.log(pose);
  }
}
mpSdk.Camera.pose.subscribe(new PoseObserver());
```

### Using Multiple Observers

As mentioned, since Observables always have an up-to-date shared view of state, having multiple Observers is supported and encouraged.

To use the camera pose in two different systems within the same application is a matter of adding two Observers.

```typescript
// Component1.ts
mpSdk.Camera.pose.subscribe(function (pose) { /* use pose */ });
// Component2.ts
mpSdk.Camera.pose.subscribe({
  onChanged(pose) { /* use pose */ },
})
```

### Shutting down an Observer

When updates to state are no longer required, Observers should be removed from the Observable. When subscribing to an Observable, an [ISubscription](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/isubscription.html) object is returned. The \`ISubscription\` object is the object used to remove the subscribed Observer and stop any callback it would have received.

```typescript
const poseSubscription = mpSdk.Camera.pose.subscribe({
  onChanged(pose) { },
});
// ... some time later
poseSubscription.cancel();
// from here on, the Observer associated with `poseSubscriptoin` will no longer be called back
```

### Cloning an Observer's View of State

Because state is cached and shared between Observers of the same Observable, any mutations that are done to the state object in the callback can be seen by all Observers and are subject to be blown away by changes to the Observable.

If a snapshot of the state is needed, saving a reference to the argument in the callback is not enough. In such a case, cloning the state object is needed.

```typescript
const poseStack: MpSdk.Camera.Pose[] = [];
mpSdk.Camera.pose.subscribe(function (pose) {
  // create a deep clone of the pose and push it into a stack
  poseStack.push({
    ...pose,
    position: { ...pose.position },
    projection: [ ...pose.projection ],
    rotation: { ...pose.rotation },
    sweep: pose.sweep.slice(),
  });
});
```

### Benefits of Observables

Observable state has multiple benefits over our previous implementations of state.

#### Less Boilerplate

Before Observables, events (\`on\`) could be used to watch for some state changes. However, events can be missed. Getting the state of infrequently changing data required polling the data using something like \`getData\` to seed the data if the event is missed.

**DON'T**: Setting up a \`Camera.MOVE\` handler and seeding the data using \`getPose\` is very verbose.

```typescript
let pose: MpSdk.Camera.Pose;
function updatePose(newPose: MpSdk.Camera.Pose) {
  // update the pose when the camera moves
  pose = newPose;
}
// listen for camera changes
mpSdk.on(mpSdk.Camera.MOVE, updatePose);
// poll the data once in case the camera hasn't been moved yet
pose = await mpSdk.Camera.getPose();
```

**DO**: Use the Observable camera pose to reduce the above code to only one call: its \`subscribe\` function.

```typescript
mpSdk.Camera.pose.subscribe({
  onChanged(newPose) {
    // log the current camera pose
    console.log(newPose);
  },
});
```

#### Better Efficiency

Another benefit to Observables is that once subscribed, Observers are only called when changes occur. When a "get" call would return the same state as the previous call, it is doing unnecessary work. The excessive "get" calls and extra work done for each call are a potential for decreasing the performance fo the application.

**DON'T**: Polling the current camera pose by using an update loop triggers unnecessary updates

```typescript
function updatePose() {
  const newPose = await mpSdk.Camera.getPose();
  requestAnimationFrame(updatePose);
}
requestAnimationFrame(updatePose)
```

**DO**: Use an Observable to track state and automatically update only as needed

```typescript
// only called on first subscribe and when pose has changed
mpSdk.Camera.pose.subscribe(function (newPose) { });
```

#### Callback Consistency

Previously mentioned, both an event callback and a "get" call were required to successfully fetch and watch data. With an Observable, all of that behavior is completely encapsulated. Any new Observers that \`subscribe\` to an Observable will always be called at least once to ensure that they have an accurate view of the state and called again as state changes to ensure that it is kept up-to-date.

**DON'T**: Subscribing to events will miss prior updates

```typescript
// may or may not be called depending on if the camera is ever moved after the callback is registered
mpSdk.on(mpSdk.Camera.MOVE, function (newPose) { });
```

**DO**: Subscribing to an Observable always has an up-to-date view of state

```typescript
// always called at a minimum of once with the current state, and with any subsequent updates afterward
mpSdk.Camera.pose.subscribe(function (newPose) { });
```

### Waiting for a Condition of State

A "Condition" can be registered to an Observable as a one-off to wait for a certain condition to be met with a given state. Functional and object-oriented Conditions are supported.

#### Using a Functional Condition

Similar to Observers, functional Conditions are merely callback functions that receive the state as their argument, but return a boolean to determine if the condition was met.

For example, to wait for the camera pose to be in FLOORPLAN mode:

```typescript
function floorplanCondition(pose: MpSdk.Camera.Pose): boolean {
  return pose.mode === MpSdk.Mode.Mode.FLOORPLAN;
}
// wait for the camera pose to be in FLOORPLAN MODE ...
await mpSdk.Camera.pose.waitUntil(floorplanCondition);
// ... before continuing
```

#### Using an Object-Oriented Condition

Object-Oriented Conditions are objects that conform to the [ICondition](https://matterport.github.io/showcase-sdk/docs/reference/current/interfaces/icondition.html) interface, or implement a member \`waitUntil\` function that returns a boolean to determine if the condition was met.

```typescript
class FloorplanCondition implements MpSdk.ICondition<MpSdk.Camera.Pose> {
  waitUntil(pose: MpSdk.Camera.Pose): boolean {
    return pose.mode === MpSdk.Mode.Mode.FLOORPLAN;
  }
}
// wait for the camera pose to be in FLOORPLAN MODE ...
await mpSdk.Camera.pose.waitUntil(new FloorplanCondition());
// ... before continuing
```
