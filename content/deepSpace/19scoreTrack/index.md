---
title: "19: Update the score"
weight: 19
---
Now that we've got a place to display the score, we need a way of managing the score. The most flexible way to handle this is to make a game object whose job is to manage aspects of the game. A `GameManager`!

In the hierarchy, create an empty game object (right click, choose "Create Empty"). Call this "GameManager".

Add a script called GameManager to it.

The game manager will keep track of the score, and have a reference to the score display so it can update the display when the score changes. There is a method called `ScoreIncrease()` which can be called by other objects to change the score. This is what our asteroids will use.

{{< highlight cs "linenos=table,hl_lines=4 8-9 14 23-27">}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class GameManager : MonoBehaviour
{
    public int score;
    public TMPro.TextMeshProUGUI scoreField;
    
    // Start is called before the first frame update
    void Start()
    {
        score = 0;
    }

    // Update is called once per frame
    void Update()
    {

    }

    public void ScoreIncrease(int n)
    {
        score += n;
        scoreField.text = "Destroyed: "+score;
    }
}
{{< /highlight >}}

Refresh your assets, and drag a reference to the score display to the field in the GameManager object.

In your Asteroid script, we need to add a reference to the GameManager, and call the `ScoreIncrease()` method each time an asteroid is destroyed.

{{< highlight cs "linenos=table,hl_lines=9 17 30">}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Asteroid : MonoBehaviour
{
    public GameObject debrisTemplate;
    private float initializationTime;
    private GameManager gm;

    // Start is called before the first frame update
    void Start()
    {
        // ...

        initializationTime = Time.timeSinceLevelLoad;
        gm = GameObject.Find("GameManager").GetComponent<GameManager>();

    }

    // ...

    void OnTriggerEnter2D(Collider2D other)
    {
        if( Time.timeSinceLevelLoad - initializationTime < 0.5 ){
            return;
        }

        if( other.gameObject.CompareTag("LaserBlast") ){
            gm.ScoreIncrease(1);
            if( debrisTemplate != null){
                // ...
        }
    }
}
{{< /highlight >}}