---
title: Forces
image: 
description: Learn all about applying physical forces in Babylon.js.
keywords: diving deeper, phyiscs, forces
further-reading:
    - title: How To Use The Physics Engines
      url: /features/featuresDeepDive/physics/usingPhysicsEngine
video-overview:
video-content:
---

## Difference between a force and an impulse

A force is a continuous effect that is applied to an object over time, which can change the object's velocity or direction of motion. For example, a force could be used to simulate gravity, wind resistance, or a player pushing an object.

An impulse, on the other hand, is a sudden, instantaneous effect that changes the velocity of an object. It is a specific amount of force applied over a very short duration of time, often modeled as a single frame in a game. For example, a collision between two objects might generate an impulse that changes the direction and speed of both objects.

In summary, a force is a continuous effect over time, while an impulse is a sudden, instantaneous effect that changes the velocity of an object.

## API calls

## Physics Helper

#### Radial explosion impulse/force & gravitational fields

You have the ability to create radial explosions & gravitational forces. 

The forces are never applied to impostors that have mass equal 0 (the ground for example).

```javascript
var physicsHelper = new BABYLON.PhysicsHelper(scene);

var origin = BABYLON.Vector3(0, 0, 0);
var radius = 10;
var strength = 20;
var falloff = BABYLON.PhysicsRadialImpulseFalloff.Linear; // or BABYLON.PhysicsRadialImpulseFalloff.Constant

var explosionEvent = physicsHelper.applyRadialExplosionImpulse( // or .applyRadialExplosionForce
    origin,
    radius,
    strength,
    falloff
);
// the second `radius` argument can also act as options: `.applyRadialExplosionImpulse(origin, { radius: radius, strength: strength, falloff: falloff })`

// or

var gravitationalFieldEvent = physicsHelper.gravitationalField(
    origin,
    radius,
    strength,
    falloff
);
// the second `radius` argument can also act as options: `.gravitationalField(origin, { radius: radius, strength: strength, falloff: falloff })`
gravitationalFieldEvent.enable(); // need to call, if you want to activate the gravitational field.
setTimeout(function (gravitationalFieldEvent) { gravitationalFieldEvent.disable(); }, 3000, gravitationalFieldEvent);

// or

var updraftEvent = physicsHelper.updraft(
    origin,
    radius,
    strength,
    height,
    BABYLON.PhysicsUpdraftMode.Center // or BABYLON.PhysicsUpdraftMode.Perpendicular
);
// the second `radius` argument can also act as options: `.updraft(origin, { radius: radius, strength: strength, height: height, updraftMode: PhysicsUpdraftMode.Center })`
updraftEvent.enable();
setTimeout(function (updraftEvent) { updraftEvent.disable(); }, 5000, updraftEvent);

// or

var vortexEvent = physicsHelper.vortex(
    origin,
    radius,
    strength,
    height
);
// the second `radius` argument can also act as options: `.vortex(origin, { radius: radius, strength: strength, height: height, centripetalForceThreshold: 0.7, centripetalForceMultiplier: 5, centrifugalForceMultiplier: 0.5, updraftForceMultiplier: 0.02 })`
vortexEvent.enable();
setTimeout(function (vortexEvent) { vortexEvent.disable(); }, 5000, vortexEvent);
```

In case you want to do some debug, like visually show the sphere and/or rays, you can do that by calling `event.getData()` *(note that if you do that, you will need to manually call `event.dispose()` to dispose the unused meshes, after you are done debugging)*. The `event.getData()` will return back the `sphere` mesh variable, which you can then use, to apply a semi-transparent material, so you can visualize it. The `explosionEvent.getData()` will also return back the `rays` rays variable, in case you want them for debugging purposes.

*For a more detailed explanation, please take a look at the playground example below.*

** example PG `physicsHelperPG.js` **