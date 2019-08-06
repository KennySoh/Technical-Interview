# Python 3  
"weakly typed" language    
  
**Variable type**
Int=3, Float=3.0, String=”Words” (‘w’, “w”, “””w”””, ‘’’w’’’)

**List** (Mutable Type -> References point to same place)  
```python
# Declaring a new list , list can have a mixture of variables
x=[“ham”,4.22,5] 

# Accessing list
print(x[0]) #prints "ham"

# Checking if list is empty
if a==[]: 
  print “list is empty”
  
##deep copying for deep arrays
list1=list2                       #list1 points to same reference as list2
list1=list2[:]                    #list1 points to a copy of list2, changes in list2 does not affect list1
from copy import deepcopy       # or import copy
list2=deepcopy(list1)         	#works for deep list



```
Starting : **x=[“ham”,4.22,5]**  

|Function            | Description           | Result|
|:-------------:|:-------------:|:-------------:|
| x.append(5)                   | #Add stuff into list                              |[“ham”,4.22,5,5]|
| x.insert(0,3.1)               | #Insert stuff into the list                       |[3.1,“ham”,4.22,5] |
| x.pop(1)                      | #remove stuff from the list                       |[“ham” ,5]   |
| len(x)                        | #number of items in list                        |len([“ham”,4.22,5])  returns 3    |
| list(“ham”)                   | #converting string into list                    |[“h”,”a”,”m”]              |
| in | Tree Insert              | #check if item is in list                       |“ham” in x… returns True, “h” in x… returns False|
| x[0],x[1]                     | #first item, second item                        |“ham”,4.22      |
| x[1:3]                        | #slicing the list                               |[“4.22”,5]  2nd item to 4th item not including 4thitem |
| x[1:3:2]	                    | #slicing increase increment                     |[“4.22”] increased increment to 2 |
| x[::-1]                       | #reverse the list                               |[1,2,3]>>>[3,2,1]    |
| x= [“c”]+x                    | #adding a list in front                         |                 |
| x*2                           | #repeat 2 times                                 | [“ham”,4.22,5,“ham”,4.22,5]   |
| list.index(“ham”)             | #returns the index of first found variable      |                          |
| list.sort()                   |#arrange from lowest to highest                  | [1, 2, 3, 4]| 

**Tuple** (Similar to List, use less memory and not adjustable)   
(Immutable Type ->  So their id(), the spot they point to in memory, changes.)  
```python
x=(“ham”,4.22,5)
x[1] #calling a tuple same as list

#Error
x[1]=3 #immutable cant be changed
```  
  
**Dictioanries: aka hashtables and maps**  
(Mutable Type)
```python
# Declaring dictioanry
exDict={‘Jack’:[15,’blonde’],’Bob’:[22,’brown’]}
print(exDict[“Jack”][1])

#Accessing and adding new key,value
mydict = {"cat":12, "dog":6, "elephant":23}
mydict["mouse"] = mydict["cat"] + mydict["dog"]
print(mydict["mouse"]) # ans =6+12=18

#getting a list of keys()
dict1.keys()
```

## Recursion
Base case (terminating), Recursion

```python
# Complete the jumpingOnClouds function below.
def jumpingOnClouds(c):
    # inputs:  (list) c
    # outputs: (int) minNumJump
    # Recursion: 2 case 
    #   1) Jump 2 and succed  
    #   2) Jump 2 and fail / Jump 1 (reduce c_list)
    # Terminating case
    #   1) if there 1 jump left
    #   2) if there 2 jump left 
    
    jumps=0;
    jumpsLeft=len(c);
    #Termintating
    if(jumpsLeft==3 or jumpsLeft==2):
        #end
        jumps=1
        print("end jump")
        print(jumps)
        return jumps
        #add to jump and return
    else:
        #Recursion
        if(c[2]==0):
            #jump2 Success
            print("jump2")
            jumps=1
            jumps =jumpingOnClouds(c[2:len(c)])+jumps
            print(jumps)
            return jumps
        else:
            #jump1 
            print("jump1")
            jumps=1
            jumps =jumpingOnClouds(c[1:len(c)])+jumps
            print(jumps)
            return jumps

```
