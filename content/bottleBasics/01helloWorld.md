---
title: Hello, World!
---

Make a new file named `hello.py` and enter the following code:
{{< highlight python "linenos=table,linenostart=1" >}}
from bottle import route, run

@route('/')
def index():
    return "Hello, world!"

run(reloader=True, debug=True)
{{< /highlight >}}

To run your file, you should be able to press the play button in the top right of the window. Failing that, from the file explorer on the left, right click on your file and choose *Open in Integrated Terminal*. The terminal will open below the main editor pane. In the terminal, type `python hello.py`. If you named your file something else, use its name here.

You should see this:
```
Bottle v0.12.19 server starting up (using WSGIRefServer())...
Listening on http://127.0.0.1:8080/
Hit Ctrl-C to quit.
```

If so, it's working! Control-click on the link to open it directly in your browser. You should see "Hello, world!" in the browser window.

# So what's going on?
{{< highlight python "linenos=table,linenostart=1">}}
from bottle import route, run
{{< /highlight >}}

The first line imports the bits of bottle that we'll be using. In more complicated examples, you'll notice this line will get longer, as we use more parts of the module.

{{< highlight python "linenos=table,linenostart=4">}}
def index():
    return "Hello, world!"
{{< /highlight >}}

This defines a function called `index()`. When called it simply returns a string. In time, we'll replace this with something more complicated: a whole HTML document, with CSS styling, generated with a template, customised with data particular to the page and user. But for now, it's a simple string.

{{< highlight python "linenos=table,linenostart=3">}}
@route('/')
{{< /highlight >}}

The odd-looking code on line 3 defines what URL patterns should be handled by this function. This weird syntax is a Python shortcut for a function called a *decorator*. For now, we don't need to worry about the name or how it works, we only need to know how to use it.

At this point we've defined all the parts of our web application, and all that is left is to turn the webserver on and start listening for requests.

{{< highlight python "linenos=table,linenostart=7">}}
run(reloader=True, debug=True)
{{< /highlight >}}

To find out more about the `run()` function (there are lots of things you fiddle with), look at the [bottle.run()]({{< ref "glossary/bottleRun.md" >}}) page.