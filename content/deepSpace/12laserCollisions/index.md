---
title: "12: Handle blast collisions"
weight: 12
---
You can see you can shoot laser blasts, and they collide with the asteroids, causing them to move. They also then bounce off in a weird way that makes them look more like shards of coloured ice than laser blasts!

Firstly, go to your playerBlast prefab (in the Assets panel). In its collider component, turn on the "Is Trigger" option. This turns the blast from a physical object that collides into more of a "magic region" that things can pass through. Imagine the finish line of a race track: you want to be alerted when things cross into and out of it still, but you don't want them to bounce off.

Now let's open the Asteroid script and write some code to react to the blasts.

We need to write a method called OnTriggerEnter2D(), which will be called whenever the collider of the object (one of the asteroids) overlaps the collider of a trigger (for example, a laser blast). In it, we check to see if the thing that we've run over has the tag LaserBlast and, if so, we destroy both it and us.

{{< highlight cs "linenos=table,hl_lines=50-56" >}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Asteroid : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        Rigidbody2D rb = GetComponent<Rigidbody2D>();
        //Choose a random angle
        float angle = Random.Range(0f, 360f);
        this.transform.rotation = Quaternion.Euler(0, 0, angle);

        //Choose a random speed
        float speed = Random.Range(0.5f, 2f);
        Vector3 s = new Vector3(0, speed, 0);
        rb.velocity = transform.rotation * s;
    }

    // Update is called once per frame
    void Update()
    {
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
    }

    void OnTriggerEnter2D(Collider2D other)
    {
        if( other.gameObject.CompareTag("LaserBlast") ){
            Destroy(this.gameObject);
            Destroy(other.gameObject);
        }
    }
}
{{< /highlight >}}