---
title: coordinates
---
3D coordinate systems can be either left- or right-handed.
In most of the maths and physics world, we us a right-handed system,
but in Unity we use a left-handed one. But what does that mean?

If you hold your left hand with your thumb pointing to the right (the x-axis)
and your index finger pointing up (the y-axis), when you extend your middle finger
it will point away from you. But if you do the same with your right hand, facing your
thumb to the right and your index finger up, your middle finger will extend toward you.

![LH vs RH Coordinate system](https://www.oreilly.com/library/view/learn-arcore/9781788830409/assets/a465e4c5-b6ca-4006-a40e-1aa9ad2ebc5d.png)

This is the question of left- and right-handed coordinate systems. Given the existing
x- and y-axis, should the z-axis point one way or the other? It's an arbitrary decision,
but it affects everything.

So, as we said above, Unity uses a LH coordinate system,
with:

- x-axis horizontal, positive right
- y-axis vertical, positive up
- z-axis in-out, positive in
