---
title: Asteroid.cs
---

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Asteroid : MonoBehaviour
{
    public GameObject explosionTemplate;
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
        if( screenPos.x > Screen.width+margin ){
            //off right, move to left
            screenPos.x = -margin;
        }else if( screenPos.x < -margin ){
            //off left, move to right
            screenPos.x = Screen.width+margin;
        }
        if( screenPos.y > Screen.height+margin ){
            //off bottom, move to top
            screenPos.y = -margin;
        }else if( screenPos.y < -margin ){
            //off top, move to bottom
            screenPos.y = Screen.height+margin;
        }
        Vector3 newPos = Camera.main.ScreenToWorldPoint(screenPos);
        transform.position = new Vector2(newPos.x, newPos.y);
    }

    void OnTriggerEnter2D(Collider2D other)
    {
        if( other.gameObject.CompareTag("rockKiller") ){
            GameObject explosion = Instantiate(explosionTemplate, transform.position, transform.rotation) as GameObject;
            Destroy(other.gameObject);
            Destroy(this.gameObject);
        }
    }
}
```