<h1>Numpy</h1>
Numpy is a python library used for <p>

1. Arithmetic Operations
2. Statistics Operations
3. Bitwise Operations
4. Linear Algebra
5. Searching, Sorting and counting</br>

and an advantage of Numpy array over python lists is that it consumes comparatively less memory and also are faster in processing.

Here's an example code of creating a numpy array:<p>

```
import numpy as np
array = np.array([1,2,3])
```
*Note: Unlike a Python list, np array holds elements of same data type*
<p></p>

And array in numpy is a dtype int64 type by default if provided by basic integers
```
import numpy as np
integers = np.array([10,20,30])
print(integers.dtype)

# Output: dtype('int64')
```
This means that if we replace an element `integers[0]` with let's say a float `21.5`, it new value will be the closest integer to that float value, i.e., `21`.

```
integers[0] = 21.5
print(integers)

# Output: array([21,20,30])
```

To change the datatype from let's say `int64` to `int8`, we can do
```
integers2 = np.array(integers, dtype=np.int8)
print(integers2)

# Output: array([21,20,30], dtype=int8)
```

<h3>Multi-Dimensional Array</h3>
Multi-dimensional arrays are the numpy arrays that are contains elements in the multiple dimensions.

```
import numpy as np
nums = np.array([[1,2,3,4,5],[6,7,8,9,10]])
print(nums)

# Output: array(([1,2,3,4,5],[6,7,8,9,10]))
```
This is a 2 dimensional array with 5 elements in each dimensions.<br>
To access the elements in this, we can use two `[]`<br>
For example,

```
print(nums[0][0])

# Output: 1
```
<h3>Creating numpy array from python lists.</h3>
This can be done by:

```
import numpy as np
first_list = [1,2,3,4,5]
first_array = np.array(first_list)
print(first_array)

# Output: array([1,2,3,4,5])
```
For a python list with multiple datatypes for let's say `int64` and `float64`, the resulting numpy array will be of `float64`.<br>
For `float + str` or `int + str`, resulting array will be `str`

Tuples can also be converted to numpy arrays.
```
import numpy as np
first_tuple = (1,2,3,4,5)
tuple_array = np.array(first_tuple)
print(tuple_array)

# Output: array([1,2,3,4,5])
```

<h3>Intrinsic Numpy array creation</h3>
"intrinsic array creation" refers to the functions and methods provided by the NumPy library that allow for the direct and efficient creation of NumPy arrays (specifically, ndarray objects) without necessarily converting from existing Python data structures like lists or tuples.<br>
<p></p>

- np.arange()<br>
  np.arange is used to create an array of `int` within a given particular range.

```
import numpy as np
integers_array = np.arange(10)
print(integers_array)

# Output: array([0,1,2,3,4,5,6,7,8,9])

int_sec_arr = np.arange(100,110)
print(int_sec_arr)

# Output: array([100, 101, 102, 103, 104, 105, 106, 107, 108, 109])

# Skip 2 elements
int_two_skip = np.arange(100,111,2)
print(int_two_skip)

# Output: array([100, 102, 104, 106, 108, 110])
```
- np.linspace()<br>
  np.linspace is used to create a `float` array of 50 samples of equidistant values within a range.

```
import numpy as np
linspace_array = np.linspace(10,20)
```

For a specific number of elements, add a third argument that contains number of elements

```
import numpy as np
linspace_arr2 = np.linspace(10,20,5)
print(linspace_arr2)

# Output: array([10. , 12.5 , 15. , 17.5 , 20. ])
```

- np.random.rand()<br>
  np.random.rand is used to generate random `float` elements. The number of elements will be equal to the number that is given in the argument.

```
import numpy as np
first_random_arr = np.random.rand(5)
print(first_random_arr)

# Output: array([0.7126, 0.3925, 0.4672, 0.5859, 0.7692])
```
For the same, if `int` is to be made, `np.random.randint()` is used.

```
int_random = np.random.randint(0,20,3)
print(int_random)

# Output: array([3,7,15])
```

<h3>Creating arrays filled with constant values</h3>
Functions used to create arrays with some fixed constant values.<br>
<p></p>

- np.zeros()<br>
Creates an array that with zeros with number of elements same as the number given in the argument.

```
import numpy as np
zero_arr = np.zeros(5)
print(zero_arr)

# Output: array([0.,0.,0.,0.,0.])

two_d_zero = np.zeros(2,2)
print(two_d_zero)

# Output: array([[0.,0.]
                [0.,0.]])
```

- np.ones()<br>
Created an array with ones.

```
import numpy as np
one_arr = np.ones(5)
print(one_arr)

# Output: array([1.,1.,1.,1.,1.])

one_arr = np.ones(5, dtype=int)
print(one_arr)

# Output: array([1,1,1,1,1])
```

-np.full()<br>
  np.full((a,b), n) creates an a*b dimensional array of n. <br>
  For example,

```
import numpy as np
full_arr = np.full((2,2),5)
print(full_arr)

# Output: array([[5,5],
                [5,5]])
```

<h3>Finding the shape and size of the array</h3>
<b>Size</b> of an ndarray is equal to the number of elements that are there in the array.<br>
<b>Shape</b> of an ndarray is a pair of integers which tells the number of rows and number of columns in an array.

```
sec_arr = np.full((2,2,2),10)
print(np.shape(sec_arr))   # (2,2,2)
print(np.size(sec_arr))    # 8
```
