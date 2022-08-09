---
title: Camera follow player
weight: 30
---

Attach this script to the main camera to make the camera track the player, keeping them in the centre of the screen.

{{< highlight cs "linenos=table" >}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CameraScript : MonoBehaviour {

    public GameObject target;
    public float offsetY = 2;
    public float offsetX = 2;

    // Use this for initialization
    void Start () {
    }
    
    // Update is called once per frame
    void Update () {
        loc = target.transform.position;
        loc.y += offsetY;
        loc.x += offsetX;
        loc.z = this.transform.position.z;
        this.transform.position = loc;
    }
}
{{< /highlight >}}