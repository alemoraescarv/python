### Strings

All the below methods were taken from the [documentation](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str).

*Some methods such as {}.format are very useful when coding complex logics.*

<pre><code>
#Defining a string on multiple lines, using triple quotes and the line continuation character ( \ )
my_string = '''My/ first/ string'''
 
#Strings - indexing
a = "Switch"
 
a.index("i")
#returns the index of i  

a.count("i")
#returns how many i there are inside the word/phrase
 
#Strings - finding a charact
a.find("tch")
 
#Strings - converting the case
a.lower() #lowercase
 
a.upper() #uppercase
 
#Strings - checking whether the string starts with a character
a.startswith("C")
 
#Strings - checking whether the string ends with a character
a.endswith("h")
 
#Strings - removing a character from the beginning and the end of a string
a = "   Switch   "
 
a.strip() #remove whitespaces
 
b = "$$$Switch$$$"
 
b.strip("$") #remove a certain character
 
#Strings - removing all occurrences of a character from a string
a = "   Switch Switch   "
 
a.replace(" ", "") #replace each space character with the absence of any character
 
#Strings - splitting a string by specifying a delimiter; the result is a list
a = "Alex,Robert, Leo, Mary" #the delimiter is a comma
 
a.split(",")
 
#Strings - inserting a character in between every two characters of the string / joining the characters by using a delimiter
a = "Cisco Switch"
 
"_".join(a)
 
capitalize()
#Capitalizes first letter of string.
 
lstrip()
#Removes all leading whitespace in string.
 
rstrip()
#Removes all trailing whitespace of string.
 
swapcase()
#Inverts case for all letters in string.
 
title()
#Returns "titlecased" version of string, that is, all words begin with uppercase and the rest are lowercase.
 
isalnum()
#Returns true if string has at least 1 character and all characters are alphanumeric and false otherwise.
 
isalpha()
#Returns true if string has at least 1 character and all characters are alphabetic and false otherwise.
 
isdigit()
#Returns true if string contains only digits and false otherwise.
 
islower()
#Returns true if string has at least 1 cased character and all cased characters are in lowercase and false otherwise.
 
isnumeric()
#Returns true if a unicode string contains only numeric characters and false otherwise.
 
isspace()
#Returns true if string contains only whitespace characters and false otherwise.
 
istitle()
#Returns true if string is properly "titlecased" and false otherwise.
 
isupper()
#Returns true if string has at least one cased character and all cased characters are in uppercase and false otherwise.
 
#Strings - concatenating two or more strings
a = "Tree"
b = "2691"
 
a + b
 
#Strings - repetition / multiplying a string
a = "Tree"
 
a * 3
 
#Strings - checking if a character is or is not part of a string
a = "Tree"
 
"o" in a
 
"b" not in a
 
#Strings - formatting v1
"Cisco model: %s, %d WAN slots, IOS %f" % ("2600XM", 2, 12.4)
"Cisco model: %s, %d WAN slots, IOS %.f" % ("2600XM", 2, 12.4)
"Cisco model: %s, %d WAN slots, IOS %.1f" % ("2600XM", 2, 12.4)
"Cisco model: %s, %d WAN slots, IOS %.2f" % ("2600XM", 2, 12.4)
 
#Strings - formatting v2
"Cisco model: {}, {} WAN slots, IOS {}".format("2600XM", 2, 12.4)
"Cisco model: {0}, {1} WAN slots, IOS {2}".format("2600XM", 2, 12.4)

</code></pre>

