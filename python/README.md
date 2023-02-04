<!--<h1 align="center">Python Notes</h1>-->

<h1 align="center">
Python Notes
</h1>

<p id="funda"></p>

### `Fundamentals`
* [Variables](#)
* [Operators](#)
* [Comments](#)
* [Data types](#)
* [Numbers](#)
* [Casting](#)
* [Strings](#)
* [List](#)
* [Tuple](#)
* [Dictionary](#)
* [Set](#)
* [Conditions](#)
* [Loops](#)
* [Functions](#)
* [Lambda](#)
* [User input](#)
* [pip](#)

<p id="inter"></p>

### `Intermediate`
* [OOP](oop.md)
* [File Handling](#)
* [Error and exception handling](#)
* [Custom Exception](#)

<p id="advanced"></p>

### `Advanced`
* [Modules](#)
* [Import Modules From Different Directory](#importFromOtherDir)
* [Use Environment Variable](#useEnv)
* [Decorators](#Decorators)
* [List Comprehension](#Comprehension)
* [Map & Filter](#map)
* [Zip Function](#zip)
* [Enumerate Function](#Enumerate)
* [If __name__ == '__main__' usage](#name)
* [Join Function](#join)
* [Using Else With For Loops](#)
* [Function Caching](#Caching)
* [SQLite](#)
* [Regular Expression](#regex)
* [iterators](#)
* [Virtual env and requirements.txt](#venv)
* [Convert .py to .exe](#)
* [Command Line Arguments](#commandlineargs)

<p id="module"></p>

### `Built In Modules`
* [Os Module](#os)
* [Request Module](#request)
* [Pickle Module](#pickle)
* [Random Module](#random)
* [Sys Module](#sys)
* [Json Module](#)
* [Time Module](#)

### `How To?`
* [Send email]()

----


<p id="importFromOtherDir"></p>

### Import Module From Another Directory
* **Method 1**
```py
import sys,os
sys.path.insert(0, os.path.join(os.getcwd(),"MyModule"))

# Now use import  ...
```

* **Method 2**
```py
export PYTHONPATH='path/to/directory'
```

<p id="useEnv"></p>

### Use Environment Variable
```py
# Method 1
from decouple import config
uri = config("uri")

# Method 2
from dotenv import dotenv_values
config = dotenv_values(".env") 
# config --> rerurn dictionary data!

```

<p id="Decorators"></p>

### Decorators
```py
def style(func):
   print('=====----=====')
   func()
   print('=====----=====')

@style
def test():
   print('Hello')
```
[⬆ Back To Top](#inter)


<p id="Comprehension"></p>

### List Comprehension
```py
fruits = ['apple','orange','banana']

[print(item) for item in fruits]

new_list = [item for item in fruits]
print(new_list)
```
[⬆ Back To Top](#inter)


<p id="map"></p>

### Map & Filter
```py
# Map
fruits = ['apple','orange','banana']
def func(item):
   return '*'+item+'*'
r = list(map(func,fruits))
print(r)

# Filter
ages = [5, 12, 17, 18, 24, 32]
def func(age):
   if age >= 18:
      return age
r = list(filter(func,ages))
print(r)

```
[⬆ Back To Top](#inter)


<p id="zip"></p>

### Zip Function
```py
LIST1 = ['name','age']
LIST2 = ['John Doe','23']

new_list = zip(LIST1,LIST2)
new_list = list(new_list)
print(new_list[0][1])
for i in new_list:
   print(i)

```
[⬆ Back To Top](#inter)


<p id="Enumerate"></p>

### Enumerate Function
```py
fruits = ['apple','orange','banana','kiwi']
for index,item in enumerate(fruits):
   print(f'{index}: {item}')

for index, item in enumerate(fruits):
   if index%2 == 0:
      print(f'[*] Please Buy {item}')

```
[⬆ Back To Top](#inter)


<p id="name"></p>

### if __name___ == '___main__'
```py
# When the program run by it's name, then the value of __name___ == '___main__'
# When the program run by others module, then the value of __name___ == 'filename'
```
[⬆ Back To Top](#inter)


<p id="join"></p>

### Join Function
```py
fruits = ['apple','orange','banana']
print('# '.join(fruits))
```
[⬆ Back To Top](#inter)


<p id="Caching"></p>

### Function Caching
```py
from functools import lru_cache
import time

@lru_cache()
def some_work(n):
   time.sleep(n)

print('Loading.')
some_work(1)
print('Loading..')
some_work(1)
print('Loading...')
some_work(1)
print('Loading....')
```
[⬆ Back To Top](#inter)


<p id="venv"></p>

### Virtual env and requirements.txt
* pip install virtualenv
* virtualenv venv `method 1`
* virtualenv --system-site-package venv `method 2`
* source ./venv/scripts/active `for active`
* source ./venv/scripts/deactive `for deactive`
* ***Make requirements.txt***
* pip freeze > requirements.txt
* ***Install all the packages using requirements.txt***
* pip install -r requirements.txt

[⬆ Back To Top](#inter)


<p id="commandlineargs"></p>

### Command Line Arguments
```py
import argparse,sys
# make an instance
parser = argparse.ArgumentParser()
# add argument
parser.add_argument("--i",type=str,default=None,help='This is a help message')     
args = parser.parse_args()
print(args.i)

# Run This By The Following Way:
# python demo.py --i hello
```
[⬆ Back To Top](#inter)


<p id="os"></p>

### Os Module
```py
import os
os.getcwd()
os.chdir()
os.listdir()
os.mkdir()
os.makedirs()
os.rename()
os.environ.get('path')
os.path.join()
os.path.exists()
os.path.isfile()
os.path.isdir()

```
[⬆ Back To Top](#module)


<p id="request"></p>

### Request Module
```py
import requests

# Get request
url = 'https://jsonplaceholder.typicode.com/posts'
# res = requests.get(url)
# print(res.text)

# Post request
data = {
   'title':'smith'
}
res = requests.post(url,data=data)
print(res.text)

```
[⬆ Back To Top](#module)


<p id="pickle"></p>

### Pickle Module
* **This Module used for store the object in a file!**
```py
import pickle
names = ['john','harry','thapa']
file = open('rabbi.pkl','wb')
pickle.dump(names,file)
file.close()

# read binary data
file = open('rabbi.pkl','rb')
data = pickle.load(file)
print(data)
file.close()

```
[⬆ Back To Top](#module)


<p id="random"></p>

### Random Module
```py
import random

print(random.randint(1,10))
print(random.randrange(1,10))
print(random.choice(['apple','orange','banana']))
fruits = ['apple','orange','banana']
random.shuffle(fruits)
print(fruits)

```
[⬆ Back To Top](#module)

<p id="sys"></p>

### Sys Module
```py
import sys,os,time,json

# print(sys.modules) # --> list of imported module
# print(sys.argv) # --> print the command line arguments
# print(sys.platform) 
a = dir(sys)
print(json.dumps(a, indent=3))
print(a)

print(sys.__name__)

```
[⬆ Back To Top](#module)



