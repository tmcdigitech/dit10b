---
title: "16: Make some noise"
weight: 16
---
It is fairly easy to make some sound when we fire our lasers. We'll cover some more complex examples later. To make sound you need an AudioSource, which makes sound, and an AudioListener, to hear it. By default, the main camera has an AudioListener attached, and that is perfect for our needs (it usually is, which is why it's there).

Select your PlayerBlast prefab and add an *Audio > AudioSource* component. You'll see it has a reference field called AudioClip. We need to drop our laser blast noise in there, and we're done. Here is one you can use:

[Retro laser sound](laserRetro_004.ogg)

Download it and add it to the assets panel. Then drag it into the reference field. Play your game and enjoy sound!
