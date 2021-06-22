### Expression
```
1+1
1-1
1/2 
1*2

5/2=2.5 # float division
5//2=2  # integer division
3 * (2+6) / (2-1) //Paranthese
500323%10  # reminder, u will get 0-9

5**2 # to the power of 2
import math
math.pow(5,2) $ 5 to the power of 2
```

### Working with Numbers
```
help(round)

round(2.5) = 2
round(2.555,1) = 2.6

import math
math.ceil(3.3) = 4 # Round Up
math.floor(3.6) = 3 # Round Down

print("hello world")
```

### Variables
```
age=(10/5) + (3 *3) #important message
age_of_user = 7 #good

"""
This is a multi-line comment
"""
print(age)
```

### String
```
msg = "Hello Mike\nThis is an Email"
msg= "\n"     #New line
msg= "\t"     #Tab
msg = "\x41"  #Hexadecimal in ur Ascii table
msg = "\""    #Escape ur \"
msg = 'She said "eww"'

print(msg1+ "..."+ msg2) #String Concatenation
msg[0]  # string indexing
msg[5:] #string slicing, inclusive of the fifth index
msg[:5] # exclusive of the fifth index
msg[-1] #starting from the back of the string
msg[6:-3] #from 6 all the way to -3

task="Subscribe"
print(id(task)) #43339983

task="task"
print(id(task)) #4328921

task[0]="s" # returns error because string is immutable
len(task) = 5
print("your message"+str(len(task))+"character long)

```
### List 
```
ages = [12,18,28]
people=["Caleb","Sabrina","emily"]
my_favourite_things = ["Working out", 7, ['amazon prime', 'netflix']]
print(my_favourite_things[2][1]) #return netflix

# Copy a List , Shallow copy a list. ( Means list of different id references, one change doesnt change the other)
copy= my_favourite_things[:]
copy= my_favourite_things.copy()

#deep copying, all items in the list are copied.
import copy 
c= copy.deepcopy(my_favourite_things)

# List Append
list.append("list_item2")

# List Updating and Slicing
age[0] = 5
age[1] = 4
ages[1:] # list slicing
ages[1:]=[6,7] #Update the list 
```

### Input
```python3
print("Hey What's your name?")
name = input()
print("Hello, " + name)
print("What's your favourite number?")
fav_num=input()
print("Give us another number.")
fav_num2 = input()
print(fav_num +fav_num2)
```
### Data Type, Type Casting
```
type() #int, float, str
str()
float()
int()
```
### If else statements
```
if (x==1):
  print("Welcome to our app!")
elif (age>65):
  print("Hey, you get a special discount")
elif (age>20):
  print("Yay!")
else:
  print("You're not old enough")
```

### for loop 
```
for i in range(len(foods)):
  print(i, foods[i], end ="")
print()
```




