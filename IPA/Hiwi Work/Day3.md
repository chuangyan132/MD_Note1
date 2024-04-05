# work memo
## What is RestructuredText?
- reStructuredText is a lightweight markup language that is used to create documents. It is easy to read and write, and it can be used to create documents in multiple formats, including HTML, PDF, and LaTeX.
## What is mermaid diagrams? link to advanced usage
- Mermaid is a simple markdown-like script language for generating charts from text via javascript. It is used to create diagrams and flowcharts in markdown documents. You can find more information about mermaid diagrams [here](https://mermaid-js.github.io/mermaid/#/).
## What is Quasar?
- Quasar is a Vue.js framework that is used to create responsive web applications. It provides a set of components and tools that make it easy to build modern web applications. You can find more information about Quasar [here](https://quasar.dev/).
- Quasar vs QT
  - both are used to create cross-platform applications
  - Quasar is based on Vue.js, while QT is based on C++
  - Quasar is more focused on web applications, while QT is more focused on desktop applications
  - Quasar is easier to learn and use, while QT is more powerful and flexible
## Python lambda
- Lambda functions in Python are small, anonymous functions defined using the lambda keyword. They can have any number of arguments but only one expression. The expression is evaluated and returned when the function is called. Lambda functions are particularly useful for short functions that are not complex enough to justify defining them with a separate def statement.
```python
from nicegui import ui

ui.button('Click me!', on_click=lambda: ui.notify('You clicked me!'))

ui.run()
```
## with in python
- The with statement in Python is used to simplify exception handling and resource management. It is used to wrap the execution
## decorator in python
- A decorator in Python is a design pattern that allows you to add new functionality to an existing object without modifying its structure. Decorators are implemented as functions that take another function as an argument and return a new function that adds the desired functionality. Decorators are commonly used to add logging, caching, and other cross-cutting concerns to functions.
- [Python Decorators](https://www.runoob.com/w3cnote/python-func-decorators.html)

## del in python
- The del statement in Python is used to delete an object or a variable. It can be used to delete variables, items from a list, attributes from an object, or slices from a list. When you delete an object, its reference count is decremented, and if the reference count reaches zero, the object is deleted from memory.

## async in python
- An async function is a function that can "pause" its execution while waiting for some operation to complete, allowing other operations to run in the meantime. Async functions are a foundational part of asynchronous programming in Python

## await in python
- This keyword is used to pause the execution of an async function until the awaited operation is completed. It can only be used inside async functions. await is commonly used for I/O-bound tasks, such as network operations, file I/O, or, as in this example, waiting for user interactions.
- async 是“异步”的意思，而 await 是等待的意思，await 用于等待一个异步任务执行完成的结果。

    async/await 是一种编写异步代码的新方法（以前是采用回调和 promise）。
    async/await 是建立在 promise 的基础上。
    async/await 像 promise 一样，也是非阻塞的。
    async/await 让异步代码看起来、表现起来更像同步代码。
- Understanding async and await
async: The async keyword is used to define a function as an "asynchronous coroutine." Coroutines are a core part of asynchronous programming in Python, allowing tasks to be suspended and resumed. An async function is a function that, when called, returns a coroutine object. It can include await expressions that pause the coroutine's execution until the awaited task is complete, without blocking the entire program.

await: The await keyword is used to pause the coroutine's execution until the awaited object is complete. await can only be used inside async functions. It's used for getting the result of an asynchronous operation, which allows other tasks to run in the meantime.

## Diaable a button with a context manager
```python
# an async-capable HTTP client for Python.
import httpx 
from contextlib import contextmanager
from nicegui import ui

@contextmanager
def disable(button: ui.button):
    button.disable()
    try:
        yield
    finally:
        button.enable()

async def get_slow_response(button: ui.button) -> None:
    with disable(button):
        async with httpx.AsyncClient() as client:
            response = await client.get('https://httpbin.org/delay/1', timeout=5)
            ui.notify(f'Response code: {response.status_code}')

ui.button('Get slow response', on_click=lambda e: get_slow_response(e.sender))

ui.run()
```
## contextmanager in python
- it  is a way to allocate and release resources precisely when you want to. The most common use is with the with statement.

## yield in python
- The yield statement in Python is used to create a generator function. When a generator function is called, it returns an iterator object but does not start execution immediately. The yield statement is used to produce a series of values one at a time, allowing the caller to iterate over the values as they are generated. This is useful for creating memory-efficient iterators that produce values on the fly rather than storing them all in memory at once.
- [Python yield](https://www.runoob.com/w3cnote/python-yield-used-analysis.html)

## joystick in python
- Joystick is a device that is used to control the movement of a cursor or other graphical elements on a computer screen. It consists of a stick that can be moved in different directions to control the movement of the cursor. Joysticks are commonly used in video games and other applications that require precise control over movement.

