### Numbers and Math operations

All the below methods were taken from the [Documentation](https://docs.python.org/3/library/stdtypes.html).

<pre><code>


		#Numbers
		num1 = 20
		num2 = 1.5
		 
		type(num1) #checking the type of this variable; integer
		type(num2) #checking the type of this variable; float
		 
		#Numbers - math operations
		2 + 2 #addition
		 
		0 – 1 #subtraction
		 
		46/ 2 #division
		 
		42 * 2 #multiplication
		 
		3 ** 2 #raising to a power
		 
		11 % 2 #modulo (this means finding out the remainder after division of one number by another)
		 
		#Numbers - float division vs. integer division (special case)
		5 / 2 #float division; result is 1 in Python 2 and 1.5 in Python 3
		 
		5 // 2 #integer division; result is 1 in Python 2 and Python 3
		 
		#Numbers - order of evaluation in math operations
		#Highest priority: raising to a power; Medium priority: division, multiplication and modulo; Low priority: addition and subtraction
		100 - 5 ** 2 / 5 * 2 #1st: 5 ** 2, second: / then *, third - ; result is 90.0
		 
		#Numbers - conversion between numeric types
		int(3.5) #result is 3
		 
		float(3) #result is 3.0
		 
		#Numbers - useful functions
		abs(3) #the distance between the number in between parantheses and 0
		 
		abs(-5) #returns the same result as abs(5)
		 
		max(1, 3) #returns the largest number
		 
		min(1, 3) #returns the smallest number
		 
		pow(3, 3) #another way of raising to a power
</code></pre>
