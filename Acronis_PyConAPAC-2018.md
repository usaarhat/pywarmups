This is a fun quiz from the guys at [Acronis](https://www.acronis.com/en-sg/) at their PyCon APAC 2018 booth.

Question 1
====

What is the result of this code?

```
a = [1,2,3,4,5]
print(a[3:1:-1])
```

- Syntax Error
- Value Error
- [3,2]
- **[4,3]**

The extended slice notation allows a **third argument (aka 'step'/'stride')** in Python's slice syntax. <br>

The [official docs for slices](https://docs.python.org/3/library/functions.html#slice) is minimalistic and I would suggest 
http://python-reference.readthedocs.io/en/latest/docs/brackets/slicing.html as a better reference to the slice syntax. 

**TL;DR:** The -1 stride usually reverse the order of the list if the start and end of the slice is in descending order.

```
>>> a = list(range(20))
>>> a
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
>>> a[8:15]  # The 8th to 15th items in the list 
[8, 9, 10, 11, 12, 13, 14]
>>> a[8:15:1]  # The 8th to 15th items in the list moving 1 "step" at a time
[8, 9, 10, 11, 12, 13, 14]
>>> a[8:15:2]  # The 8th to 15th items in the list moving 2 "steps" at a time
[8, 10, 12, 14]
>>> a[8:15:-1]  # The 8th to 15th items in the list moving -1 "steps" at a time?!
[]
>>> a[15:8]  # The 15th to 8th items in the list?!
[]
>>> a[15:8:1]  # The 15th to 8th items in the list moving 1 "step" at a time?!
[]
>>> a[15:8:-1]  # The 15th to 8th items in the list moving -1 "step" at a time?!
[15, 14, 13, 12, 11, 10, 9]
>>> a[15:8:-2]  # The 15th to 8th items in the list moving -2 "step" at a time?!
[15, 13, 11, 9]
```

Question 2
====

How to assign a tuple of length 1 to a?

 - a=1
 - a=(1)
 - a=tuple(1)

Hmmm, typo? 

```
a = tuple(1) # is surely a SyntaxError because it's trying to cast an integer to a tuple.
a = (1)      # returns an integer not a tuple since the parenthesis would be parsed as mathematical bracket.
a = 1        # is essentially the same as `a=(1)`, returns an integer.
```

Perhaps these:

```
a = ()   # returns a tuple of length 0
a = (1,) # returns a tuple of length 1 with 1 assigned to the 1st element.
```

Question 3
====

What is the type of `b` (Python 3) [in the code below]?

```
a = -1
b = a ** 0.5
```

- **float**
- complex 
- int
- str

That's surely a `float`. In Python 3, operations with `float` and `int` would "upcast" the output to `float`

The interesting part of the question is the `complex` options, we'll seldom see it in use unless we're working with mathematical functions beyond real numbers: https://docs.python.org/3/library/functions.html#complex 

Question 4
====

What will be the value of `a` [in the following code]?

```
a = -4 // 1.5
```

- 2.0
- 3.0
- -2.0
- **-3.0**

The `//` syntax is floor division. It does the standard division and the take the "floor" of it.

Here's a nice post that describe basic Python operator https://www.tutorialspoint.com/python/python_basic_operators.htm; stealing their examples:

```
>>> 9 // 2
4
>>> 9.0 // 2.0
4.0
>>> -11 // 3
-4
>>> -11.0 // 3
-4.0
```

Question 5
====

Is this syntax valid?

```
a = { i for i in range(0,10,2) }
```

- **Yes**
- No

This is interesting. 

The `{...}` syntax should return a `dict` or `set` but the lack of `:` that maps key-value, the `{}` here should return a `set`.

The `set` is able to any sequence types (generator included) to initialize a variable. 

Looking at the inner list comprehension `i for i in range(0,10,2)`, it makes little use to iterate through the range and do nothing but it's valid. 

To summarize, yes it's looks valid and to validate:

```
# Though this is valid,
>>> a = { i for i in range(0,10,2) }
>>> a
{0, 2, 4, 6, 8}

# you should do this instead
>>> a = set(range(0,10,2))
>>> a
{0, 2, 4, 6, 8}
```

Question 6
====

What is the value of `a`?

```
a = {1,2,3} < {2,3,4,5}
```

- True
- False

This is a really fun question! The less-than operator says that the type would return as a boolean. 

The fun part is understanding how sets are comparable. 
