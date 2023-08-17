---
title: "11: Make a laser blast"
weight: 11
---
We now need to make our laser blast. Grab the laser blast you chose (ours is green) and drag it into the scene to make a new game object. Call it "playerBlast". As you did for the asteroids, make a tag called "LaserBlast" and tag your new playerBlast.

While we're setting things up, go ahead and add a `BoxCollider2D` and a `Rigidbody2D`.

Now turn your playerBlast into a prefab (drag it from the hierarchy down into the Assets panel). Since we don't want a random green blast in the middle of the scene, select the blast in the scene and delete it.

We can now edit the Player script and add the firing code.

First, on line 10 we add a variable which will point to the object we want to create when we hit the fire button.

Secondly, at the end of the `Update()` method, we add the code that handles the firing. We check to see if the Fire1 button (left Ctrl on the keyboard, by default) has just been pressed and, if so, get a reference to our "gun1". Note that the name of the gun in quotes must exactly match what you called the gun in Unity when you made it. This is why you don't want to leave it called Square! We now Instantiate (create an instance of) our desired firing object at the same location and rotation as the gun. Finally, we give the blast a brief kick with a strong force, and off it goes.

Once you have copied the code in and updated it, you'll see that the player has a new variable in the inspector called `Projectile Template`. Drag your playerBlast prefab onto that reference field.

{{< highlight cs "linenos=table,hl_lines=10 57-61" >}}
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
{{< /highlight >}}