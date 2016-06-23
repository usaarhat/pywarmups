This is a fun quiz from the guys at [Acronis](http://www.acronis.com/) at their PyCon Singapore booth:

Question 1
====

What will be the output of the code below:

```python
list = ['a', 'b', 'c', 'd', 'e']
print list[10:]
```

**Answer:**

Now, if we overthink this, we'll think it's a trick question cos `list` is a keyword in Python. But in this case, Python will treat it as a variable name. In that case, the output would be an empty list, since you're trying to access a range of a list that won't be there:

```python
>>> list = ['a', 'b', 'c', 'd', 'e']
>>> print list[10:]
[]
```

The funny thing is when you want to return a range that don't exist in the list, Python returns an empty list but when you try to access an index that don't exists, it explodes in your face:

```python
>>> list = ['a', 'b', 'c', 'd', 'e']
>>> print list[10:]
[]
>>> print list[10]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
```

Back to the scary stuff, now that you have overwritten the `list` native keyword from Python, you won't be able to cast things into a list =( 

```python
>>> list = ['a', 'b', 'c', 'd', 'e']
>>> print list[10:]
[]
>>> print list[10]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
>>> atuple = ('a', 'b', 'c')
>>> atuple
('a', 'b', 'c')
>>> type(atuple)
<type 'tuple'>
>>> list(atuple)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'list' object is not callable
```

Normally, list casting would work if you don't override the keyword:

```python
>>> alist = ['a', 'b', 'c', 'd', 'e']
>>> print alist[10:]
[]
>>> atuple = ('a', 'b', 'c')
>>> type(atuple)
<type 'tuple'>
>>> list(atuple)
['a', 'b', 'c']
>>> type(list(atuple))
<type 'list'>
```

So lessons learnt:

 - Don't overthink the problem, Python allows quite flexiable variable names.
 - Don't try to use variable names that clashes with your namespace 
 
----
 
 
Question 2
====

What will be the output of the code below:

```python
[x ** 2 for x in range(5)]
```

This is an easy one but you might get stymied by the `**` operator, this is simply the square or power of 2 math operation. Here's a nice Stackoverflow to quirky operators: [What does these operators mean?](http://stackoverflow.com/questions/15193927/what-does-these-operator-mean-python)

**Answer:**

```python
>>> [x ** 2 for x in range(5)]
[0, 1, 4, 9, 16]
```

If we take a closer look and compare it to `x*x` and `math.pow(x,2)` is the same as using `x**2`:

```python
>>> [x ** 2 for x in range(5)]
[0, 1, 4, 9, 16]
>>> [x for x in range(5)]
[0, 1, 2, 3, 4]
>>> [x * x for x in range(5)]
[0, 1, 4, 9, 16]
>>> import math
>>> [math.pow(x,2)  for x in range(5)]
[0.0, 1.0, 4.0, 9.0, 16.0]
```

----

Question 3
====

What will be the output of the code below:

```python
value = 1
def change():
    value = 2
change()
print value
```

The obvious answer would be that "it would return a SyntaxError" since there's only 3 spaces instead of 4 after the definition of the `change():` function. But after asking the people at Acronis, they say treat it as 4 spaces instead of 3.

So the asnwer:

```python
>>> value = 1
>>> def change():
...     value = 2
... 
>>> change()
>>> print value
1
```

Now that's a tricky question. the global `value` variable doesn't change because when we call the `change()` function, it sets a local `value` within the function scope and once we get out of the function, this local variable gets thrown away.


And here's the more interesting fact, even if you pass in the `value` variable into a `change()` function that takes the `value` parameter, the global value still doesn't change:

```
>>> value = 1
>>> def change(value):
...     value = 2
... 
>>> change(value)
>>> print value
1
```

Even if we do silly things like adding a `return` to the `change()` function, it's still won't change the global `value` variable:

```python
>>> value = 1
>>> def change(value):
...     value = 2
...     return value
... 
>>> print value
1
```

**So the question is how do we change the global `value`?**

So there's 2 ways to do this, one is to "re-assign" the return value from `change()` to the global `value`:

```python
>>> value = 1
>>> def change():
...     value = 2
...     return value
... 
>>> value = change()
>>> print value
2
```

The other way is (IMHO) way cooler by using the `global` keyword inside the function scope and then whenever we access the variable `value` inside the function, it's referring to the global `value` variable.

```python
>>> value = 1
>>> def change():
...     global value
...     value = 2
... 
>>> change()
>>> print value
2
```

----

Question 4
====

What will be the output of the code below:

```python
value = [1]

def change():
   value.append(2)
   
change()
print value
```

Similarly, the obvious answer would be SyntaxError since there's only 3 spaces instead of 4. So let's assume that there's 4 spaces in the question. 

```python
>>> value = [1]
>>> def change():
...     value.append(2)
... 
>>> change()
>>> print value
[1, 2]
```

Ah ha! Now that's interesting, we have a `value` list in the global but now apparently, the function is change the global variable outside of its scope.

On StackOverflow, there's a good answer for this: http://stackoverflow.com/a/6329536/610569

So let's test it a little, below we'll see that if we try to change the existing element inside the global list, it doesn't change the element in the global list:

```python
>>> value = [1]
>>> def change():
...     value[0] = 2
... 
>>> print value
[1]
```

Ah, but we can append, why?! Now that brings us to a dark place of programming where we talk about:

 - mutation / mutable vs immutable
 - rebinding
 - copy by value 
 - copy by reference

A good starting point would be http://stackoverflow.com/questions/9073995/difference-between-mutation-rebinding-copying-value-and-assignment-operator

----

Question 5
====

Write a function that count and print number of words in given string. Word is a sequence of symbols without whitespaces.

For example, for input string "one one two one two three one two three four" your function should print:

```python
"one" : 4
"two" : 3
"three": 2
"four": 1
```

If we don't know how to solve a looping kinda problems in Python, the first thing to do is always to look into [`itertools`](https://docs.python.org/3.5/library/itertools.html) and [`collections`](https://docs.python.org/3.5/library/collections.html) where powerful functions are already coded and most probably optimized to do you looping. 

**Answer:**


```python
>>> from collections import Counter
>>> s = "one one two one two three one two three four"
>>> Counter(s.split())
Counter({'one': 4, 'two': 3, 'three': 2, 'four': 1})
>>> for k,v in Counter(s.split()).most_common():
...     print '"{}" : {}'.format(k,v)
... 
"one" : 4
"two" : 3
"three" : 2
"four" : 1
```

Question 6
====

Write a function that accepts nested lists of any depth and returns "flattened" list - list of elements from first list without sub lists.

For example:

```
[[[1]]] -> [1]
[[1,2], [3,4,[5,6]],7] -> [1,2,3,4,5,6,7]
```

Hmmm, flattening is a much-talked about feature disccused/proposed in core Python, as [Raymond Hettinger puts it](https://mail.python.org/pipermail/python-dev/2006-September/068957.html):

> It has been discussed ad nauseam on comp.lang.python. People seem to enjoy writing their own versions of flatten more than finding legitimate use cases that don't already have trivial solutions.

> A general purpose flattener needs some way to be told what is atomic and what can be further subdivided. Also, it is not obvious how the algorithm should be extended to cover inputs with tree-like data structures with data at nodes as well as the leaves (preorder, postorder, inorder traversal, etc.)

**Answer**:

In that case, there're isn't an easy answer to this but there's always our good friend [Rosetta Code](https://rosettacode.org/wiki/Flatten_a_list), so I'm going with:


```python
>>> lst = [[1,2], [3,4,[5,6]],7]
>>> def flatten(lst):
...     return sum((flatten(x) if type(x) == list else [x] for x in lst), [])
... 
>>> flatten(lst)
[1, 2, 3, 4, 5, 6, 7]
```


