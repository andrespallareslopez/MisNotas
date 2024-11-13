# Apuntes Python Machine Learning

---
## Run SQL directly in Jupyter Notebook with IPython-SQL


https://levelup.gitconnected.com/run-sql-directly-in-jupyter-notebook-with-ipython-sql-4b39c2105930



---
## Learn Jupyter Notebooks for SQL Server

https://www.sqlshack.com/learn-jupyter-notebooks-for-sql-server/


---

Python Tutorial - For Loop with List Comprehensions

https://platzi.com/tutoriales/4227-python-fundamentos/31662-python-tutorial-for-loop-with-list-comprehensions/


~~~
# Define a list of numbers 
numbers = [1, 2, 3, 4, 5]

# Create a new list of squares using a list comprehension
squares = [number ** 2 for number in numbers]

# Print the new list
print(squares)
~~~

~~~
# Create a new list of squares for even numbers only
even_squares = [number ** 2 for number in numbers if number % 2 == 0]

# Print the new list
print(even_squares)
~~~




---

## Context Managers and Python's with Statement

https://aulas.campusmvp.com/SELF/lesson.self?LessonId=113745

~~~
file = open("hello.txt", "w")

try:
    file.write("Hello, World!")
except Exception as e:
    print(f"An error occurred while writing to the file: {e}")
finally:
    # Make sure to close the file after using it
    file.close()
~~~


~~~
with expression as target_var:
    do_something(target_var)

~~~





---
## leer datos desde el portapapeles


~~~



~~~


~~~
import pandas as pd
calidad_aire = pd.read_clipboard()
calidad_aire.describe()
~~~





---

## Missing Values With Pandas

https://medium.com/swlh/data-science-for-beginners-how-to-handle-missing-values-with-pandas-73db5fcd46ec


~~~
import pandas as pd
pd.read_excel('Students_Scores.xlsx')

missing_value_forms=['?','Nil']
df= pd.read_excel('Students_Scores.xlsx',na_values= missing_value_forms, index_col= 'Student ID')
df

df.isnull()

~~~


---
