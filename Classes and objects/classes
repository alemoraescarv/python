###Classes

Summarizing, classes are objects constructors. Also, classes can inherit others.

```python
#creating a class which inherts from the default "object" class
class Person(object): 
#class constructor; initializing some variables and the method is called whenever you create a new instance of the class 
    def __init__(self, name, age, height): self.routername = routername #"self" is a reference to the current instance of the class
        self.name = name
        self.age = age
        self.height = height
 
    def print_router(self, job):
        print("The person's name is: ", self.name)
        print("The person's age is: ", self.age)
        print("The person's height is: ", self.height)
        print("The person's name and job are: ", self.name + job)

#creating an object by simply calling the class name and entering the arguments required by the __init__ method in between parentheses
p1 = Person('Ana', '28', '179') 

p1.name 
#returns Ana

p1.print_router("engineer") #accessing a function (actually called method) from within the class 
#it will print out all the info inside the method
 
#getting the value of an attribute 
getattr(p1, "name") 
 
#setting the value of an attribute 
setattr(p1, "age", "32") 

#checking if an object attribute exists
hasattr(p1, "job") 
 
#deleting an attribute
delattr(p1, "height")

#verifying if an object is an instance of a particular class
isinstance(p1, MyRouter) 
 
#creating a new class (child) inheriting from the Person parent class 
class Extra_info_person(Person): 
 
#returns True or False; checking if a class is the child of another class 
issubclass(Extra_info_person, Person) 
```
