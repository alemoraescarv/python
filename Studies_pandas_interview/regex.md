```python
import re

p="Hello, my name is Alex."

r = re.findall('\w+', p)


len=(len(r))
print(len)
for i in r:
    reverse=[]
    #print(i)
    reverse.insert(len, i)
    len-=1
    #print(reverse)
        
print(reverse)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-2-414d3af941d3> in <module>()
          6 
          7 
    ----> 8 len=(len(r))
          9 print(len)
         10 for i in r:


    TypeError: 'int' object is not callable



```python
p="Hello, my name is Alex."

rev=" ".join(reversed(p.split(' ')))
print(rev)
```

    Alex. is name my Hello,

