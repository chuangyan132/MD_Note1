# Note in Frauenhofer project
## Python
### How to understand staticmethod
### How to understand type hint in function 
```python
def greeting(name: str) -> str:
    '''
    # type hint: its been used to indicate the type of the parameter and the return value of the function
    # the type hint is not enforced by the Python interpreter, but it can be used by static analysis tools to check for type consistency
    '''


    return 'Hello, ' + name
```

### How to understand async def
```python
async def fetch_data(url):
    '''
    # async def: it defines an asynchronous function that can perform non-blocking I/O operations
    # it allows the function to pause its execution while waiting for I/O operations to complete
    # it can be used with the await keyword to pause the function and resume it when the awaited operation is complete
    '''
    response = await aiohttp.get(url)
    return response
```


