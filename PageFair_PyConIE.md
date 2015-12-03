This is a cool quiz from the guys at [PageFair](https://pagefair.com/) at their PyCon Dublin booth:

## Question 1

```python
def f(x=[]):
  x.append(1)
  return x

f()
print f()
```

## Choices: 
> 1. `[]`
> * `[1]`
> * `[1,1]`
> * `Throws an error.`

## Answer:

    [1, 1]


**Explanation**: Python's default arguments are evluated once when the function is defined, not each time the function is called.

----


## Question 2

```python
name = 'snow store'
name[5] = 'X'
print name
```

## Choices

> 1. `snow Xtore`
> *  `Throws an Error`
> *  `snowXstore`
> *  `X`

## Answer:

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-2-48b4801957d2> in <module>()
          1 name = 'snow store'
    ----> 2 name[5] = 'X'
          3 print name


    TypeError: 'str' object does not support item assignment


**Explanation**: Python strings are immutable

----

## Question 3

```python
import re
sum = 0
pattern = 'back'
if re.match(pattern, 'backup.txt'):
    sum += 1
if re.match(pattern, 'text.back'):
    sum += 2
if re.match(pattern, 'backup.txt'):
    sum += 4
if re.match(pattern, 'text.back'):
    sum += 8
print sum
```

## Choices

> 1. 7 
> 2. 15
> 3. 12
> 4. 5

## Answer

    5


**Explanation**: re.match checks if the pattern exists at the start of the string, so there is no match for 'text.back'

----

## Question 4

```python
aList = [1,2]
bList = [3,4]

kvps = {'1': aList, '2': bList}
theCopy = kvps.copy()

kvps['1'][0] = 5

sum = kvps['1'][0] + theCopy['1'][0]
print sum
```

## Choices

> 1. 10  
> * 6
> * 2
> * 8

## Answer

    10


**Explanation**: The copy method provides a shallow copy, therefore the list being held as the value inside the dictionary is the same list in the copy as the original

----

## Question 5 

```python
name = 'snow storm'
print '%s' % name[6:8]
```

## Choices

> 1. sto
> * so 
> * tor
> * to

## Answer

    to


**Explanation**: Slices the string from index 6 to index 8 not including index 8. The firest character in string is position 0

----

## Question 6

```python
class NumFactory:
    def __init__(self, n):
        self.val = n
    def timesTwo(self):
        self.val *= 2
    def plusTwo(self):
        self.val += 2
        
f = NumFactory(2)
for m in dir(f):
    mthd = getattr(f,m)
    if callable(mthd):
        mthd()
        
print f.val
```

## Choices

> 1. 8
> * 4
> * Throws an Error
> * 2

## Answer


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-10-f50edb0aa21e> in <module>()
         11     mthd = getattr(f,m)
         12     if callable(mthd):
    ---> 13         mthd()
         14 
         15 print f.val


    TypeError: __init__() takes exactly 2 arguments (1 given)


**Explanation**: Exception is thrown when trying to call __init__ mehtod of the object without any parameters: 

----

## Question 7

```python
class Person:
    def __init__(self, id):
        self.id = id

obama = Person(100)
obama.__dict__['age'] = 49
print obama.age + len(obama.__dict__)
```

## Choice

> 1. 51 
> * 100
> * 49
> * 149

## Answer

    51


**Explanation**: We have created a member variable named 'age' by adding it directory to the objects dictionary, so there are 2 items in the dictionary: 'age' and 'id'

----

## Question 8

```python
gen = (c for c in 'pycon')
set1 = set(gen)
set2 = set(gen)
print 'p' in set1, 'y' in set2
```

## Choices

> 1. True True
> *  False False
> *  Throws an error
> *  True False

## Answer

    True False


**Explanation**: Generator expression returns the characters of 'pycon' when creating set1 but has nothing to return when creating set2

----

## Question 9

```python
# Which of these are NOT a built-in function? 
any, bin, decimal, format
```

## Choices

> 1. all of the above are not built-in
> * decimal
> * bin
> * format


## Answer

    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-14-96a2976054ce> in <module>()
          1 # Which of these are NOT a built-in function?
    ----> 2 any, bin, decimal, format
    

    NameError: name 'decimal' is not defined


----

## Question 10

```python
# A coin is tossed three times. What is the probability
# that it lands on heads exactly one time?
```

[out]:

> If you toss a coin three times, there are a total of 
> 8 possible outcomes.
> HHH, HHT, HTH, THH, HTT, THT, TTH, and TTT

> Of the 8 possible outcomes, 3 have exactly one head,
> HTT, THT, TTH. Therefore the possibility that 3 flips
> of a coin will produce exactly one head is 3/8 = 0.375
