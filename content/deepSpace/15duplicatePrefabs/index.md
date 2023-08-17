---
title: "15: Make debris (part 2)"
weight: 15
---
Select your asteroidLarge prefab and from the menubar choose *Edit > Duplicate* (Ctrl-D). Choose the copy (should have a 1 at the end of the name) and choose Open from the inspector. You can now rename it asteroidMedium. It'll ask you if you want to rename the file or keep the old name: choose Rename File. Drag your medium sprite image into the Sprite Renderer's sprite field. You'll now need to adjust the Collider size: Choose "Edit Collider" in the collider panel in the inspector, and use the green knobs to adjust the size. Click the button again to stop editing.

Congratulations, you now have medium rocks as well as big ones! You can now go to your asteroidLarge, and set its debris template to the medium asteroid.

You can repeat this process to create small ones as well. Whatever you decide is the smallest size, make sure it doesn't have a debris template selected (or you'll never be able to clear the screen). If it has one selected, click on the debris template reference field and press Delete to clear it.