### Exceptions

*Attention:* The syntax for exception handling has changed in Python 3. Thus, make sure you are using Python 3 to properly use the syntax below.
Below 'ZeroDivisionError' is used, but it is possible to customise the error it will be handled.

```python
#Handling an exception: telling Python to keep executing the rest of the lines of code in the program
#"try" clause you insert the code that you think might generate an exception at some point
try:
    print(1/0) 
except ZeroDivisionError:
    print("Division Error!") #specifying what exception types Python should expect as a consequence of running the code inside the "try" block and how to handle them
else:
    print("No exceptions raised by the try block!") #executed if the code inside the "try" block raises NO exceptions
finally:
    print("I don't care if an exception was raised or not!") #executed whether the code inside the "try" block raises an exception or not
 
#result of the above block
#Division Error!
```
