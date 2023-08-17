---
title: "5: Add components"
weight: 5
---

Using the Add Component button, add a `Rigidbody2D` and a `BoxCollider2D` component:
- *Physics 2D > Rigidbody 2D* to add the [Rigidbody2D]({{< ref "/glossary/components#rigidbody2d" >}}) component, and
- *Physics 2D > BoxCollider 2D* to add a [BoxCollider2D]({{< ref "/glossary/components#collider2d" >}}) component.

The Rigidbody component exposes the object to the Physics engine, allowing forces to operate on it. If you press the play button above your scene now, you will see that the force of gravity causes your ship to fall off the bottom of the screen. Press play again to stop.

{{< hint warning >}}
A note of caution: you can use the Inspector to modify your game while it is playing, and this can be very handy for quickly trying things on the go, but any changes you make while the game is running will be lost when you stop it. So make sure that your game is stopped before you do anything you're planning to keep.
{{< /hint >}}

Colliders are used to detect when objects collide with one another. The simplest (and fastest for the computer) is the BoxCollider2D, but there are other 2D and 3D colliders which may better match the shape of your sprite.