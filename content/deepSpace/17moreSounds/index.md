---
title: "17: More sounds"
weight: 17
---
Let's add a sound for when our asteroids blow up.

You'll have noticed that we didn't need any code for our LaserBlast sounds, and that might have surprised you. That's because we got lucky, and we didn't need to. In general, you will, and we'll look at that now. If you look at the setup for our LaserBlast, you'll see in the AudioSource that there is an option checked called "Play On Awake". This says that whenver our object "wakes up", the sound should play and since the Rigidbody component sets our LaserBlast to "Start Awake" it goes off as soon as our laser blast is constructed, which is exactly what we wanted. Job done, free of charge.

If we did the same though, with our asteroids, there would be three copies of the noise when our asteroids were hit, as the new smaller ones were created, or none, when the smallest are destroyed. So we need to do something different.

In the Asteroid script, we'll add a variable which links to the sound clip we want to play, and then we'll trigger it in code when we blow up an asteroid.

Refresh your assets in Unity, and drag a suitable audio clip onto the reference field in the asteroid script for each of your asteroid prefabs. Here is one you can try:

[Suitable asteroid explosion](explosionCrunch_000.ogg)

The number in the sound function is the volume, a number between 0 and 1. You can tune these so they are balanced (the laser blast in the previous step is WAAAY louder than the explosion above). For the laser blast, go to the inspector and adjust the volume there.

{{< hint info >}}
You may have noticed that the laser blast sound can be cut short sometimes. This is because in these cases the laser blast is destroyed before the sound finishes playing. If this bothers you, remove the audio source and copy the process we used here for the asteroids.

What is happening with our asteroid explosions is that when we want to play the sound an AudioSource is created at the location of the asteroid, but it is not attached to the asteroid. So when the asteroid is destroyed the AudioSource is still there. The sound plays, and the AudioSource destroys itself automatically when the sound is finished.
{{< /hint >}}

{{< highlight cs "linenos=table,hl_lines=9 63">}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Asteroid : MonoBehaviour
{
    public GameObject debrisTemplate;
    private float initializationTime;
    public AudioClip explosionSound;

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
            AudioSource.PlayClipAtPoint(explosionSound, transform.position, 1f);
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
