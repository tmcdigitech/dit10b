---
title: Endless 2D background
weight: 0
---

*from [pressstart.vip](https://pressstart.vip/tutorials/2019/04/15/93/endless-2d-background.html)*

*HOW TO MAKE A SEAMLESS 2D BACKGROUND IN UNITY*

If you need some backgrounds in a hurry, [check these ones out](https://tmcdigitech.github.io/dit8/gameDesign/02basics/assetsPlatform/backgrounds/).

{{< youtube 3UO-1suMbNc >}}
[Link to view at TMC](https://web.microsoftstream.com/video/38117d48-3462-4639-a646-40a7e9a771ac)

## Video sections
- 1:10 - Create C# Script
- 1:50 - Calculating Screen Boundaries
- 2:45 - Cycle through each of our background objects and load them on the screen
- 3:50 - Creating a function to setup the scene
- 6:40 - Creating a function to move our background elements to create a seamless effect
- 9:15 - Repositioning objects to fill the screen
- 10:20 - Adding a choke value to fix seams
- 11:00 - Final Product

## Source code for backgroundloop.cs

{{< highlight cs "linenos=table" >}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class backgroundLoop : MonoBehaviour{
    public GameObject[] levels;
    private Camera mainCamera;
    private Vector2 screenBounds;
    public float choke;
    public float scrollSpeed;

    void Start(){
        mainCamera = gameObject.GetComponent<Camera>();
        screenBounds = mainCamera.ScreenToWorldPoint(new Vector3(Screen.width, Screen.height, mainCamera.transform.position.z));
        foreach(GameObject obj in levels){
            loadChildObjects(obj);
        }
    }
    void loadChildObjects(GameObject obj){
        float objectWidth = obj.GetComponent<SpriteRenderer>().bounds.size.x - choke;
        int childsNeeded = (int)Mathf.Ceil(screenBounds.x * 2 / objectWidth);
        GameObject clone = Instantiate(obj) as GameObject;
        for(int i = 0; i <= childsNeeded; i++){
            GameObject c = Instantiate(clone) as GameObject;
            c.transform.SetParent(obj.transform);
            c.transform.position = new Vector3(objectWidth * i, obj.transform.position.y, obj.transform.position.z);
            c.name = obj.name + i;
        }
        Destroy(clone);
        Destroy(obj.GetComponent<SpriteRenderer>());
    }
    void repositionChildObjects(GameObject obj){
        Transform[] children = obj.GetComponentsInChildren<Transform>();
        if(children.Length > 1){
            GameObject firstChild = children[1].gameObject;
            GameObject lastChild = children[children.Length - 1].gameObject;
            float halfObjectWidth = lastChild.GetComponent<SpriteRenderer>().bounds.extents.x - choke;
            if(transform.position.x + screenBounds.x > lastChild.transform.position.x + halfObjectWidth){
                firstChild.transform.SetAsLastSibling();
                firstChild.transform.position = new Vector3(lastChild.transform.position.x + halfObjectWidth * 2, lastChild.transform.position.y, lastChild.transform.position.z);
            }else if(transform.position.x - screenBounds.x < firstChild.transform.position.x - halfObjectWidth){
                lastChild.transform.SetAsFirstSibling();
                lastChild.transform.position = new Vector3(firstChild.transform.position.x - halfObjectWidth * 2, firstChild.transform.position.y, firstChild.transform.position.z);
            }
        }
    }
    void Update() {

        Vector3 velocity = Vector3.zero;
        Vector3 desiredPosition = transform.position + new Vector3(scrollSpeed, 0, 0);
        Vector3 smoothPosition = Vector3.SmoothDamp(transform.position, desiredPosition, ref velocity, 0.3f);
        transform.position = smoothPosition;

    }
    void LateUpdate(){
        foreach(GameObject obj in levels){
            repositionChildObjects(obj);
        }
    }
}
{{< /highlight >}}