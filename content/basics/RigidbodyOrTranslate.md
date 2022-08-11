---
title: Rigidbody vs Translate
weight: 200
---

*from [pressstart.vip](https://pressstart.vip/tutorials/2018/10/19/71/rigidbody-vs-translate.html)*

{{< youtube ixM2W2tPn6c >}}
[Link to view at TMC](https://web.microsoftstream.com/video/c1a1f426-951c-4009-aadd-e18f6af8bcd3)

## Video sections
- 0:28 - Moving An Object Using Translate
- 2:20 - Problems with using Translate
- 2:50 - Using RigidBody for Physics & Collisions
- 5:00 - 3 Ways to Move An Object with RigidBody
- 5:10 - Using AddForce()
- 6:15 - Using Velocity
- 7:05 - Using MovePosition
## Source code for `translate`
``` cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class translate : MonoBehaviour {
    public float speed = 10.0f;

    // Update is called once per frame
    void Update () {
        moveCharacter(new Vector2(Input.GetAxis("Horizontal"), Input.GetAxis("Vertical")));

    }
    void moveCharacter(Vector2 direction){
        transform.Translate(direction * speed * Time.deltaTime);
    }
}
```

## Source code for `Rigidbody`
``` cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class rbmovement : MonoBehaviour {
    public float speed = 10.0f;
    public Rigidbody rb;
    public Vector2 movement;

    // Use this for initialization
    void Start () {
        rb = this.GetComponent<Rigidbody>();
    }
    
    // Update is called once per frame
    void Update () {
        movement = new Vector2(Input.GetAxis("Horizontal"), Input.GetAxis("Vertical"));
    }
    void FixedUpdate(){
        moveCharacter(movement);
    }
    void moveCharacter(Vector2 direction){
        //insert one of the 3 types of movement here
    }
}
```

## To move with `AddForce()`
``` cs
void moveCharacter(Vector2 direction){
    rb.AddForce(direction * speed);
}
```

## To move with `velocity`
``` cs
void moveCharacter(Vector2 direction){
    rb.velocity = direction * speed;
}
``` 

## TO move with `MovePosition()`
``` cs
void moveCharacter(Vector2 direction){
    rb.MovePosition((Vector2)transform.position + (direction * speed * Time.deltaTime));
}
```