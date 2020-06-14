### Dictionaries

Dictionaries as also known as associative arrays. It consists in a collection of key-value pairs. In other words, each key-value maps to an associate value. [LINK](https://docs.python.org/3/whatsnew/3.7.html)

*Pay attention to the changes in the latest Python's version*

<pre><code>

#Dictionaries - a dictionary is an unordered set of key-value pairs
dict1 = {} #creating an empty dictionary
 
dict1 = {"Name": "Ana", "Age": "28", "Job": "Engineer", "Company": "Apple"}
 
dict1["Name"] #returns "Ana"; extracting a value for a specified key
 
dict1["Age"] = "28" #modifies an existing key-value pair
#and so on
 
 
del dict1["Age"] #deleting a key-value pair from the dictionary
 
len(dict1) #returns the number of key-value pairs in the dictionary
 
"Name" in dict1 #verifies if "IOS" is a key in the dictionary
 
"Surname" not in dict1 #verifies if "IOS2" is not a key in the dictionary
 
#Dictionaries - methods
dict1.keys() #returns a list having the keys in the dictionary as elements
 
dict1.values() #returns a list having the values in the dictionary as elements
 
dict1.items() #returns a list of tuples, each tuple containing the key and value of each dictionary pair
 
#Conversions between data types
str() #converting to a string
int() #converting to an integer
float() #converting to a float
list() #converting to a list
tuple() #converting to a tuple
set() #converting to a set
bin() #converting to a binary representation
hex() #converting to a hexadecimal representation
int(variable, 2) #converting from binary back to decimal
int(variable, 16) #converting from hexadecimal back to decimal

</pre></code>
