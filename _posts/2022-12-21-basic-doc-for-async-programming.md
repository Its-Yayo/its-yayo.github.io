---
layout: post
tags: [Python, Asyncio]
author: Luis De León
---

When a programmer is writing some code, usually is noted that a function requires to be executed, making 
this code synchronous. Here's a basic example. 

```python 
# Add 2 numbers

def sum_numbers(x, y):
    return x + y

def main():
    x, y = 4, 5
    print(sum_numbers(x, y))

main()
```

In this example, the interpreter knows that the args in the function above needs to be known
to be executed. Because of this, the numbers are known calling the main function. (What is to 
be expected.) In this example, the output will be 9. 				

* * *

 

However, there's another way to code in a simply way, when 2 (or more) functions are being executed at the same time, with different responses and 
one after the other. I know this seems pretty confusing, so I'm gonna explain it to you in a more simple way. 

```python 
def sum_numbers(x, y):
    return x + y
```

From the previous example, we can note that there's a return value. However, we're not calling the function, so there will be no output. When this function is being called 
while another function is running, this is what is known as asynchronous code. In Python (and JavaScript), it's being denoted by the key word ```async```. So, refering as a main function, it is something like: 

```python
async def main():
    # Code here
```
Now, in order to code asynchronous programming, is important to import a library called ```asyncio```, which provides high-level APIs, structured network code and asynchronous frameworks. You
can find more information about this library [here](https://docs.python.org/3/library/asyncio.html).

That's very important at the time we need to schedule a function that's needed to be executed. And I say "schedule" because as I mentioned
before, you need to code a sequence of statements inside a block of code. To add more fundamental concepts related to this, first check this snippet code:

```python
# By Yayo
import asyncio
import time

async def test(word: str):
    return word

async def main():
    print("Time started at: ", time.strftime('%X'))
    print(await asyncio.gather(test(word="Hello")))
    await asyncio.sleep(0.5)

    print("World")

    print("Time finished at: ", time.strftime('%X'))

if __name__ == "__main__":
    asyncio.run(main())

```
When you run this, your console should show you something like this:

```
$ python3 some_code.py
Time started at:  15:34:02
['Hello']
World
Time finished at:  15:34:02
$
```
And yea, I can read your mind and I'd say you have no idea what I just code. Lemme explain you better. In case you have some experience
with Python, you can see that the first function is just returning an string object. In the main function we are calling it but, there's something new for non-async programmers and that's known as Task-based Asynchronous Pattern (TAP), using async/await syntax. 

The concept ```await``` is used as a key word to control a loop passed as an event. Both synchronous and asynchronous uses tasks perfomed while the whole code is executed. The only main difference between being sync and async is the code's threads, so referering to the explanation at the beginning of this doc, a sync code has only one thread, while an async code has multiple threads because of a code block's awaiting. 

In the previous example, we have some asyncio's methods and this is trully important. That will allow us to make a code asynchronous and there are plenty of methods you as a programmer can use, but just let's take a look. 

```python
print(await asyncio.gather(test(word="Hello")))
```
What we are doing in this sniṕpet code? First, let's define what does  ```asyncio.gather()``` means. Asyncio provides this method to call awaitable objects together. In our example, it doesn't make too sense because we are using just one object to call  ```test(word: str)``` and it's just one arg, but it's useful when we have +2 objects calling 'em at the same time. I've got this well-written [doc](https://superfastpython.com/asyncio-gather/) for you if you wanna play with gathering objects. 

```python
await asyncio.sleep(0.5)
```
This snippet code seems pretty easy to understand, but hold up, not too fast eh.  ```time``` (another Python module) already has a similar method, named  ```time.sleep()```. Ok, so what's the main difference? Yeah, one's for async threads and the other one for a single-thread code. Mmm, not so close, because we are talking about something really important. 

If we use ```time.sleep()```, we are suspending a whole single-thread execute until with an specific time range. In simple words, the code will just do nothing during the specified time. However, ```asyncio.sleep()``` works slightly different, considering we're coding async code. Assuming we have multiple-thread tasks, this method will allow us to suspend an event while there's a loop running at the same time. This means that there's a loop stopped while an await statement finishes it's execution. 

In our example, we have just little time setted, but this is useful when we code lots of tasks and we wanna set loop-running events suspended or doing something else while the main execute finishes. 

Now, see at the final code block. 

```python
if __name__ == "__main__":
    asyncio.run(main())
```

Here's a useful [doc](https://realpython.com/if-name-main-python/) why ```if __name__ == "__main__"``` is so important in Python and why we should include this in all our Python codes. We should look what we can see next. 

As I wrote before, you need to call a function to be executed, otherwise, it will be more statically than useful. (Yea, your code will impress even a farmer lol). Well, a programmer knows this and it's important in any compilated/interpreted programming language. In Python,  we call any function by the function's name and the main args if it has. In the first example, I typed ```main()``` to call the main function, so refering as the last example, we can suppose that we call it like in the first example. Is this true? 

Check what happens if we run our code with ```main()``` instead of ```asyncio.run(main())```:

```
$ python3 some_code.py
/home/user/some_code.py:32: RuntimeWarning: coroutine 'main' was never awaited
  main()
RuntimeWarning: Enable tracemalloc to get the object allocation traceback
$
```
In simple words, the ```main()``` function is not actually awaited due of not being really a concurrent task, calling it as a not regular asynchronous function. If u are a curious programmer, ```tracemalloc``` is just a Python debugger module to trace memory blocks disabled. Check [this](https://docs.python.org/3/library/tracemalloc.html) for more info. 

Now, remember that each object is stored in a memory location. In C/C++, pointers are really important, they allow us a programmers to know where is our object. I'm not going to write C/C++ code here because is not the main objective, but in Python, we can note that every async objects is allocated in a memory location once I already setted in my code. 

Also, I'ma tell you that the ```await``` key word is not valid if we wanna code an awaiting object outside the async function, so it's important to take this in consideration. This is the error showed in your console:

```
$ python3 some_code.py
File "/home/user/some_code.py", line 12
    await main()
    ^^^^^^^^^^^^
SyntaxError: 'await' outside function
$
```
Now, after all of this, I need to set an object while another object is being executed and it's already noted that this is an asynchronous code with multiple threads setted on. 

I need you to understand this, because this will solve our doubt why we use ```asyncio.run(main())``` to run our function, so in order to this, let's introduce a new important object based on TAP. A coroutine is an object used in async programming to be scheduled in case of suspending it and then being executed again. It's based on our syntax we stablished before (async/await), so at the time we are scheduling an object, we are scheduling a coroutine to be awaited in case we wanna do it (Usually yes). Also, as I mentioneed before in this doc, there's an event-loop running while a function is being awaited, due of having multiple threads. At this point, we can call 'em as subroutines, because at the end, it's just a sequence of instructions performing a specific task. 

```asyncio.run(main())``` let us to run a event-loop coroutine in order for each function awaited, then to be executed.

***

I mentioned what's a task and how it's performed during an execution inside an async block code. But now we run into another doubt: Is it possible to create our own tasks, avoiding an unquote object blocked by an another awaitable object? Or in simple words: Execute a task while another is awaiting? Yes and I'm gonna show you:

```python
# By Yayo
import asyncio
import time

async def test(word: str):
    print(word)
    await asyncio.sleep(1)

async def main():
    print("Time started at: ", time.strftime('%X'))
    
    print("Task 1 Done")
    task_created = asyncio.create_task(test(word="Task 2 Done"))
    print("Task 3 Done")

    await asyncio.sleep(1)

    for i in range(0, 3):
        print("Looped task 4 Done")
    
    print("Time finished at: ", time.strftime('%X'))

if __name__ == "__main__":
    asyncio.run(main())
```

This is what your console should show:

```
$ python3 some_code.py
Time started at:  10:29:39
Task 1 Done
Task 3 Done
Task 2 Done
Looped task 4 Done
Looped task 4 Done
Looped task 4 Done
Time finished at:  10:29:40
$
```
In this snippet code, I'm showing you how to create a task with asyncio using ```asyncio.create_task()```, and showing you when a task is being either awaited or executed. 

```asyncio.create_task()``` is a method that allows us to create a task, but it's important to note that this method is not a coroutine, so we can't await it. 
