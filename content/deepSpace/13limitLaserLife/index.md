---
title: "13: Limit laser life"
weight: 13
---
If you're not a particularly accurate shot, those laser blasts you fire will continue to travel for ever, until the scene is unloaded (either due to changing the scene or quitting the game). This feels untidy and, in a big game, can cause resources to be tied up and used on things which aren't relevant anymore. Let's use the same idea used to handle screen wrapping to destroy the laser blasts once they reach the edge of the screen.

Make a script for your laser blasts, called `LaserBlast`.

In the `Update()` method, we'll get the laser blast's screen position from the main camera, and check it. The `||` symbol (two vertical bars next to each other) means "or", so it says that if the blast has gone off the right edge *or* the left edge *or* the bottom edge *or* the top edge, then destroy it.

If you play the game in window mode so you can see the hierarchy, you should see blasts appear in the hierarchy as you fire them, and then disappear again once they reach the edge of the screen.

{{< highlight cs "linenos=table,hl_lines=16-25" >}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class LaserBlast : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        //See if we've hit the edge of the screen
        Vector2 screenPos = Camera.main.WorldToScreenPoint(transform.position);
        if(
            screenPos.x > Screen.width ||
            screenPos.x < 0 ||
            screenPos.y > Screen.height ||
            screenPos.y < 0
        ){
            Destroy(this.gameObject);
        }
    }
}
{{< /highlight >}}