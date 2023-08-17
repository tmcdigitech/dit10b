---
title: "14: Make debris"
weight: 14
---
Here we're going to implement "debris". When an asteroid is destroyed, it can break into smaller pieces, which can also be destroyed (and also potentially break into pieces). In practice, we will use a combination of `Destroy()` and `Instantiate()` to remove the old asteroid and create three new ones in its place. One is in the direction of the original asteroid, and the other two are mirrored at a random angle from that direction.

We need a variable which shows what debris this asteroid should generate. Eventually we'll have a prefab for medium asteroids and small asteroids, which will be copied from the large asteroid. Then we can set up a chain, so large asteroids break into mediums, mediums into smalls, and then smalls disappear to nothing.

For now, just to check that things are working, once you've got the code in and refreshed, drag the asteroidLarge prefab in as the debris reference. This means, of course, that when you destroy an asteroid, it just replaces itself with three copies, which will have problems, but we can at least check that our code works.

{{< hint info >}}
If you want some more fun here, you can try setting the debris object to a playerBlast, or make a prefab out of your player, and use that as the debris! Crazy, but the stuff of inspiration...
{{< /hint >}}

{{< highlight cs "linenos=table,hl_lines=7-8 23 57-59 62-81" >}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Asteroid : MonoBehaviour
{
    public GameObject debrisTemplate;
    private float initializationTime;

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

        initializationTime = Time.timeSinceLevelLoad;
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
            screenPos.x = -margin/2;
        }else if( screenPos.x < -margin ){
            //off left, move to right
            screenPos.x = Screen.width+margin/2;
        }
        if( screenPos.y > Screen.height+margin ){
            //off bottom, move to top
            screenPos.y = -margin/2;
        }else if( screenPos.y < -margin ){
            //off top, move to bottom
            screenPos.y = Screen.height+margin/2;
        }

        //Work out our new world position
        Vector3 newPos = Camera.main.ScreenToWorldPoint(screenPos);
        transform.position = new Vector2(newPos.x, newPos.y);
    }

    void OnTriggerEnter2D(Collider2D other)
    {
        if( Time.timeSinceLevelLoad - initializationTime < 0.5 ){
            return;
        }

        if( other.gameObject.CompareTag("LaserBlast") ){
            if( debrisTemplate != null){ // "!=" = "!" + "="
                float angle = Random.Range(0f, 180f);
                float speed = Random.Range(5f, 10f);
                Vector3 s = new Vector3(0, speed, 0);

                GameObject a = Instantiate(debrisTemplate,
                    this.transform.position, this.transform.rotation)
                    as GameObject;
                a.GetComponent<Rigidbody2D>().velocity = a.transform.rotation * s;

                GameObject b = Instantiate(debrisTemplate,
                    this.transform.position, this.transform.rotation * Quaternion.Euler(0, 0, angle))
                    as GameObject;
                b.GetComponent<Rigidbody2D>().velocity = b.transform.rotation * s;

                GameObject c = Instantiate(debrisTemplate,
                    this.transform.position, this.transform.rotation * Quaternion.Euler(0, 0, -angle))
                    as GameObject;
                c.GetComponent<Rigidbody2D>().velocity = c.transform.rotation * s;
            }

            Destroy(this.gameObject);
            Destroy(other.gameObject);
        }
    }
}
{{< /highlight >}}