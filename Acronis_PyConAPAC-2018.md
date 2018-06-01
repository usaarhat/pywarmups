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
