---
title: LaserBlast.cs
---

```cs
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
        //Handle screen wrapping
        int margin = 50;
        Vector2 screenPos = Camera.main.WorldToScreenPoint(transform.position);
        if(
            screenPos.x > Screen.width+margin ||
            screenPos.x < -margin ||
            screenPos.y > Screen.height+margin ||
            screenPos.y < -margin
        ){
            Destroy(this);
        }

        Vector3 newPos = Camera.main.ScreenToWorldPoint(screenPos);
        transform.position = new Vector2(newPos.x, newPos.y);
    }
}
```
