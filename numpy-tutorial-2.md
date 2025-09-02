<h2>Manipulating NumPy Arrays</h2>
Numpy supports Array manipulation in certain ways.<br>
Adding, Removing and sorting elements can be done using Numpy.<br>

<h3>Adding/Inserting an element</h3>

```
import numpy as np
first_arr = np.array([1,2,3,5])
new_first = np.insert(first_arr,3,4)
print(new_first)

# Output: array([1,2,3,4,5])
```
In this, the format of the function is `np.insert(array,index,element)`.<br>
If the element has to be added at the last, instead of `np.insert()`, `np.append()` can also be used.<br>

```
new_arr = np.append(new_first, 6)
print(new_arr)

# Output: array([1,2,3,4,5,6])
```

<h3>Deleting an element</h3>
To remove an element, `np.delete` can be used as `np.delete(array, index)`

```
third_arr = np.delete(new_arr, 4)
print(third_arr)

# Output: array([1,2,3,4,5])
```

<h3>Sorting elements</h3>
Elements in a numpy array can be sorted in order using `np.sort()` function.

```
import numpy as np
int_arr = np.array([2,3,1,5,4])
print(np.sort(int_arr))

# Output: array([1,2,3,4,5])
```
For a 2-D array, sorting happens in each of the subarray.

```
two_dim_arr = np.array([[3,2,5,7,4],[5,0,8,3,1]])
print(np.sort(two_dim_arr))

# Output: array([2,3,4,5,7],[0,1,3,5,8])
```

<h3>Copies and Views</h3>
- <b>Copy</b> is a copy or duplicate of the original array.<br>
- <b>View</b> is a different view of the original array.<br>
<p></p>
In View of an array, if any change is made in the view array, the same will be there in the existing array. ID of the array will also remain the same.<br>

```
import numpy as np
id_num = np.array([111,222,333,444,555])
student_id = id_num

student_id[1] = 777
print(student_id)
print(id_num)

# Output:
array([111,777,333,444,555])
array([111,777,333,444,555])
```

In Copy of the array, any change made in the copy array will not be there in the existing array. ID of the array will also change.

```
import numpy as np
id_num = np.array([111,222,333,444,555])
student2_id = id_num.copy()
print(student2_id)

# Output: array([111,222,333,444,555])

student2_id[1] = 777
print(student2_id)
print(id_num)

# Output:
array([111,777,333,444,555])
array([111,222,333,444,555])
```

<h3>Reshaping the Array</h3>
Reshaping the array means giving the array a new shape without changing its data.<br>

```
import numpy as np
first_arr = np.arange(1,9)
print(first_arr)

# Output: array([1,2,3,4,5,6,7,8])

sec_arr = np.reshape(first_arr, (2,4))
print(sec_arr)

# Output: array([1,2,3,4],[5,6,7,8])
```
To reshape a numpy array, `np.reshape(arr,(row,col))` is used. The parameters specified are 
- the array
- number of rows required
- number of columns required

<i>Note: Rows x Columns should always be equal to the number of the elements in the numpy array, otherwise, it'll show an error.</i><br>

<h3>Indexing and Slicing</h3>

- <b>Indexing</b> means the position of an element in the array. Index of an array always starts from 0, if starting from left and starts with -1, if starting from right to left.<br>
- <b>Slicing</b> means slicing a particular part of an array. It can be done using the index of the first and last element in the sliced array.<br>

```
import numpy as np
first_arr = np.array([1,2,3,4,5])
print(first_arr[0])    # Indexing
print(first_arr[0:3])  # Slicing

# Output
1
array([1,2,3,4])
```

<h3>Joining Arrays</h3>
Two or more Numpy Arrays can be joined in various ways through some predefined Functions. Those Functions are: 

- concatenate
- stack
- hstack
- vstack

`Concatenate Function`
```
import numpy as np
first_arr = np.arange(1,6)
second_arr = np.arange(6,11)
con_arr = np.concatenate(first_arr, second_arr)
print(con_arr)

# Output: array([1,2,3,4,5,6,7,8,9,10])

first_two_arr = np.array([[1,2,3],[4,5,6]])
second_two_arr = np.array([[4,5,6],[7,8,9]])
con_two_arr = np.concatenate((first_two_arr, second_two_arr), axis=1)
print(con_two_arr)

# Output: array([[1,2,3,4,5,6],[4,5,6,7,8,9]])
```

`stack`
```
import numpy as np
arr_one = np.array([1,2,3,4,5])
arr_two = np.array([6,7,8,9,10])
st_arr = np.stack((arr_one, arr_two))
print(st_arr)

# Output: array([[1,2,3,4,5],[6,7,8,9,10]])
```

`hstack` or `horizontal stack`
```
import numpy as np
arr_one = np.array([1,2,3,4,5])
arr_two = np.array([6,7,8,9,10])
hst_arr = np.hstack((arr_one, arr_two))
print(hst_arr)

# Output: array([1,2,3,4,5,6,7,8,9,10])
```

<h3>Splitting Arrays</h3>
A Numpy Arrays can be split in various ways through some predefined Functions. Those Functions are: 

- split
- array_split
- hsplit
- vsplit

`array_split`
```
first_arr = np.arange(1,13)
sp_arr = np.array_split(first_arr,4)
print(sp_arr)

# Output: [array([1,2,3]), array([4,5,6]), array([7,8,9]), array([10,11,12])]
```
