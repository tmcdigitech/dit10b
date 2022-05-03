---
title: Databases
weight: 5
---
*from [BottlePy.org](https://bottlepy.org/docs/dev/tutorial_app.html)*

*See also this [funprojects.blog](https://funprojects.blog/2020/03/30/sqlite-bottle-todo-list/) tutorial.*

{{< tabs "example" >}}
{{< tab "main.py" >}}
```python
import sqlite3
from bottle import route, run, debug, template, request, static_file, error


@route('/todo')
def todo_list():

    conn = sqlite3.connect('todo.db')
    c = conn.cursor()
    c.execute("SELECT id, task FROM todo WHERE status LIKE '1'")
    result = c.fetchall()
    c.close()

    output = template('tpl/make_table.html', rows=result)
    return output


@route('/new', method='GET')
def new_item():

    if request.GET.save:

        new = request.GET.task.strip()
        conn = sqlite3.connect('todo.db')
        c = conn.cursor()

        c.execute("INSERT INTO todo (task,status) VALUES (?,?)", (new, 1))
        new_id = c.lastrowid

        conn.commit()
        c.close()

        return '<p>The new task was inserted into the database, the ID is %s</p>' % new_id

    else:
        return template('tpl/new_task.html')


@route('/edit/<no:int>', method='GET')
def edit_item(no):

    if request.GET.save:
        edit = request.GET.task.strip()
        status = request.GET.status.strip()

        if status == 'open':
            status = 1
        else:
            status = 0

        conn = sqlite3.connect('todo.db')
        c = conn.cursor()
        c.execute("UPDATE todo SET task = ?, status = ? WHERE id LIKE ?", (edit, status, no))
        conn.commit()

        return '<p>The item number %s was successfully updated</p>' % no
    else:
        conn = sqlite3.connect('todo.db')
        c = conn.cursor()
        c.execute("SELECT task FROM todo WHERE id LIKE ?", (str(no)))
        cur_data = c.fetchone()

        return template('tpl/edit_task.html', old=cur_data, no=no)


@route('/item<item:re:[0-9]+>')
def show_item(item):

        conn = sqlite3.connect('todo.db')
        c = conn.cursor()
        c.execute("SELECT task FROM todo WHERE id LIKE ?", (item,))
        result = c.fetchall()
        c.close()

        if not result:
            return 'This item number does not exist!'
        else:
            return 'Task: %s' % result[0]


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
    return 'Sorry, this page does not exist!'


run(reloader=True, debug=True)
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

{{< tab "tpl/edit_task.html" >}}
```html
%#template for editing a task
%#the template expects to receive a value for "no" as well a "old", the text of the selected ToDo item
<p>Edit the task with ID = {{no}}</p>
<form action="/edit/{{no}}" method="get">
  <input type="text" name="task" value="{{old[0]}}" size="100" maxlength="100">
  <select name="status">
    <option>open</option>
    <option>closed</option>
  </select>
  <br>
  <input type="submit" name="save" value="save">
</form>
```
{{< /tab >}}

{{< tab "tpl/new_task.html" >}}
```html
%#template for the form for a new task
<p>Add a new task to the ToDo list:</p>
<form action="/new" method="GET">
  <input type="text" size="100" maxlength="100" name="task">
  <input type="submit" name="save" value="save">
</form>
```
{{< /tab >}}

{{< tab "tpl/make_table.html" >}}
```html
%#template to generate a HTML table from a list of tuples (or list of lists, or tuple of tuples or ...)
<p>The open items are as follows:</p>
<table border="1">
%for row in rows:
  <tr>
  %for col in row:
    <td>{{col}}</td>
  %end
  </tr>
%end
</table>
```
{{< /tab >}}

{{< /tabs >}}