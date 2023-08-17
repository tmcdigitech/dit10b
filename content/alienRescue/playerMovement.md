---
title: Player movement
weight: 20
---

{{< highlight cs "linenos=table,hl_lines=7-9 13 19-22" >}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Player : MonoBehaviour
{
    public float accel;
    private Rigidbody2D rb;

    // Start is called before the first frame update
    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    // Update is called once per frame
    void Update()
    {
        float inX = Input.GetAxis("Horizontal");
        float inY = Input.GetAxis("Vertical");
        Vector2 direction = new Vector2(inX, inY);
        rb.AddForce(direction * accel);
    }
}
{{< /highlight >}}