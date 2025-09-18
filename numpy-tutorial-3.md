<h2>Arithmetic Operations and Functions</h2>
Through NumPy, various Arithmetic Operations can be performed and mathematical functions can be applied which simplifies the workflow.<br>

<h3>Vectorization</h3>
Vectorization can be executed in parallel on multiple elements of the array.<br>
The <b>benefits</b> of vectorization are: <br>
<p></p>

 - Higher performance code
 - Less verbose code
 - Better maintainability

<h3>Basic Arithmetic Operations</h3>
Basic Arithmetic Operations like Addition, Subtraction, Multiplication and Division can be performed on the numpy arrays.

```
import numpy as np
a = np.arange(1,11)
b = np.arange(21,31)
print(a+b)        # Addition
print(b-a)        # Subtraction
print(a*b)        # Multiplication
print(b/a)        # Division

# Output:
# array([22,24,26,28,30,32,34,36,38,40])
# array([20,20,20,20,20,20,20,20,20,20])
# array([21,44,69,96,125,156,189,224,261,300])
# array([21.,11.,7.6667,6.,5.,4.3333,3.5,3.])
```

```
# Exponetiation
c = np.arange(2,12)
print(a**c)

# Output:
# array([1,8,81,1024,15625,279936,5764801,134217728,3486784401,100000000001])
```
This is the basic arithmetic operations that are done on NumPy Arrays. But to perform these operations, certain functions of these arithmetic operations are also provided with the NumPy Library.

```
import numpy as np
a = np.arange(1,11)
b = np.arange(21,31)

print(np.add(a,b))
print(np.subtract(a,b))
print(np.multiply(a,b))
print(np.divide(a,b))

# Output
# array([22,24,26,28,30,32,34,36,38,40])
# array([20,20,20,20,20,20,20,20,20,20])
# array([21,44,69,96,125,156,189,224,261,300])
# array([21.,11.,7.6667,6.,5.,4.3333,3.5,3.])
```

There are some other numpy functions as well

```
np.mod(b,a)    # Modulus
np.power(a,c)  # Power
np.sqrt(a)     # Square root

# Output
# array([0,0,2,0,0,2,6,4,2,0])
# array([1,8,81,1024,15625,279936,5764801,134217728,3486784401,100000000001])
# array([1.,1.414,1.732,2.,2.236,2.449,2.645,2.828,3.,3.162])
```

<h3>Broadcasting</h3>
The term broadcasting describes how NumPy treats arrays with different shapes during arithmetic operations.<br>
Subject to certain constraints, the smaller array is broadcast across the larger array so that they have compatible shapes.<br>
<p></p>
So how does broadcasting works and when can we apply it?<br>
There is a simple rule for it.<br>

- Dimensions are compatible
  If their axes on a one-by-one basis, they have either the same length or a length of one.

  ```
  import numpy as np
  a = np.arange(1,10).reshape(3,3)
  b = np.arange(1,4)
  print(a+b)

  # Output: array([[2,4,6],[5,7,9],[8,10,12]])
  ```

<h3>Aggregate Function</h3>
Aggregate Functions are a set of functions provided by NumPy for calculating aggregates for NumPy Arrays. It takes an array as an input and returns a scaler as output.<br>
Here are sum functions:

- Add

 ```
 import numpy as np
 first_arr = np.arange(10,110,10)
 second_arr = np.arange(10,100,10).reshape(3,3)
 
 print(first_arr.sum())
 print(second_arr.sum(axis=0))
 print(second_arr.sum(axis=1))

 # Output: 550
 # Output: array([120,150,180])
 # Output: array([60,150,240])
 ```

- Product

  ```
  import numpy as np
  third_arr = np.arange(10,110,10).reshape(2,5)
  print(third_app.prod(axis=0))

  Output: array([600,1400,2400,3600,5000])
  ```

- Average & Mean

  ```
  print(np.average(first_arr))
  print(np.mean(first_app))
  
  # Output: 55.0
  # Output: 55.0 
  ```

- Max & Min
  
  ```
  print(np.max(first_app))
  print(np.min(second_app))

  # Output: 100
  # Output: 10
  ```

- Standard Deviation

  ```
  print(np.std(first_app))

  # Output: 28.72281322
  ```

<h3>How to get unique values and counts</h3>
How to get unique values and counts?<br>
NumPy provides some functions to unique elements in array.

```
import numpy as np
first_arr = np.array([1,2,3,4,5,6,1,2,7,2,1,10,7,8])
np.unique(first_arr)

# Output: array([1,2,3,4,5,6,7,8,10])

second_arr = np.array([[1,1,2,1],[3,1,2,1],[1,1,2,1],[7,1,1,1]])
print(np.unique(second_arr))

# Output: array([1,2,3,7])
```

<h3>Transpose like operations</h3>
There are various transpose like functions like transpose, moveaxis and swapaxes.<br>
<p></p>
<i>The difference between <b>Reshape</b> and <b>Transpose</b> is that reshape takes an array and forwards the array into a desired shape. Whereas, transpose changes rows and columns and columns into rows.</i><br>
Transpose takes in two parameters, one is the array and other is the axes which optional. As a result, it returns the input array with an inverted axes.<br>
<p></p>

```
first_2dim = np.arange(12).reshape((3,4))
print(first_2dim)
# Output: array([[0,1,2,3],[4,5,6,7],[8,9,10,11]])

print(np.transpose(first_2dim))
# Output: array([[0,4,8],[1,5,9],[2,6,10],[3,7,11]])
```

<h3>Reversing an array</h3>
Reversing an array can be done conventionally without using any functions using slicing.
In slicing the parameters are [start:stop:step]. If the step is set to -1, the elements are printed in a reverse order.<br>

```
arr_idim = [10,1,9,2,8,3,7,4,6,5]
print(arr_idim[::-1])

# Output: [5,6,4,7,3,8,2,9,1,10]
```

In NumPy, flip function is used to reverse an array. Flip function takes a single parameter which is the array that is required to be reversed.<br>

```
import numpy as np
print(np.flip(arr_idim))

# Output: array([5,6,4,7,3,8,2,9,1,10])
```


<h2>Where() function</h2>
Where Function in numpy performs a logical test and returns a given value if the test is True, or another if the test is False.<br>

```
import numpy as np
inv_arr = np.array([12, 102, 18, 0, 0])
print(np.where(inv_arr <= 0, "Out of stock", "In Stock"))

# Output: np.array(['In Stock', 'In Stock', 'In Stock', 'Out of stock', 'Out of stock'])
```

This where() function can also be used in a nesting format. For example:

```
import numpy as np
my_arr = np.array([1,2,3,4,5])

print(np.where(my_arr % 2 == 0, 'even', np.where(my_arr == 3, my_arr, 'odd)))

# Output: np.array(['odd','even',3,'even','odd'])
```
