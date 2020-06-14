### Loops

The basics of loops in Python.


<pre><code>
#For / For Else loops - executes a block of code a number of times, depending on the sequence it iterates on; the "else" clause is optional
names = ["Alex", "Anna", "Robert", "Ivy", "Mary"]
 
for name in names: #interating over a sequence and executing the code indented under the "for" clause for each element in the sequence
    print(name)
else: #the indented code below "else" will be executed when "for" has finished looping over the entire list
    print("The end of the list has been reached")
   

</code></pre>

- While/While-else

<pre><code>
#While loop executes as long as an user-specified condition is evaluated as True; the "else" clause is optional
x = 1
 
while x <= 10:
    print(x)
    x += 1
else:
    print("Out of the while loop. x is now greater than 10")
 
#result of the above "while" block
#1 2 3 4 5 6 7 8 9 10
#Out of the while loop. x is now greater than 10

</code></pre>

- Break/Continue/Pause

<pre><code>
for i in list1:
    for j in list2:
        if j == 20:
            break #stops the execution here, ignores the print statement below and completely quits THIS "for" loop; however, it doesn't quit the outer "for" loop, too!
        print(i * j)
    print("Outside the nested loop")
    
for i in list1:
    for j in list2:
        if j == 20:
            continue #ignores the rest of the code below for the current iteration, then goes up to the top of the loop (inner "for") and starts the next iteration
 
 for i in range(10):
    pass #pass is the equivalent of "do nothing"; it is actually a placeholder for when you just want to write a piece of code that you will treat later
</code></pre>
