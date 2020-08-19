---
layout: post
title:  "Project 4: TODO app but on the web! ☑️"
date:   2020-07-25 13:42:19 -0400
categories: software engineering
---

# Project 4: TODO app but on the web! ☑️

To get familiar with pythons webframework i decided to extend the TODO app to the Web using Flask. It was a fairly easy task as I used a simple text file as my database - but the most difficult part probably was to find good resources that had a tutorials for beginners. After learning about various requests that occur in a server, it was easy to build the application. For now the apps can add items and delete all todo items.

```python
@app.route('/')
def index():
    with open('todo.txt', 'r') as output:#reads the text file todo.txt which i am using a database
        new_list = output.read()
        x = new_list.splitlines()# x is each todo item 
        


    return render_template('index.html',  todo=x, id = index_id)

@app.route('/add', methods=['POST'])
def task():
    task_content = request.form['content']#requests the content of the todo item
    with open('todo.txt', 'a') as output:
        global index_id
        index_id += 1
        revised = (str(index_id))
        string_length=len(revised)+1
        output.write(revised.ljust(string_length))#numbering 
        output.write(task_content)
        output.write("\n")
        
    return redirect(url_for('index')) #returns to the main page

@app.route('/delete', methods=['POST'])#deletes all the item in the todo list
def delete():
    file = open("todo.txt","r+")
    file.truncate(0)
    file.close()
    global index_id
    index_id = 0
        
    return redirect(url_for('index'))


```

    


**For now you can see the code here:**
https://github.com/maishathasin/todo_flask/tree/master/server