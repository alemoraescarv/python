### Tuples

Tuples are sequences just like lists and a tuple is also immutable. While with lists parentheses are used, with tuples brackets are used.[LINK](https://docs.python.org/3.3/tutorial/datastructures.html#tuples-and-sequences)


```python

#Tuples - immutable lists (their contents cannot be changed by adding, removing or replacing elements)
tuple = () #creating an empty tuple
 
tuple = (9,) #creating a tuple with a single element; DO NOT forget the comma
 
tuple = (1, 2, 3, 4)
 
# Same indexing & slicing rules apply as for strings and lists
len(tuple) #returns the number of elements in the tuple
 
tuple[0] #returns the first element in the tuple (index 0)
tuple[-1] #returns the last element in the tuple (index -1)
tuple[0:2] #returns (1, 2)

 
#Tuples - tuple assignment / packing and unpacking
tuple = ("Robert", "175", "32")
 
(Eng, USA, 28) = tuple1 #Eng will be mapped to "Robert" and so are the rest of the elements with their corresponding values; both tuples should have the same number of elements
 
(a, b, c) = (1, 2, 3) #assigning values in a tuple to variables in another tuple
 
min(tuple) #returns "32"
 
max(tuple) #returns "Robert"
 
tuple1 + (5, 6, 7) #tuple concatenation
 
tuple * 20 #tuple multiplication
 
"32" in tuple #returns True
 
784 not in tuple #returns True
 
del tuple #deleting a tuple

```
