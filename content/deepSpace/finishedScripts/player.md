---
title: Player.cs
---

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Player : MonoBehaviour
{
    public float rotSpeed;
    public float linSpeed;
    private Rigidbody2D rb;
    public GameObject projectileTemplate;

    // Start is called before the first frame update
    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    // Update is called once per frame
    void Update()
    {
        //Update rotation
        rb.MoveRotation(rb.rotation - Input.GetAxis("Horizontal") * rotSpeed * Time.deltaTime);

        //Update velocity
        Vector3 pos = transform.position;
        float y = Input.GetAxis("Vertical") * linSpeed * Time.deltaTime;

        Vector2 vChange = new Vector2(0, y);
        vChange = transform.rotation * vChange;
        rb.velocity += vChange;

        //Handle screen wrapping
        int margin = 50;
        //Work out our screen position
        Vector2 screenPos = Camera.main.WorldToScreenPoint(transform.position);

        //Check if we've moved too far offscreen
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

        //Work out our new world position
        Vector3 newPos = Camera.main.ScreenToWorldPoint(screenPos);
        transform.position = new Vector2(newPos.x, newPos.y);

        //Handle fire button
        if( Input.GetButtonDown("Fire1") ){
            GameObject gun1 = GameObject.Find("gun1");
            GameObject blast = Instantiate(projectileTemplate, gun1.transform.position, gun1.transform.rotation) as GameObject;
            blast.GetComponent<Rigidbody2D>().AddRelativeForce(new Vector2(0, 800));
        }
    }
}
```
