# Lecture 1:  Introduction to Jupyter Notebook

- Got Introduced to IDEs and Jupyter Notebooks
- Advantages of Notebooks.

## Summary

- Jupyter notebook is a convenient interface to develop python code.
- Incrementally update and run.
- Embed documentation using Markdown.
- Preserves output when exporting.
- Useful for collaboration sharing.
- Google Colab - Free to use version configured for ML


# Lecture 2

- Sir showed practically using screen cast about how Jupyter looks and works.

# Lecture 3: Python recap - I

### Computing GCD
- gcd (m,n) <= min (m,n)
- Compute list of common factors from 1 o min (m,n)
- Return the last common factor

```python
def gcd(m,n);
	cf = [] # List to store common factors
	for i in range(1, min(m,n) + 1):
		if (m % i) == 0 and (n % i) == 0:
			cf.append(i)
	return(cf[-1])
```

*We can also do the same using a different approach with minimal changes*

```python
def gcd(m,n):
	for i in range(1, min(m,n) + 1):
		if (m % i) == 0 and (n % i) == 0:
			mrcf = i
	return mrcf
```


# Lecture 4: Python recap - II

### Prime Numbers

- A prime number *n* has exactly 2 factors, *1* and *n* 
- Compute the list of factors
- *n* is a prime if the list of factors contains precisely *[1,n]*

> First let's create a function to find the factors

```python
def factors(n):
	f1 = []
	for i in range(1, n + 1):
		if (n % i) == 0:
			f1.append(i)
	return f1
```
```python
def prime(n):
	return factors(n) == [1,n]
```

#### List of all primes up-to *m*

```python
def primesupto(m):
	pl = []    # prime list to store all prime values
	for i in range(1, m+1):
		if prime(i):
			pl.append(i)
	return pl
```

#### List of first *m* primes

```python
def firstprimes(m):
	(count, i, pl) = (0, 1, [])
	while (count < m):
		if prime(i):
			(count, pl) = (count + 1, pl + [i])
		i+=1
	return pl
```

#### Another way to calculate primes

- Directly check if n has a factor between *2* and *n-1*

```python
def prime(n):
	result = True    # we will consider n as a prime
	for i in range(2, n-1):
			if (n % i) == 0:
				result = False
				break
	return result
```

> Using While loop

```python
def prime(n):
	(result, i) = (True, 2)
	while (result and i < n):
		if (n % i) == 0:
			result = False
		i += 1
	return result
```

> Speeding up the process using Square root

```python
import math
def prime(n):
	(result, i) = (True, 2)
	while (result and i < math.sqrt(n)):
		if (n % i) == 0:
			result = False
		i += 1
	return result
```

#### Finding frequency of prime difference

```python
def primediffs(n):
	lastprime = 2
	pd = {}    # dictionary to store frequency 
               # where key is the difference and value is the frequency	
    for i in range(3, n+1):    # start checking from 3 since 3 is the smallest
                               # after 2
	    if prime(i):
		    d = i - lastprime
		    lastprime = i

			if i in pd.keys():
				pd[d] = pd[d] + 1
			else:
				pd[d] = 1
	return pd
```


# Lecture 5: Exception handling

- **Exception contains two parts:**
	1. Type of Error
	2. Error Message

> Syntax for using Exception handling

```python
try:
...
...
...

except NameError:    # Handles specific error
...
...
...

except:    # Handles all types of error
...
...
...

else:    # Get's executed when there is not error
...
...
...
```

# Lecture 6: Python recap - III

- Used Euclid's algorithm to solve GCD problem
- Refer to [this](https://www.youtube.com/watch?v=JUzYl1TYMcU) for a clear explanation of the algorithm since the lecture is bit confusing.

# Lecture 7: Classes and Objects

#### Abstract Datatypes
- Separate the (private) implementation from (public) specification.

#### Class
- Template for a data type.

#### Object
Concreate example of a template.

#### Special Functions
- `__init__()` - Constructor
- `__str__()` - Convert object to string
- `__add__()` - Implicitly invoked by +
- `__multi__()` - Invoked by *
- `__lt__()` - Invoked by <
- `__ge__()` - Invoked by >=


# Lecture 8: Implementation of Python Codes II

Jupyter notebook tutorial on classes and objects

# Lecture 9: Timing our Code

- Python has a library called `time` with various useful functions.
- `perf_time()` returns a random time whose exact value may not be relevant to us but we can use it to find the difference in time and get the interval between two consecutive `perf_time()` readings.
- Default unit is seconds.

```python
import time

start = time.perf_time()
...
# Execute the code
...
end = time.perf_time()

elapsed = end - start
```

#### A timer object

- Create a timer class
- Two internal values
	- `_start_time`
	- `_elapsed_time`
- `start` starts the timer
- `stop` records the elapsed time.

```python
import time

class Timer:

	def __init__(self):
		self._start_time = 0
		self._elapsed_time = 0
	
	def start(self):
		self._start_time = time.perf_counter()

	def stop(self):
		self._elapsed_time = time.perf_counter() - self._start_time
	
	def elapsed(self):
		return(self._elapsed_time)
```

> Python execute 10^7 operations per second

# Lecture 10: Why efficiency matters?

Efficiency matters because in real world scenario some operations can take years which is practically not feasible. But by making best use of data structures and algorithms we can reduce that time drastically which will make it easier for us.