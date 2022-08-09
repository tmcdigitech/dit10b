---
title: Scenes
weight: 40
---

Scenes are selected by number (on the right hand side of the scene list in the build settings).

The two highlighted lines are the key ingredients here.

{{< highlight cs "linenos=table,hl_lines=4 11" >}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class Player : MonoBehaviour
{
    public void LoadScene(int level)
    {
        SceneManager.LoadScene(level);
    }
}
{{< /highlight >}}