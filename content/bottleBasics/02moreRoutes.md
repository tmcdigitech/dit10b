---
title: More routes
weight: 2
---

{{< tabs "example" >}}
{{< tab "main.py" >}}
```python
from bottle import route, run

@route('/')
def index():
    return """
        <h1>Hello, world!</h1>
        Go to <a href="/other">the other page</a>.
    """

@route('/other')
def other_page():
    return """
        <h1>The other page</h1>
        Go back to <a href="/">the home page</a>.
    """

run(reloader=True, debug=True)
```
{{< /tabs >}}