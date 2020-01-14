---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.1'
      jupytext_version: 1.2.4
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

# Name(s)
Xavier Graham


**Instructions:** This is an individual assignment, but you may discuss your code with your neighbors.


# Python and NumPy

While other IDEs exist for Python development and for data science related activities, one of the most popular environments is Jupyter Notebooks.

This lab is not intended to teach you everything you will use in this course. Instead, it is designed to give you exposure to some critical components from NumPy that we will rely upon routinely.

## Exercise 0
Please read and reference the following as your progress through this course. 

* [What is the Jupyter Notebook?](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/What%20is%20the%20Jupyter%20Notebook.ipynb#)
* [Notebook Tutorial](https://www.datacamp.com/community/tutorials/tutorial-jupyter-notebook)
* [Notebook Basics](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/Notebook%20Basics.ipynb)

**In the space provided below, what are three things that still remain unclear or need further explanation?**

I don't have many questions, but I always have trouble with the setup of these workspaces, and was wondering if it was better to setup a remote way to access my jupyter notebook from my computer, or to rather just use the hub online and then download it in order to git commit it as my solution?


## Exercises 1-7
For the following exercises please read the Python appendix in the Marsland textbook and answer problems A.1-A.7 in the space provided below.


## Exercise 1

```python
import numpy as np

a = np.full((6, 4), 2)
print(a)
```

## Exercise 2

```python
import numpy as np

b = np.full((6, 4), 1)
np.fill_diagonal(b, 3)
print(b)
```

## Exercise 3

```python
import numpy as np

# You cannot multiply the two matrices together because they are both 6 x 4
# In order to multiply matrices, the number of columns in the first matrix must
# equal the number of rows in the second matrix

# a * b does not multiply the matrices, simply the individual components in a
# 1-to-1 fashion

print(a * b)

# dot(a, b) attempts to multiply the matrices, which is why it doesnt work

# print(np.dot(a, b))
```

## Exercise 4

```python
import numpy as np

print(np.dot(a.transpose(), b))
print(np.dot(a, b.transpose()))

# The above outputs are different shapes because in the first one, we are
# matrix multiplying a 4 x 6 matrix by a 6 x 4 matrix, resulting in a 4 x 4 matrix

# The second one is multiplying a 6 x 4 matrix by a 4 x 6 matrix, resulting in
# a 6 x 6 matrix
```

## Exercise 5

```python
import numpy as np

def definitely_not_lyrics():
    print("Is this the real life? Is this just fantasy?")
    print("Caught in a landslide, no escape from reality")
    print("Open your eyes, look up to the skies and see")
    print("I'm just a poor boy, I need no sympathy")
    print("Because I'm easy come, easy go, little high, little low")
    print("Any way the wind blows doesn't really matter to me, to me")

definitely_not_lyrics()
```

## Exercise 6

```python
import numpy as np
import random
import array as arr

def print_array(arr_in):
    print("[", end = "")
    for i in range(len(arr_in) - 1):
        print(arr_in[i], end = ", ")
    print(arr_in[i + 1], "]", sep = "")

def create_rand_array():
    random_stuff = arr.array('i', [])
    # Generate array
    for i in range(10):
        random_stuff.append(random.randint(0, 100))
    # Print array
    print("ARRAY: ", end = "")
    print_array(random_stuff)
    # Print sum
    print("SUM:", np.sum(random_stuff, dtype = np.uint8))
    # Print mean value
    print("MEAN:", np.mean(random_stuff))
        
create_rand_array()
print()
create_rand_array()
print()
create_rand_array()
print()
```

## Exercise 7

```python
import numpy as np
import array

def count_ones_nowhere(arr_in):
    sum = 0
    for row in arr_in:
        for num in row:
            if num == 1:
                sum += 1;
    return sum

def count_ones_where(arr_in):
    return np.sum(np.where(arr_in == 1, 1, 0))


c = np.array([[3, 2, 1, -9, 1, 0],
              [1, -2, 1, 8, -2, 10],
              [5, 2, 3, 4, 5, 15],
              [1, -1, 0, -9, 1, 1],
              [0, 1, 7, 7, 1, 1],
              [3, 1, -1, 8, 0, 12]])

print(count_ones_where(c))
print(count_ones_nowhere(c))
```

## Excercises 8-???
While the Marsland book avoids using another popular package called Pandas, we will use it at times throughout this course. Please read and study [10 minutes to Pandas](https://pandas.pydata.org/pandas-docs/stable/getting_started/10min.html) before proceeding to any of the exercises below.


## Exercise 8
Repeat exercise A.1 from Marsland, but create a Pandas DataFrame instead of a NumPy array.

```python
import pandas as pd

col_names = ['1', '2', '3', '4']
row_names = ['1', '2', '3', '4', '5', '6']
a = pd.DataFrame(dtype = int, columns = col_names, index = row_names)

for i in row_names:
    a.loc[i] = pd.Series({'1': 2, '2': 2, '3': 2, '4': 2})

print(a)
```

## Exercise 9
Repeat exercise A.2 using a DataFrame instead.

```python
import pandas as pd

b = pd.DataFrame(np.ones((6, 4)))
b.iloc[range(4), range(4)] = 3
    
b
```

## Exercise 10
Repeat exercise A.3 using DataFrames instead.

```python
import pandas as pd

# Same as above, you cannot multiply the two matrices together because they are both 6 x 4
# so the row and column counts do not match up

# a * b multiplies the individual components in a 1-to-1 fashion

print(a * b)

# dot(a, b) attempts to multiply the matrices, which is why it doesnt work
# print(np.dot(a, b))
```

## Exercise 11
Repeat exercise A.7 using a dataframe.

```python
import pandas as pd

def count_ones_nowhere(frame_in):
    sum = 0.0
    for label, content in frame_in.items():
        for index, value in content.items():
            if value == 1:
                sum += 1;
    return sum

def count_ones_where(frame_in):
    return frame_in.where(frame_in == 1.0, other = 0).sum(numeric_only = True).sum()
    
print(count_ones_nowhere(b))
print(count_ones_where(b))

```

## Exercises 12-14
Now let's look at a real dataset, and talk about ``.loc``. For this exercise, we will use the popular Titanic dataset from Kaggle. Here is some sample code to read it into a dataframe.

```python
titanic_df = pd.read_csv(
    "https://raw.githubusercontent.com/dlsun/data-science-book/master/data/titanic.csv"
)

titanic_df
```

Notice how we have nice headers and mixed datatypes? That is one of the reasons we might use Pandas. Please refresh your memory by looking at the 10 minutes to Pandas again, but then answer the following.

## Exercise 12
How do you select the ``name`` column without using .iloc?

```python
import pandas as pd

out_df = titanic_df.get("name")
print(out_df)
```

## Exercise 13
After setting the index to ``sex``, how do you select all passengers that are ``female``? And how many female passengers are there?

```python
titanic_df.set_index('sex',inplace = True)
# Get female passengers only using the line below
female_df = titanic_df.loc["female"]
print(female_df)
# Number of female passengers
print("NUMBER OF FEMALES:", len(female_df.index))
```

## Exercise 14
How do you reset the index?

```python
# Reset index
titanic_df.reset_index()
```

```python

```
