---
title: rock.cs
---

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Rock : MonoBehaviour
{
    private Rigidbody2D rb;
    public GameObject explosionTemplate;
    public GameObject debrisTemplate;
    private float initializationTime;
    
    // Start is called before the first frame update
    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
        initializationTime = Time.timeSinceLevelLoad;

        //Choose a random angle
        float angle = Random.Range(0f, 360f);
        this.transform.rotation = Quaternion.Euler(0, 0, angle);

        //Choose a random speed
        float speed = Random.Range(0f, 5f);
        Vector3 s = new Vector3(0, speed, 0);
        rb.velocity = transform.rotation * s;
    }

    // Update is called once per frame
    void Update()
    {
        int margin = 50;
        Vector2 screenPos = Camera.main.WorldToScreenPoint(this.transform.position);
        if( screenPos.x > Screen.width+margin ){
            //off right, move to left
            screenPos.x = -margin;
        }
        if( screenPos.x < -margin ){
            //off left, move to right
            screenPos.x = Screen.width+margin;
        }
        if( screenPos.y > Screen.height+margin ){
            //off bottom, move to top
            screenPos.y = -margin;
        }
        if( screenPos.y < -margin ){
            //off top, move to bottom
            screenPos.y = Screen.height+margin;
        }

        Vector3 newWorldPosition = Camera.main.ScreenToWorldPoint(screenPos);
        this.transform.position = new Vector2(newWorldPosition.x, newWorldPosition.y);
    }
    
    public void OnCollisionEnter2D(Collision2D other)
    {
        if( Time.timeSinceLevelLoad - initializationTime < 0.5 ){
            return;
        }

        if( other.gameObject.CompareTag("Rock") || other.gameObject.CompareTag("LaserBlast") ){
            this.gameObject.SetActive(false);
            Destroy(this.gameObject);
            GameObject explosion = Instantiate(explosionTemplate,
                this.transform.position, this.transform.rotation)
                as GameObject;
            
            if( debrisTemplate != null){ // "!=" = "!" + "="
                float angle = Random.Range(30f, 150f);
                float speed = Random.Range(5f, 10f);
                Vector3 s = new Vector3(0, speed, 0);

                GameObject a = Instantiate(debrisTemplate,
                    this.transform.position, this.transform.rotation * Quaternion.Euler(0, 0, angle))
                    as GameObject;
                a.GetComponent<Rigidbody2D>().velocity = a.transform.rotation * s;

                GameObject b = Instantiate(debrisTemplate,
                    this.transform.position, this.transform.rotation * Quaternion.Euler(0, 0, -angle))
                    as GameObject;
                b.GetComponent<Rigidbody2D>().velocity = b.transform.rotation * s;
            }
        }
    }
}
```
