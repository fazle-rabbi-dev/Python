<h2 align="center"> 

Object Oriented Programming

</h2>

<p id="index"></p>

1. [Class](#Class)
   * [self & __init__](#)
   * [Class Method](#ClassMethod)
   * [Class Method As Constructor](#classMethodAsConstructor)
   * [Static Method](#StaticMethod)
   * [Public,Protected,Private access specifiers](#accessModifier)
2. [Object](#Object)
3. `Inheritance`
   * [Super & Overriding](#Super)
   * [Single/Hierarchical](#singleInheritance) 
   * [Multiple](#multipleInheritance) 
   * [Multilevel](#multilevelInheritance) 
   * [Operator Overloading & Dunder Method](#operatorOverloading) 
4. `Abstruction`
5. `Encapsulation`
6. `Polymorphism`
7. [Magic Method](#Magic)

<p id="Class"></p>

### Class
* *Class is a blueprint/template*
```py
class Person():
   def __init__(self,name,age):
      self.name = name
      self.age = age
      
   def __str__(self):
      return f'Name: {self.name}\nAge: {self.age}'
      
Karim = Person('Karim',20)
print(Karim)

```

[Back To Top](#index)

<p id="Object"></p>

### Object
* **
```py
class Person():
   def __init__(self,name,age):
      self.name = name
      self.age = age
      
   def __str__(self):
      return f'Name: {self.name}\nAge: {self.age}'

# object/instance:     
Karim = Person('Karim',20)
print(Karim)

```

[Back To Top](#index)

<p id="ClassMethod"></p>

### Class Method
* ***it is used for access class from a class method!***
```py
class Student():
   id_number = 98
   
   def __init__(self,name,age):
      self.name = name
      self.age = age
      
   @classmethod
   def change_id(cls,new_value):
      # cls --> class of an instance
      cls.id_number = new_value

obj = Student('John',20)
# obj.id_number = 99
# Student.id_number = 99
Student.change_id(99)
print(Student.id_number)
```
### 
```py

```

[Back To Top](#index)

<p id="classMethodAsConstructor"></p>

### Class Method As Constructor
```py
class Student():
   def __init__(self,name,age):
      self.name = name
      self.age = age
   
   @classmethod
   def demo(cls,name,age):
      return cls(name,age)
   
   # classmethod as constructor
   @classmethod
   def set_values(cls,string):
      string = string.split('-')
      # print(string)
      return cls(string[0],string[1])

obj = Student.demo('john',20)
obj2 = Student.set_values('karim-20')
print(obj2.name)
```

[Back To Top](#index)

<p id="StaticMethod"></p>

### Static Method
* ***in a staticmethod (self) is not required!***
```py
class Student():
   def __init__(self,name,age):
      self.name = name
      self.age = age
      
   @staticmethod
   def say_hi():
      print('Hii!')
   
obj = Student('john',20)
obj.say_hi()
```

[Back To Top](#index)

<p id="accessModifier"></p>

### Public,Protected,Private
```py
class Person:
   ID = 99 # public
   _apiUrl = 'https://example.com' # protected
   __isActive = False # private
   
print(Person.ID)
print(Person._apiUrl)
print(Person._Person__isActive)

```

[Back To Top](#index)

<p id="Super"></p>

### Super & Overriding
```py
class Person:
   def __init__(self,name):
      self.name = name
   
   @staticmethod
   def say_hi():
      print('Hi')
      
   
class Student(Person):
   # __init__ will be override here!
   def __init__(self,name,age):
      # self.name = name
      super().__init__(name) # keeps old constructor
      # call the method of parent class:
      super().say_hi()
      self.age = age

A = Student('Rahim',20)
print(A.name)
print(A.age)

```

[Back To Top](#index)

<p id="singleInheritance"></p>

### Single Inheritance
```py
# Parent Class
class Person():
   def __init__(self,name,age):
      self.name = name
      self.age = age
      
   def __str__(self):
      return f'Name: {self.name}\nAge: {self.age}'

# Child Class
class Student(Person):
   pass

# Instance
Rahim = Student('Rahim',22)
print(Rahim.name)
```

[Back To Top](#index)

<p id="multipleInheritance"></p>

### Multiple Inheritance
* ***This means --> 1 class inherit Multiple-Class***
```py
class Person:
   def __init__(self,name,age):
      self.name = name
      self.age = age
 
 
class Player:
   def __init__(self,hobby):
      self.hobby = hobby

# in (Player,Person) --> first class got max priority!
class Student(Player,Person):
   pass

# Instance
# Rahim = Student('Rahim',22,['Cricket','Vollyball'])
Rahim = Student('coding')
print(Rahim.hobby)
```

[Back To Top](#index)

<p id="multilevelInheritance"></p>

### Multilevel Inheritance
```py
class Parent:
   eye_color = 'Brown'

class Child(Parent):
   eye_color = 'Gray'

class Grand_Child(Child):
   # eye_color = 'Black'
   pass

A = Grand_Child()
print(A.eye_color)
# --> at first search in the Grand_Child class
# if not found :
# --> then, search in the Child class
# if not found :
# --> then, search in the Parent class


```

[Back To Top](#index)

<p id="operatorOverloading"></p>

### Operator Overloading and Dunder method
* Dunder method --> `same as magic method`
```py
class Employee:
   def __init__(self,name,sallary):
      self.name = name
      self.sallary = sallary
   
   # this method help for operator overloading
   def __add__(self,other):
      return self.sallary+other.sallary
   
   def __repr__(self):
      return f'Employee({self.name},{self.sallary})'
   
   def __str__(self):
      return f'Name: {self.name},sallary:{self.sallary}'
   

A = Employee('john',200)
B = Employee('harry',300)

print(A+B)
print(A)
print(repr(B))

```

[Back To Top](#index)

<p id="Abstruction"></p>

### Abstruction
```py
from abc import ABC,abstractmethod

# abstract based class
class Person(ABC):
   @abstractmethod # this method must use in the child class!
   def eye_color(self):
      pass

class Player(Person):
   def eye_color(self):
      return 'Blue'

A = Player()
print(A.eye_color())

```
[Back To Top](#index)

<p id="Magic"></p>

### Magic Method
```py
__str__()
__gt__(item1,item2)
__lt__()
__eq__()
```

[Back To Top](#index)
