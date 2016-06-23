This is a fun quiz from the guys at [Acronis](http://www.acronis.com/) at their PyCon Dublin booth:

Question 1
====

What will be the output of the code below:

```python
list = ['a', 'b', 'c', 'd', 'e']
print list[10:]
```

Answer
====



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
