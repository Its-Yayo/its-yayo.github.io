---
layout: post
tags: [Python, Flask, Backend, Web Dev]
author: Luis De León
---
Github Resource [here](https://github.com/Its-Yayo/f-test)

## Table of Contents
1. [Intro](#intro)
2. [F-test](#f-test)
3. [APIs](#apis)
4. [Conclusion](#conclusion)


---

## Intro
I had to make a web app for a complete architecture project. This includes 2 mobile apps made with Kotlin, a fully-functional dynamic web app and an RDS DB instance. My team's doing both mobile apps (Yea, I'm not an Android dev lmao), so I focused on making this website. I'll say one of the members of my team helped me with the client-side code. (Yea, also the ```XMLHttpRequest();``` stuff). I was focused more in the server-side code, since I have more experience with it. 

In April 2023, I learnt Express.js, a backend framework to build minimal APIs for Node and JavaScript. I wasn't comfortable with it a lot (and not because my professor wasn't teach it well. In fact, he is one of the best programming teachers I've ever had) because JavaScript is not a language I really love. It's good for basic stuff and for beginners but I'ma say I'd rather use Python or Rust (soooooon). Also, I find the fact that I cannot learn so quite a bit at the time I'm surrounded with my fellow extroverts haha. I need some space to learn, to capture more knowledge to my fully-prepared brain. I discarted Express.js for this project for time reasons but also I needed to build something with passion and discipline. 

My professor suggested me Flask as a good option framework with Python. I didn't know how th I'd implement Flask in the whole app. I started resourcing by myself in a week we call "Semana Tec", which is like an week-off once we finish a period (A semester has 3 periods). 

Before starting this journey, I'll say that previously I had some knowledge about HTTP methods, status codes and basic APIs development since my experience with Express.js. But, as I said before, I didn't learne quite a bit so I checked it again by my own before starting out. 

Yea, that's when I proposed myself I can learn a whole framework within 2 days. For that, I needed to find a good idea for a project that may allow me to learn Flask. Then, back in Sep 11 2023, I decided to make F-test.

## F-test
Originally, F-test was a BMI calculator. A basic web app and super boring lmao. I improved it by setting up a new goal: A single app that sends, edits and deletes data from a single HTTP layout. Where is this data stored? Yea, good question. Remember I said something about an RDS DB instance? Yea, well... I used MariaDB as the DBMS since I had experience with MySQL back in the day. Also. I used SQL Server someday but I didn't like it at all lol. 

Anyways, for this project, I needed to make the design, the requirements .txt, etc. I realized that also I needed some dependencies.

```
$ pip install flask werkzeug python-dotenv tenacity mariadb
```

I did all stuff a software developer would do (I'm not referring to drink 8 cups of coffee). I set up my environment, my project distribution by folders, etc. I created my .env and .gitignore for my env variables in Python. 

And I moved on. I needed to make the app functional first rather than deploying it useless but with a good look. I created a simple HTML format and I started to make tests. 

I have 3 labels: Name, Phone and Email (Yea, what you can expect from a basic register format), but the intersting thing is here: You also can access, edit and delete those labels in the app, not in the proper DB. Also you can add data!

In the Frontend section I'll explain how I did it, but first I needed to build the APIs 


## APIs
Flask is a modern backend framework to build minimal and scalable applications. If you are interested in more about this framework, you can click [here](https://flask.palletsprojects.com/en/2.3.x/). 

The whole app makes 5 apps: Deploy the ```layout.html``` file, show the data, adds data, deletes data and edits that data. For this stuff, I already know that at least, I'll need 4 APIs: "/", "/edit", "/add", "/delete". But I guess, I'm not done. 

Somehow I need to figure out how to send data into a DB (In this case, a MariaDB server cuz I like MariaDB lmao). I remember I learnt how to create and manage stored procedures. These are like a simple .sql code block that may allow us to insert, get, delete or show any data. What I wanted to do is all of that inside the view. Flask will allow me to create queries and stuff. 

Before showing any code, I'ma say that F-test uses its HTML format to call the endpoints, then to be shown in the view. It's like the MVC model. Now, how I call an endpoint from the HTML using Flask? Welllllll, there's something called [Jinja2](https://palletsprojects.com/p/jinja/). To summarize it, Jinja2 is a template engine for Python that supports unicode characters. Also, Flask is compatible with Jinja2. So yea, I use it. 

I said before I needed to show some data in the page retrieved from the DB. Mhm, alright-

```sql
SELECT * FROM contacts
```
Easy peasy. Just I need to figure out how I will show this. Alright. But, waittttt, I need to create the Flask project with the dependencies I installed before!

```python
#!/usr/bin/env python3
from flask import Flask
import os


app = Flask(__name__)
app.secret_key = os.getenv('DB_SECRET_KEY')
```
Easy peasy again. Now I can show the data? No, wait. I need the DB connection.

```python
#!/usr/bin/env python3
from dotenv import load_dotenv
import mariadb
import os
import sys

load_dotenv()


def connection() -> mariadb.Connection:
    config = {
        'host': os.getenv('DB_HOST'),
        'port': int(os.getenv('DB_PORT')),
        'user': os.getenv('DB_USERNAME'),
        'password': os.getenv('DB_PASSWORD'),
        'database': os.getenv('DB_NAME')
    }

    try:
        conn = mariadb.connect(**config)
        print("Connected")  # Debug Message
        return conn
    except mariadb.Error as e:
        print(f"Error Connecting: {e}")
        sys.exit(1)
```

Alrighty then. Now may I? Sure, let's do it.
```python
@main.route("/")
def root() -> str:
    conn = connection()
    cur = conn.cursor()
    cur.execute("SELECT * FROM contacts")
    data = cur.fetchall()

    return render_template('index.html', contacts=data)
```

As u noticed before, I'm using decorators to stablish the endpoint route and the HTTP method (In this case, it's GET but it's not necessary to type it in the root endpoint. (The root endpoint in this case will be the first layout HTML that'll be shown the first time I deploy a page (locally or remotely). 

Note that also I'm using enviroment variables for the connection requirements, as well as the secret key (without it, the page raises an exception lmao). 

But here's the major question: How I call this endpoint with HTML to be shown then into the page? Mm alright. 

```html
<div class="col-md-7">
        <table class="table table-bordered table-borderless table-active bg-white table-responsive-sm">
            <thead>
                <tr>
                    <td>FullName</td>
                    <td>Phone</td>
                    <td>Email</td>
                    <td>Operation</td>
                </tr>
            </thead>
            <tbody> {% raw %}
            {% for contact in contacts %}
                <tr>
                    <td>{{ contact.1}}</td>
                    <td>{{ contact.2}}</td>
                    <td>{{ contact.3}}</td>
                    <td>
                        <a href='/edit_contact/{{ contact.0 }}' class="btn btn-secondary">Edit</a>
                        <a href='/delete_contact/{{ contact.0 }}' class="btn btn-danger">Delete</a>
                    </td>
                </tr>
            {% endfor %} {% endraw %}
            </tbody>
        </table>
    </div>
``` 
The main objective of this article is not about frontend and HTML. I'm not a frontend dev (I mean, I know some HTML stuff about divs and formats) but honestly, I had a little help with this. It's quite easy to learn!

With jinja2, I'm using divs to make a table where I will allocate the data. Inside the table, I need a loop to iterate every contact just to be shown like {% raw %} {{ contact.1 }} {% endraw %}. The last HTML cell, notice I'm already referencing 2 endpoints with a parameter (as well as a button class). 

Inside the UI, I need to store, edit and delete data. I'll not do that by queries using phpmyadmin dude, the client is not going to be happy with that lmao. Anyways, I need the endpoints to make all these stuff ("/all_contact", "/edit_contact/<parameter>", "/delete_contact/<parameter>" and "/delete_contact/<parameter>"). NOTE: You also can clone the repo resource to test it by yourself.  

Soon...


## Conclusion
This is the final design of F-test (for now), let me know if you like it. 
[![F-Test](/f-test_img.png)

Soon...

