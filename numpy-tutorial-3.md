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
