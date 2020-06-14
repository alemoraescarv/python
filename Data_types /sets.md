### Sets

Different from lists, Set is a unordered collection of elements which are **interable, mutable and it does not have duplicate elememts.**[LINK](https://docs.python.org/3/library/stdtypes.html#set-types-set-frozenset)
Whereas, the only difference to FrozenSet is that it is immutable.

<pre><code>

#Sets - unordered collections of unique elements
set1 = {"1.1.1.1", "2.2.2.2", "3.3.3.3", "4.4.4.4"} #creating a set
 
list1 = [11, 12, 13, 14, 15, 15, 15, 11]
string1 = "aaabcdeeefgg"
 
set1 = set(list1) #creating a set from a list; removing duplicate elements; returns {11, 12, 13, 14, 15}
 
set2 = set(string1) #creating a set from a string; removing duplicate characters; returns {'b', 'a', 'g', 'f', 'c', 'd', 'e'}; remeber that sets are UNORDERED collections of elements
 
len(set1) #returns the number of elements in the set
 
11 in set1 #returns True; checking if a value is an element of a set
 
10 not in set 1 #returns True; checking if a value is an element of a set
 
set1.add(16) #adding an element to a set
 
set1.remove(16) #removing an element from a set
 
#Frozensets - immutable sets. The elements of a frozenset remain the same after creation.
fs = frozenset(list1) #defining a frozenset
 
type(fs)
#Result: <class 'frozenset'>
 
#proving that frozensets are indeed immutable
fs.add(10)
#Result: AttributeError: 'frozenset' object has no attribute 'add'
 
fs.remove(1)
#Result: AttributeError: 'frozenset' object has no attribute 'remove'
 
fs.pop()
#Result: AttributeError: 'frozenset' object has no attribute 'pop'
 
fs.clear()
#Result: AttributeError: 'frozenset' object has no attribute 'clear'
 
#Sets - methods
set1.intersection(set2) #returns the common elements of the two sets
 
set1.difference(set2) #returns the elements that set1 has and set2 doesn't
 
set1.union(set2) #unifying two sets; the result is also a set, so there are no duplicate elements; not to be confused with concatenation
 
set1.pop() #removes a random element from the set; set elements cannot be removed by index because sets are UNORDERED collections of elements, so there are no indexes to use
 
set1.clear() #clearing a set; the result is an empty set

</code></pre>
