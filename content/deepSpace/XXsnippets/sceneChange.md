---
title: Changing scenes
---

At the top of any script which calls scene changes, you will need to add:

```cs
using UnityEngine.SceneManagement;
```

At the point in your script where you want to change scenes, add the line:

```cs
SceneManager.LoadScene(level);
```

Replace `level` either with the name of the scene (a string) or the number of the scene from *File > Build Settings* (an int).

![](../buildSettings.png)

