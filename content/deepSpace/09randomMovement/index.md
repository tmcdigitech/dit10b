---
title: "9: Move asteroids"
weight: 9
---
Having the asteroids hang in space as they do looks a litle unrealistic, so let's add some code to the `Start()` method to give them some initial movement.

The first part chooses a random angle from `0` to `360`, and sets the z-axis rotation to that angle.

The second part chooses a random speed from `0.5` to `2`. It then creates a vector pointing up (positive-y) which is the natural forward direction, and then rotates that vector to match the rotation of the asteroid.

Because this code is attached to the prefab, by changing it we change the prefab and hence all the asteroids together. Cool, huh?

{{< hint info >}}
Asteroids not moving? Do you need to refresh your assets? (Ctrl-R)
{{< /hint >}}

{{< highlight cs "linenos=table,hl_lines=10-18" >}}
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
}
{{< /highlight >}}