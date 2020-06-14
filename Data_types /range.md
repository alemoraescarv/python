### Ranges

[Link](https://docs.python.org/3/library/stdtypes.html#ranges) for the documentation.

*Attention for the diffenrece between Python 2 and Python 3 (it is advisable to use Python 3)*

```python

#Ranges - unlike in Python 2, where the range() function returned a list, in Python 3 it returns an iterator; cannot be sliced
range1 = range(9)   #defining a range
 
range1
#Result: range(0, 9) 
 
type(range1)
<class 'range'> #the result
 
list(range1) #converting a range to a list
#Result: [0, 1, 2, 3, 4, 5, 6, 7, 8]  
 
list(range1)[2:5]    #slicing a range by using the list() function first
#Result: [2, 3, 4]   

</code></pre>

