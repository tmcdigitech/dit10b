---
title: Complete project
weight: 6
---

{{< tabs "example" >}}
{{< tab "main.py" >}}
```python
import sqlite3
from bottle import route, run, debug, template, request, static_file, error, redirect, abort

# only needed when you run Bottle on mod_wsgi
# from bottle import default_app

@route('/')
@route('/todo')
def todo_list():
    conn = sqlite3.connect('todo.db')
    c = conn.cursor()
    c.execute("SELECT id, task FROM todo WHERE status LIKE '1'")
    result_ongoing = c.fetchall()
    c.execute("SELECT id, task FROM todo WHERE status LIKE '0'")
    result_finished = c.fetchall()
    c.close()

    output = template('tpl/make_table.html', ongoing=result_ongoing, finished=result_finished)
    return output



@route('/new', method='GET')
def new_item_form():
    return template('tpl/new_task.html')

@route('/new', method='POST')
def new_item_make():
    if 'task' in request.POST:
        new = request.POST['task'].strip()
        conn = sqlite3.connect('todo.db')
        c = conn.cursor()

        c.execute("INSERT INTO todo (task,status) VALUES (?,?)", (new, 1))
        id = c.lastrowid

        conn.commit()
        c.close()

        redirect(f'/#{id}')



@route('/edit/<id:int>', method='GET')
def edit_item(id):
    if 'save' in request.GET:
        edit = request.GET['task'].strip()
        status = int(request.GET['status'].strip())

        conn = sqlite3.connect('todo.db')
        c = conn.cursor()
        c.execute("UPDATE todo SET task = ?, status = ? WHERE id LIKE ?", (edit, status, id))
        conn.commit()

        redirect(f'/#{id}')
    elif 'delete' in request.GET:
        conn = sqlite3.connect('todo.db')
        c = conn.cursor()
        c.execute("DELETE FROM todo WHERE id LIKE ?", (str(id)))
        conn.commit()

        redirect(f'/#{id}')

    else:
        conn = sqlite3.connect('todo.db')
        c = conn.cursor()
        c.execute("SELECT task FROM todo WHERE id LIKE ?", (str(id)))
        cur_data = c.fetchone()

        return template('tpl/edit_task.html', old=cur_data, id=id)


@route('/item<item:re:[0-9]+>')
def show_item(item):
        conn = sqlite3.connect('todo.db')
        c = conn.cursor()
        c.execute("SELECT task FROM todo WHERE id LIKE ?", (item,))
        result = c.fetchall()
        c.close()

        if not result:
            return mistake404(404)
        else:
            return 'Task: %s' % result[0]



@route('/static/<filepath:path>')
def server_static(filepath):
    return static_file(filepath, root='./static')

@route('/help')
def help():

    static_file('help.html', root='.')


@route('/json<json:re:[0-9]+>')
def show_json(json):

    conn = sqlite3.connect('todo.db')
    c = conn.cursor()
    c.execute("SELECT task FROM todo WHERE id LIKE ?", (json,))
    result = c.fetchall()
    c.close()

    if not result:
        return {'task': 'This item number does not exist!'}
    else:
        return {'task': result[0]}


@error(403)
def mistake403(code):
    return 'There is a mistake in your url!'


@error(404)
def mistake404(code):
    return 'Sorry, this task does not exist!'


debug(True)
run(reloader=True)
# remember to remove reloader=True and debug(True) when you move your
# application from development to a productive environment
```
{{< /tab >}}

{{< tab "schema.py" >}}
```python
import sqlite3
conn = sqlite3.connect('todo.db') # Warning: This file is created in the current directory
conn.execute("CREATE TABLE todo (id INTEGER PRIMARY KEY, task TEXT NOT NULL, status INTEGER NOT NULL)")
conn.execute("INSERT INTO todo (task,status) VALUES ('Read A-byte-of-python to get a good introduction into Python',0)")
conn.execute("INSERT INTO todo (task,status) VALUES ('Visit the Python website',1)")
conn.execute("INSERT INTO todo (task,status) VALUES ('Test various editors for and check the syntax highlighting',1)")
conn.execute("INSERT INTO todo (task,status) VALUES ('Choose your favorite WSGI-Framework',0)")
conn.commit()
```
{{< /tab >}}

{{< tab "tpl/base.html" >}}
```html
<!doctype html>
<html lang="en">
<head>
    <!-- Required meta tags -->
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous" />
    <!-- Our custom CSS -->
    <link href="/static/css/base.css" rel="stylesheet" />
    <!-- window/tab label -->
    <title>Hello, world!</title>
</head>
<body>
    <div class="container">
        <h1>{{title or 'No title'}}</h1>
        {{!base}}
    </div>
    <!-- Bootstrap Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
</body>
</html>
```
{{< /tab >}}

{{< tab "tpl/edit_task.html" >}}
```html
% rebase('tpl/base.html',title=f"Edit task")

%#template for editing a task
%#the template expects to receive a value for "id" as well a "old", the text of the selected ToDo item
<form action="/edit/{{id}}" method="GET">
    <div class="input-group mb-3">
        <span class="input-group-text" id="taskId">{{id}}:</span>
        <input type="text" name="task" value="{{old[0]}}" placeholder="Buy new shoes for the tortoise" class="form-control" id="task" aria-label="task" aria-describedby="taskId">
        </div>
    <select name="status" class="form-select mb-3" aria-label="Ongoing or finished">
        <option value="1">Ongoing</option>
        <option value="0">Finished</option>
    </select>
    <div class="row">
        <div class="col-6"><button name="save" class="btn btn-success" type="submit" id="button-save">Save</button></div>
        <div class="col-6 text-end"><button name="delete" class="btn btn-danger" type="submit" id="button-delete">Delete</button></div>
    </div>
</form>
```
{{< /tab >}}

{{< tab "tpl/new_task.html" >}}
```html
% rebase('tpl/base.html',title="New task")

%#template for the form for a new task
<p>Add a new task to the ToDo list:</p>
<form action="/new" method="POST">
    <div class="input-group mb-3">
        <input type="text" name="task" class="form-control" placeholder="Task description" aria-label="Task description" aria-describedby="button-addon2">
        <button name="save" class="btn btn-outline-success" type="submit" id="button-addon2">Save</button>
    </div>
</form>
```
{{< /tab >}}

{{< tab "tpl/make_table.html" >}}
```html
% rebase('tpl/base.html',title="Todo List")

<p>The open items are as follows:</p>
<table class="table table-striped">
    <tr>
        <th>id</th>
        <th>task</th>
        <th></th>
    </tr>
%for row in ongoing:
    <tr>
        <td><a id="{{row[0]}}">{{row[0]}}</a></td>
        <td>{{row[1]}}</td>
        <td>
            <a href="/edit/{{row[0]}}" class="btn btn-warning btn-sm">Edit</a>
        </td>
    </tr>
%end
<tr>
    <td></td>
    <td>
        <a href="/new" class="btn btn-primary btn-sm">New task</a>
    </td>
    <td></td>
</tr>
%for row in finished:
    <tr>
        <td class="text-muted"><a id="{{row[0]}}">{{row[0]}}</a></td>
        <td class="text-muted"><del>{{row[1]}}</del></td>
        <td>
            <a href="/edit/{{row[0]}}?delete" class="btn btn-danger btn-sm">Delete</a>
        </td>
    </tr>
%end
</table>
```
{{< /tab >}}

{{< tab "static/css/base.css" >}}
```css
@import url('https://fonts.googleapis.com/css2?family=Fredoka:wght@400;700&display=swap');
body {
    font-family: 'Fredoka';
}
```
{{< /tab >}}

{{< /tabs >}}