---
title: unity components
---

{{< toc >}}

## Transform
The transform component is responsible for tracking the position, rotation and scale of the component in each of the three dimensions. Note that transform always has three dimensions, even when working in a 2D project.

{{< hint info >}}
If you want to rotate an object in a 2D project, you probably want to rotate about the z-axis!
{{< /hint >}}

## Sprite Renderer
Sprite renderers draw (render) 2D images (sprites). In 2D games, objects are often drawn using images, either standalone or as part of a sprite sheet. (Alternatives to sprites include constructed graphics like squares or ellipses made using a graphics library function.)

## Rigidbody [2D]
A rigidbody component interacts with the physics engine in Unity, so an object with a rigidbody component will interact with others in a natural way. *A Rigidbody is a 3D component; its 2D counterpart is a Rigidbody2D.*

## Collider [2D]
Colliders are components to detect collisions. There are many different colliders, which vary in shape and complexity (which translates into load on the computer). 2D colliders are marked as 2D; otherwise they are 3D.

The simplest (and fastest) collider is the Box Collider, which comes in 2D and 3D versions. 