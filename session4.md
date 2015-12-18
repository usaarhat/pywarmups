Do. Or do not. There is no try
====

*Timely, it is, with a Star Wars joke, I start*. Off with the Jedi jokes... 

This warm-up session would cover some basics of error handling in Python. 

Fire up our https://try.jupyter.org/ notebook and let's go...


Exploding Errors 
====

Sometimes there are just those things that breaks our Python code and it explodes and throws an Error!! Here's some examples:

```python
x = 'foobar'
print (len(x)) # We know that there are only 6 characters.
print (x[0]) # We can access the individual characters as such.
print (x[8])
```

But when we try to retrieve a character index that's out of range, i.e. `x[8]`, Python explodes and throws an `IndexError`:

```python
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range
```

Here's one more example:

```python
filename = 'imaginaryfile.txt' # An imagainary file that doesn't exist
open(filename, 'r')
```

When we try to open a file with a filename that doesn't exist on our computer, Python explodes once again and throws an `IOError`:

```python 
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IOError: [Errno 2] No such file or directory: 'imaginaryfile.txt'
```

Another common error is when you have a function that takes in integers and it tries to do some division:

```python
def divide(numerator, denominator):
    return numerator / denominator
    
divide(10, 0)
```

And Python throws:

```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: integer division or modulo by zero
```

(**Note**: I'm using *"throw an error"* due to historical reasons. In C/C++ or Java, when the compiler gives an error, they call it *"throwing"* an error. And usually *throw* is a built-in keyword in othe programming languages.)


Forgiveness and Leaping
===

So Python likes to throw tantrums, we can try to handle our 0 division problem with some smart `if-else`, e.g.:

```python
def divide(numerator, denominator):
    if denominator == 0:
        return 0
    else:
        return numerator / denominator
        
divide(10, 0)
```

But this is not always the case that we want the results to be 0 whenever we divide, it's better to know explicitly wait for Python to throw the Error before returning the 0. So we introduce the `try-except` clause and specifically when Python throws a `ZeroDivision` Error.


```python
def divide(numerator, denominator):
    try:
        return numerator / denominator
    except ZeroDivisionError: 
        return 0
        
divide(10, 0)
```

This `try-except` coding style is call [EAFP (Easier to Ask for Forgiveness than Permission)](https://docs.python.org/2/glossary.html#term-eafp)

> Easier to ask for forgiveness than permission. This common Python coding style assumes the existence of valid keys or attributes and catches exceptions if the assumption proves false. This clean and fast style is characterized by the presence of many try and except statements. The technique contrasts with the LBYL style common to many other languages such as C.

The `if-else` coding style is call [LBYL (Look Before You Leap)](https://docs.python.org/2/glossary.html#term-lbyl)

> Look before you leap. This coding style explicitly tests for pre-conditions before making calls or lookups. This style contrasts with the EAFP approach and is characterized by the presence of many if statements.
> In a multi-threaded environment, the LBYL approach can risk introducing a race condition between “the looking” and “the leaping”. For example, the code, if key in mapping: return mapping[key] can fail if another thread removes key from mapping after the test, but before the lookup. This issue can be solved with locks or by using the EAFP approach.

Below is a "lazy" way to write `try-except` that is discouraged. It's because by not explicitly stating the exception, we allow anything to skip to the lines within after the `except`. So the code below returns 0 too!

```python
def divide(numerator, denominator):
    try:
        return numerator / denominator
    except: 
        return 0
        
divide(10, 'foobar')
```

Finally
====

From the `divide()` example with `try-except`, still we don't know when it's divided by 0. Recall that when Python throws a ZeroDivisionError, it gives:

```python
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: integer division or modulo by zero
```

Note that there is a message *`integer division or modulo by zero`*, we can catch this *message*, tells the user that a zero division occurs while still returning a 0 result:

```python
def divide(x,y):
	try:
		return x / y
	except ZeroDivisionError, e: # We catch error
		print (e)
		return 0

divide(10, 0)
```

And the code above should output:

```
integer division or modulo by zero
0
```

Finally, we have reached the `finally` section of this warmup. The `finally` keyword in python is often called the [*"clean-up"*](https://docs.python.org/3.5/tutorial/errors.html#defining-clean-up-actions) code in the `try-except` section of the code. 

Although, this is not well motivated, one use case is for the `try-except` to figure out the computation and then only return the result of our division at the finally clause.


```python
def divide(x,y):
	try:
		result = x / y
	except ZeroDivisionError, e: # We catch 
		print e
		result = 0
	finally:
		return result
		
divide(10,0)
```

Here's another example where `finally` is a little more useful:

```python
def divide_plus_one(x,y):
	try:
		result = x / y
	except ZeroDivisionError, e: # We catch 
		print e
		result = 0
	finally:
		return result + 1
		
divide_plus_one(10,0)
```

In most cases, there are other ways to handle (i) file I/O (but now with the `with` context manager, this is normally not needed), (ii) threading (e.g. lock releases in multi-threading and multi-core), (iii) database cursor manipulation (e.g. to close a cursor or to commit the queries). For these use cases, it's out of scope for what we do, but someday we'll need it. 

Congratulations!!!
====

You have learn some introduction to error handling in Python with `try-except`. There'll be more to come in future sessions as we look at handling other Errors. 

**And here's more Star Wars**: https://www.youtube.com/watch?v=BQ4yd2W50No


