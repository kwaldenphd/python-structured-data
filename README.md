# Working With Structured Data in Python

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

This lab covers various methods for reading structured data into Python, focusing on `csv` and `json`. It covers other types of delimiters and escape characters. 

By the end of this lab, students will be able to:
- Describe the structure and components of a .csv file
- Understand how to approach other types of delimited files
- Understand how to work with escape characters when loading structured data
- Understand how Python dictionaries work as a type of structured data
- Write data from Python to a .csv file
- Read a .csv file into Python using the csv module and a for loop
- Describe JSON data structure/components
- Write data from Python to a JSON file
- Read a JSON file into Python using the JSON module

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=762d6791-024a-46bf-a5a1-add301722b86">Lab overview</a></td>
  </tr>
  </table>
  
<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=4c2b0eb8-f898-40be-ac96-add30171600e">Lecture/live coding playlist</a></td>
  </tr>
  </table>
  
## Acknowledgements

Peer review and editing on the CSV and XLSX portions of this lab was provided by Spring 2021 graduate teaching assistant [Aidan Draper](https://github.com/adraper2).

Peer review and editing on the JSON and XML portions of this lab was provided by Spring 2021 graduate teaching assistant [Subhadyuti Sahoo](https://github.com/SDSAHOO703).

Information and exercises in this lab are adapted from:
- Al Sweigart [*Automate the Boring Stuff With Python*](https://nostarch.com/automatestuff2) (No Starch Press, 2020).
  * Chapter 16 "Working With CSV Files and JSON Data" (371-388)
- Wes McKinney, "Chapter 6.1, Reading and Writing Data in Text Format" in [*Python for Data Analysis*](https://www.oreilly.com/library/view/python-for-data/9781491957653/) (O'Reilly, 2017): 169-184.
- Wes McKinney, Chapter 6 "Data Loading, Storage, and File Formats" from [*Python for Data Analysis*](https://www.oreilly.com/library/view/python-for-data/9781491957653/) (O'Reilly, 2018): 169-193

# Table of Contents

- [Lecture and Live Coding](#lecture-and-live-coding)
- [Lab Notebook Template](#lab-notebook-template)
- [Data](#data)
- [CSV](#csv-data-in-python)
  * [What is a `.csv` file?](#what-is-a-csv-file)
  * [File Methods in Python](#file-methods-in-python)
    * [`open()`](#open)
    * [Access Modes](#access-modes)
    * [`open()` examples](#open-examples)
    * [`write()`](#write)
    * [`open()`, `write()`, and `CSV` files](#open-write-and-csv-files)
    * [The CSV Module](#the-csv-module)
      * [A Quick Detour Into Packages, Modules, and Libraries](#a-quick-detour-into-packages-modules-and-libraries)
      * [Back to the CSV Module](#back-to-the-csv-module)
  * [Reading a `.csv` file into Python](#reading-a-csv-file-into-Python)
    * [Reading `.csv` data using a `for` loop](#reading-csv-data-using-a-for-loop)
  * [Other delimiters](#other-delimiters)
  * [Escape characters](#escape-characters)
  * [Reading in `.csv` files using dictionaries](#reading-in-csv-files-using-dictionaries)
  * [Writing to a `.csv` file](#writing-to-a-csv-file)
  * [Additional CSV Lab Notebook Questions](#additional-csv-lab-notebook-questions)
- [JSON](#json)
  * [What is JSON and why are we learning about it](#what-is-json-and-why-are-we-learning-about-it)
  * [Reading JSON into Python](#reading-json-into-python)
  * [Working with JSON in Python](#working-with-json-in-python)
  * [Writing to JSON from Python](#writing-to-json-from-python)
  * [Additional JSON Lab Notebook Questions](#additional-json-lab-notebook-questions)
- [Lab Notebook Questions](#lab-notebook-questions)

[Link to lab procedure as a Jupyter Notebook](https://drive.google.com/file/d/1OMuQkkJoKkUlNNHl27BmXNe4uWnPHnyu/view?usp=sharing)

# Lecture and Live Coding

Throughout this lab, you will see a Panopto icon at the start of select sections.

This icon indicates there is lecture/live coding asynchronous content that accompanies this section of the lab. 

You can click the link in the figure caption to access these materials (ND users only).

Example:

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=762d6791-024a-46bf-a5a1-add301722b86">Lab overview</a></td>
  </tr>
  </table>
  
<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=4c2b0eb8-f898-40be-ac96-add30171600e">Lecture/live coding playlist</a></td>
  </tr>
  </table>

# Lab Notebook Template

Lab notebook template:
- [`.py` file](https://drive.google.com/file/d/1Dacp329cBMosmJvJcD10qSavgHpP3rYN/view?usp=sharing)
- [Jupyter Notebook](https://colab.research.google.com/drive/1sL-GUG-NtBguee6NaYoazgPQmdKxmWpV?usp=sharing)

# Data

You'll need four data files for this lab.
- `example.csv`
- `example.txt`
- `example.xlsx`
- `exampleWithHeader.csv`

These files are already loaded in the Replit project template for this lab.

You can also access them [via Google Drive](https://drive.google.com/drive/folders/1Sp_N34753ONJRU2AFKcocQ2DhCEhyL-m?usp=sharing) (ND users only).

# `.csv` data in Python

## What is a `.csv` file? 

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=0076f2aa-1167-4e86-8d1f-add3013f6d6d">What is a CSV</a></td>
  </tr>
  </table>

1. CSV stands for "comma-separated values." CSV files are tabular data structures (i.e. a spreadsheet), stored in a plain-text format.

2. Python includes a built-in `csv` module that allows us to read in data from a `.csv` file (or other type of delimited plain-text file), as well as write data to a `.csv` file.

3. In `.csv` files, each line represents a row in the spreadsheet, and commas separate cells in each row (thus the file format name comma-separated values).

4. At first glance, `.csv` files look similar to proprietary spreadsheet program file formats, such as files saved in Microsoft Excel or Apple Numbers. 

5. However, file formats like `.xls` or `.xlsx` (Microsoft Excel) or `.numbers` (Apple Numbers) are NOT plain-text formats. Try to open these file types in a text editor and you'll quickly see the additional content and markup added by the spreadsheet program. More on this later.

6. A few characteristics that distinguish `.csv` files (or other plain-text structured data formats) from proprietary spreadsheet file types:
- Columns in a `.csv` file don't have a value type. Everything is a string.
- Values in a `.csv` file don't have font or color formatting
- `.csv` files only contain single worksheets
- `.csv` files don't store formatting information like cell width/height
- `.csv` files don't recognize merged cells or other kinds of special formatting (frozen or hidden rows/columns, embedded images, etc.)

7. Given these limitations, especially compared to the way we often interact with spreadsheet programs like Microsoft Excel or Google Sheets, what's the advantage of working with `.csv` files?

8. One key advantage of `.csv` files is their simplicity. You can load or open a `.csv` file in a text editor and be able to quickly see the values in the file. 

9. When working with data in a programming environment, `.csv` files as a plain-text format simplify the process of loading structured data.

<blockquote>Q1: Open the <code>example.xlsx</code> file in a text editor. Describe what you see.</blockquote>

<blockquote>Q2: How does your answer to Q1 compare to what you see when you open the <code>example.csv</code> file in a text editor?</blockquote>

<blockquote>Q3: Open the <code>example.xlsx</code> file in a spreadsheet program. Save the file as a <code>.csv</code> format. What happens? Or what happens when you open the newly-created <code>.csv</code> file in a spreadsheet program or text editor?</blockquote>


## File Methods in Python

10. Before we start loading data files in Python, let's talk more about how Python handles creating, reading, and writing files.

11. Specifically, we will be focusing on a few key Python functions for working with files.
- `open()`
- `write()`

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=19e7779b-344a-42d6-84c8-add30142fe8d">File Methods: Open and Write</a></td>
  </tr>
  </table>

### `open()`

12. The `open()` function lets us open an existing file or create a new file in Python.

13. For either version of `open()` (new file or existing file), we need to specify the file name (with the file type extension) and access mode.

14. Core syntax for opening an existing file:

```Python
open(file_name.extension, access_mode)
```

15. The file type extension is the string of characters that follows the period after the file name.

16. Examples include `.py`, `.csv`, `.txt`, etc.

17. The types of file handling functions we are covering in this lab will generally only support reading and writing plain-text (or machine-readable) files.

### Access Modes

18. The access mode parameter specifies the types of modifications that can be made to the file. It can also specify the type of data or information contained in the file.

19. Possible access mode parameters:

<table>
 <tr>
  <th>Parameter</th>
  <th>Name</th>
  <th>Description</th>
 </tr>
 <tr>
  <td><code>"r"</code></td>
  <td>Read</td>
  <td>Opens a file for reading; also the default value</td>
 </tr>
 <tr>
  <td><code>"a"</code></td>
  <td>Append</td>
  <td>Opens the file for appending new or additional information; Creates the file if it does not already exist</td>
 </tr>
 <tr>
  <td><code>"w"</code></td>
  <td>Write</td>
  <td>Opens the file for writing new information; Creates the file if it does not already exist</td>
 </tr>
 <tr>
  <td><code>"x"</code></td>
  <td>Create</td>
  <td>Creates the file if it does not already exist</td>
 </tr>
 </table>

20. Additionally, we can specify the type of data contained in the file, or how Python should handle the information in the file.

<table>
 <tr>
  <th>Parameter</th>
  <th>Name</th>
  <th>Description</th>
 </tr>
 <tr>
  <td><code>"t"</code></td>
  <td>Text</td>
  <td>Treats file as text data; also the default value</td>
 </tr>
 <tr>
  <td><code>"b"</code></td>
  <td>Binary</td>
  <td>Treats the file as binary data</td>
 </tr>
 </table>
 
 #### `open()` examples
 
 ```Python
 # opens an existing text (TXT) file with overwrite permission
 f = open("existing_file.txt", "w")
 ```
 
 ```Python
 # opens an existing CSV file and reads the content
 f = open("existing_file.csv", "r")
 ```
 
 ```Python
 # creates new txt file with write permission
 f = open("new_file.txt", "w")
 ```
 
 ```Python
 # creates new CSV file without write privileges
 f = open("new_file.csv", "x")
```
 
21. If you these examples, you will see a newly-created file appear in your environment or project workspace. 

### `write()`

22. Now that we have a newly-created file in Python, we can use the `write()` function to ***write*** content to that file.

23. Let's say we want to create a `.txt` (plain text) file and write a string to that file.

24. We can do that using `write()`.

25. An example:

```Python
# creates new txt file with write permission
f = open("new_file.txt", "w")

# writes string to new file
f.write("Hello world!")

# closes file
f.close()
```

26. NOTE: It is ***very important*** to `close()` the file once you are done writing content or making modifications.

27. Another example where we have assigned a string to a variable and write the variable to the `.txt` file:

```Python
# creates new txt file with write permission
f = open("new_file.txt", "w")

# assigns string to variable
hello_world = "Hello world!"

# writes string variable to new file
f.write(hello_world)

# closes file
f.close()
```

28. Open the `new_file.txt` file to see the newly-added content.

29. For more on file handling methods in Python:
- [Python File Handling, W3Schools](https://www.w3schools.com/python/python_file_handling.asp)
- [Python File Write, W3Schools](https://www.w3schools.com/python/python_file_write.asp)
- [Python open() Function](https://www.w3schools.com/python/ref_func_open.asp)

### `open()`, `write()`, and `CSV` files

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=83ea18fa-8a66-49ad-a583-add30148f6d4">File Methods: Open, Write, and CSV Files</a></td>
  </tr>
  </table>

30. A couple quick reminders: `CSV` stands for comma-separated values, and `CSV` files are the plain-text, machine-readable file type for tabular data (table data, or data in a spreadsheet structure)

31. For example, a table that looks like this in a spreadsheet program like Excel or Google Sheets:

<table>
 <tr>
  <th>Parameter</th>
  <th>Name</th>
  <th>Description</th>
 </tr>
 <tr>
  <td><code>"t"</code></td>
  <td>Text</td>
  <td>Treats file as text data; also the default value</td>
 </tr>
 <tr>
  <td><code>"b"</code></td>
  <td>Binary</td>
  <td>Treats the file as binary data</td>
 </tr>
 </table>

32. Would look like this as a CSV:

```CSV
Parameter, Name, Description
"t", Text, Treats file as text data; also the default value
"b", Binary, Treats the file as binary data
```

33. So when writing data to a `CSV` file, we need Python to understand the row structure and comma-separated syntax for the file type.

34. Specifically, we need Python to understand we are writing individual rows of data to the file, and we need Python to understand that those rows consist of columns of data separated by columns.

### The CSV Module

35. Thankfully, Python has a built-in [`CSV` module](https://docs.python.org/3/library/csv.html) with specialized functions designed to help with writing `CSV` files.

#### A Quick Detour Into Packages, Modules, and Libraries

36. We're now starting to encounter language like `package`, `module`, and `library` when working in Python.

37. All of these terms refer to external Python programs that we can use in our program without having to recreate the entire original code.

38. We can think of these resources as "expansion packs" for Python that expand or extend the programming language's built-in functionality.

39. A few preliminary definitions...

40. A ***module*** is a Python file that typically includes specialized functions and variables. 
- Modules typically have `.py` file extensions.

41. A single or simple directory of modules is called a ***package***. 
- Packages are typically a simple directory with multiple modules.
- They include an `__init__.py` file that provides additional details on how to initialize the package and access its modules.
- Packages can also contain sub-packages

42. A ***library*** includes blocks of code that can be reused within a program. Libraries are a collection of modules.
- Libraries can include methods we call using period-method name (`.method_name()`)
- They have a much more complex directory/sub-directory/etc structure than packages

43. Some modules, packages, and libraries are built-in to Python and require no additional installation.

44. Others have to be installed (typically at the command line, or in the terminal) before you can import and use them in a program.

#### Back to the `CSV` Module

45. We can create a file using the `open()` function covered in a previous section of the lab.

```Python
 # create new CSV file with write privileges
 f = open("new_file.csv", "w")
```
 
46. The next step is to create the `writer` object using the `csv.writer()` function.

```Python
# create writer object
outputWriter = csv.writer(f)
```

47. Next, we can use the `.writerow()` method to write individual lists as rows in our `CSV` file.

```Python
# write first row
outputWriter.writerow(['Parameter', 'Name', 'Description')]

# write second row
outputWriter.writerow(['t', 'Text', 'Treats file as text data; also the default value'])

# write third row
outputWriter.writerow(['b', 'Binary', 'Treats the file as binary data')]
```

48. After we have finished writing new rows of data, we can close the file.

```Python
f.close()
```

49. Putting that all together:

```Python
 # create new CSV file with write privileges
 f = open("new_file.csv", "w")
 
 # create writer object
outputWriter = csv.writer(f)

# write first row
outputWriter.writerow(['Parameter', 'Name', 'Description')]

# write second row
outputWriter.writerow(['t', 'Text', 'Treats file as text data; also the default value'])

# write third row
outputWriter.writerow(['b', 'Binary', 'Treats the file as binary data')]

# close file
f.close()
```

50. Check out `new_file.csv` to see the newly-created file with rows of data.

## Reading a `.csv` file into Python

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=1bf35b7c-81c2-4e5e-a754-add3014d8c3c">File Methods: Reading a CSV File Into Python</a></td>
  </tr>
  </table>

51. To read data from a `.csv` file into Python, we will use the `csv` module.

<blockquote>Check out <a href = "https://docs.python.org/3/library/csv.html#module-csv">Python's documentation</a> to learn more about the <code>csv</code> module.</blockquote>

52. The `csv` module allows us to create a `reader` object that iterates over lines in a `.csv` file.

53. What does this workflow look like? 
```python
# import csv module
import csv

# open csv file
exampleFile = open('example.csv')

# create reader object from lines of data in example.csv file using csv.reader function
exampleReader = csv.reader(exampleFile)

# create list with rows of data from example.csv file
exampleData = list(exampleReader)

# output list rows
exampleData
```

54. You'll notice that the `exampleData` output is a list of lists, or a list that contains sub-lists. 

55. Each row of data from the original `example.csv` file is a sub-list (with field values separated by commas) within the `exampleData` list.

56. Now we can access the value at a particular row and column using the expression `exampleData[row][col]`.
 
57. `row` is the index position of one of the lists in `exampleData`. 

58. `col` is the index position of the item located in that list.

59. For example, `exampleData[0][0]` would give us the first string from the first list. 

60. `exampleData[0][1]` would give us the second string from the first list.

## Reading `.csv` data using a `for` loop

61. The method we just used to read data from a `.csv` file into Python loads the entire file into memory at once.

62. If we use this method on a large `.csv` file, Python is going to try to load the entire file into memory at once. Which does not bode well for Python or your computer's performance.

63. We can use a `reader` object as part of a `for` loop to iterate through the lines in a `.csv` file and load the file line-by-line.

<blockquote>Remember <code>for</code> loops iterate through each item in a series or list of items and performs the content of the loop on each item.</blockquote>

64. What does this workflow look like?
```python
# import csv module
import csv

# open .csv file
exampleFile = open('example.csv')

# create reader object from .csv file
exampleReader = csv.reader(exampleFile)

# iterate through each row in .csv file and print out row content and number
for row in exampleReader:
  print('Row #' + str(exampleReader.line_num) + ' ' + str(row))
```

65. This program imports the `csv` module, makes a `reader` object from the `example.csv` file, and loops through each of the rows in the `reader` object.

66. Each row is a list of values, and each value represents a cell.

67. The `print()` function prints the current row number and that row's contents. 

68. The `reader` object includes a `line_num` variable, which contains the number of the current line.

69. NOTE: The `reader` object can only be looped over once. If you need to re-read the same `.csv` file, you'll use `csv.reader` to create a new `reader` object.

## Other delimiters

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=59159f47-4764-4422-b65b-add301517243">Other Delimiters</a></td>
  </tr>
  </table>

70. But what happens if you need to load in structured data that uses another delimiter, not a comma? 

71. Remember when we opened a `.csv` file in a plain-text editor, the value fields are separated by a comma.

72. But commas are not the only possible delimiter. Tabs, spaces, pipes, or other characters can be used to separate or delimit fields in a dataset.

<table>
	<tr>
		<td>Delimiter Name</td>
		<td>Symbol</td>
		<td>Python Expression</td>
	</tr>
	<tr>
		<td>Tab</td>
		<td><code>\t</code></td>
		<td><code>delimiter = "\t"</code></td>
	</tr>
	<tr>
		<td>Space</td>
		<td><code> </code></td>
		<td><code>delimiter = " "</code></td>
	</tr>
	<tr>
		<td>Pipe</td>
		<td><code>|</code></td>
		<td><code>delimiter = "|"</code></td>
	</tr>
	</table>

73. The `csv` module includes a range of formatting parameters, known as a `Dialect` class. 

74. The `Dialect` class includes a range of methods you can use to specify alternate delimiters and (as we'll discover shortly), handle situations like special characters, line breaks, etc.

75. The `delimiter` attribute in the `Dialect` class lets us specify what delimiter is being used in the data we want to load.

```Python
# import csv module
import csv

# load tab-separated value file
tsv_file = open(FILE NAME)

# create a reader object and specify the new delimiter
read_tsv = csv.reader(tsv_file, delimiter=SPECIFY DELIMITER HERE)

# use a for loop to read in the data
for row in read_tsv:
  print(row)
```

<blockquote>Q4: Modify the code provided above to load the example.txt file provided in this lab.</blockquote>

## Escape characters

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=59159f47-4764-4422-b65b-add301517243">Escape Characters</a></td>
  </tr>
  </table>

76. But what happens if the values in your dataset include the same character that's being used as a delimiter?

77. For example, let's say you have address data in the following structure:

Name | Age | Address
--- | --- | ---
Jerry | 10 | 2776 McDowell Street, Nashville, Tennessee
Tom | 20 | 3171 Jessie Street, Westerville, Ohio
Mike | 30 | 1818 Sherman Street, Hope, Kansas

78. In this example, we want to keep `Address` as an intact field and not separate based on the commas located within the address.

79. In order to do this, we need to specify how Python parses fields that include the delimiter character.

80. The `quotechar` attribute in the `Dialect` class specifies what character will be used to enclose fields that should be treated as distinct entities and not be split into columns or fields based on the presence of the delimiter character within the field.

81. The default for `quotechar` is `"` (double quotation marks).

82. So what does that mean? We put double quotation marks around the field that includes the delimiter character.

83. Modified data structure:

Name | Age | Address
--- | --- | ---
Jerry | 10 | "2776 McDowell Street, Nashville, Tennessee"
Tom | 20 | "3171 Jessie Street, Westerville, Ohio"
Mike | 30 | "1818 Sherman Street, Hope, Kansas"

84. Then we can read the modified data into Python.

85. But what happens if we have quotation marks within a field that needs to be treated as a distinct entity?

86. For example, the following data structure would run into problems when read into Python.

Id | User | Comment
--- | --- | ---
1 | Bob | "John said "Hello World""
2 | Tom | ""The Magician""
3 | Harry | ""walk around the corner" she explained to the child"
4 | Louis | "He said, "stop pulling the dog's tail""

87. See our problem? The `Comment` field is enclosed with double quotation marks but also includes quotation marks in the field. 

88. We need Python to understand the enclosing double quotation marks serve a different purpose than the double quotation marks contained within the `Comment` field.

89. We can use a blackslash `\` character to escape the embedded double quotes.

90. Modified data structure:

<table>
	<tr>
		<th>Id</th>
		<th>User</th>
		<th>Comment</th>
	</tr>
	<tr>
		<td>1</td>
		<td>Bob</td>
		<td>"John said \"Hello World\""</td>
	</tr>
	<tr>
		<td>2</td>
		<td>Tom</td>
		<td>"\"The Magician\""</td>
	</tr>
	<tr>
		<td>3</td>
		<td>Harry</td>
		<td>"\"walk around the corner\" she explained to the child"</td>
	</tr>
	<tr>
		<td>4</td>
		<td>Louis</td>
		<td>"He said, \"stop pulling the dog's tail\""</td>
	</tr>
	</table>

91. Since the default for `quotechar` is `"`, we need to modify that default to reflect the new data structure.

```Python
# import csv module
import csv

# read csv using quote quotechar
# NOTE: This is placeholder code- it will not run as written...unless you have a csv file with this name

with open('MY-FILE-NAME.csv', 'rt') as f:
  csv_reader = csv.reader(f, skipinitialspace=True, quotechar='\\')
  
  for line in csv_reader:
    print(line)
```

<blockquote>Q5: Describe the concept of escape characters or quote characters in your own words. Describe a situation in which escape characters would be needed, and how you would address that challenge using Python syntax.</blockquote>
  
# Reading in `.csv` files using dictionaries

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=b1d40bd6-1199-4368-a467-add30156e3be">Reading in a CSV File Using Dictionaries</a></td>
  </tr>
  </table>

92. For `.csv` files that contain header rows, we might want to connect the header row values with subsequent row values.

93. We can do this by reading the `.csv` file as a dictionary, rather than a list containing row sub-lists.

94. Remember dictionaries have key-value pairs, where we can access a value by using its key name.

95. For tabular data, we can think of the key as the field name contained in the header row and the value as column or field values.

96. We read a `.csv` file to a dictionary using a `DictReader` object (versus the `csv.reader` object).

```Python
# import csv module
import csv

# open csv file
exampleFile = open('exampleWithHeader.csv')

# reading exampleFile to a DictReader object
exampleDictReader = csv.DictReader(exampleFile)

# outputs DictReader object as a dictionary
for line in exampleDictReader:
	print(line)
```

97. Within the `for` loop, the `DictReader` object sets `row` to a dictionary object with keys derived from the headers in the first row.

98. The `DictReader` object means we don't have to separate the header information from the rest of the data contained in the file, because the `DictReader` object does this for us.

99. But what can we do if we want to read to a dictionary a `.csv` file that doesn't incldue a header row?

100. We can pass a second argument to the `DictReader()` function to manually set header names.
 
```Python
# import csv module
import csv

# open csv file
exampleFile2 = open('example.csv')

# reading exampleFile to a dictionary with added field names
exampleDictReader2 = csv.DictReader(exampleFile, ['time', 'name', 'amount'])

# set keys for key-value pairs
for row in exampleDictReader2:
  print(row)
```

<blockquote>Q6: Describe in your own words how csv_DictReader interacts with structured data.</blockquote>

# Writing to a `.csv` file

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=a4deb213-a407-4a84-91dd-add3015a5d6f">Writing to a CSV File</a></td>
  </tr>
  </table>

101. We can create a `writer` object using the `csv.writer()` function to write data to a `.csv` file.

```Python
# import csv module
import csv

# create and open output.csv file in write mode
outputFile = open('output.csv', 'w')

# create writer object
outputWriter = csv.writer(outputFile)

# write first row
outputWriter.writerow(['spam', 'eggs', 'bacon', 'ham'])

# write another row
outputWriter.writerow(['Hello, world!', 'eggs', 'bacon', 'ham'])

# write a third row
outputWriter.writerow([1, 2, 3.141592, 4])

# close the output file
outputFile.close()
```

102. The `writerow()` method takes a list argument and writes that to a new row in the `writer` object, that is added to the `.csv` file.

<blockquote>Q7: Create a small data structure and write it to a CSV file. Include code + comments.</blockquote>

## Writing from a dictionary to a `.csv` file

103. We can use the `DictWriter` object to write data in a dictionary to a `.csv` file.

```Python
# import csv module
import csv

# create and open output.csv file in write mode
outputFile = open('output.csv', 'w')

# create writer object
outputDictWriter = csv.DictWriter(outputFile, ['Name', 'Pet', 'Phone'])

# create header row
outputDictWriter.writeheader()

# write first row
outputDictWriter.writerow({'Name': 'Alice', 'Pet': 'cat', 'Phone': '555-1234'})

# write another row
outputDictWriter.writerow({'Name': 'Bob', 'Phone': '555-9999'})

# write a third row
outputDictWriter.writerow({'Phone': '555-5555', 'Name': 'Carol', 'Pet': 'dog'})

# close the output file
outputFile.close()
```

104. Note that the order of the key-value pairs in the dictionaries created manually using `writerow()` doesn't matter.

105. Python writes the dictionaries to the `.csv` file using the order of the keys given to `DictWriter()`.

106. Missing keys will be empty in the newly-created `.csv` file.

<blockquote>Q8: Create a small dictionary and write it to a CSV file. Include code + comments.</blockquote>

## Additional CSV Lab Notebook Questions

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=783c4603-b270-48eb-9d09-add3015e7721">Lab Notebook Questions 9-11</a></td>
  </tr>
  </table>

Q9: Navigate to an open data portal and download a `.csv` file. 

A few places to start:
- [Data.gov](https://www.data.gov/)
- [City of Chicago Data Portal](https://data.cityofchicago.org/)
- [City of South Bend Open Data](https://data-southbend.opendata.arcgis.com/)
- [Sports Reference](https://www.sports-reference.com/)

These open data portals are catalogs of datasets- you will need to explore the websites to identify and then download a specific dataset.

Open the data in a spreadsheet program and/or text editor. 
- What do you see?
- How can we start to make sense of the data based on available documentation?

Q10: Write code + comments that load the data in Python using the two different approaches highlighted in this lab:
- Lists and sublists (steps 51-60, or steps 61-69 for loading the file using a for loop)
- Dictionaries (steps 92-98, and steps 99-100 cover how to deal with a file that does not include a header row)

Q11: What challenges did you encounter for Q9 and Q10? How did you address or solve them? 

# JSON

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=590176fc-855a-4537-8d4e-add30162fb87">JSON Data in Python</a></td>
  </tr>
  </table>


## What is JSON and why are we learning about it

107. JavaScript Object Notation (JSON) is as popular way to format data as a single (purportedly human-readable) string. 

108. JavaScript programs use JSON data structures, but we can frequently encounter JSON data outside of a JavaScript environment.

109. Websites that make machine-readable data available via an application programming interface (API- more on these in an upcoming lab) often provide that data in a JSON format. Examples include Twitter, Wikipedia, Data.gov, etc. Most live data connections available via an API are provided in a JSON format.

110. JSON structure can vary WIDELY depending on the specific data provider, but this lab will cover some basic elements of working with JSON in Python.

111. The easiest way to think of JSON data as a plain-text data format made up of something like key-value pairs, like we've encountered previously in working with dictionaries.

112. Example JSON string: `stringOfJsonData = '{"name": Zophie", "isCat": true, "miceCaught": 0, "felineIQ": null}'`

113. From looking at the example string, we can see field names or keys (`name`, `isCat`, `miceCaught`, `felineIQ`) and values for those fields.

114. To use more precise terminology, JSON data has the following attributes:
- uses name/value pairs
- separates data using commas
- holds objects using curly braces `{}`
- holds arrays using square brackets `[]`

115. In our example `stringOfJsonData`, we have an object contained in curly braces. 

116. An object can include multiple name/value pairs. Multiple objects together can form an array.

117. Values stored in JSON format must be one of the following data types:
- string
- number
- object (JSON object)
- array
- boolean
- null

118. How is data stored in a JSON format different than a CSV? 

119. A `.csv` file uses characters as delimiters and has more of a tabular (table-like) structure.

120. JSON data uses characters as part of the syntax, but not in the same way as delimited data files. 

121. Additionally, the data stored in a JSON format has values that are attached to names (or keys).

122. JSON can also have a hierarchical or nested structure, in that objects can be stored or nested inside other objects as part of the same array.

123. For example, take a look at sapmle JSON data from Twitter's API:

```JSON
{
  "created_at": "Thu Apr 06 15:24:15 +0000 2017",
  "id_str": "850006245121695744",
  "text": "1\/ Today we\u2019re sharing our vision for the future of the Twitter API platform!\nhttps:\/\/t.co\/XweGngmxlP",
  "user": {
    "id": 2244994945,
    "name": "Twitter Dev",
    "screen_name": "TwitterDev",
    "location": "Internet",
    "url": "https:\/\/dev.twitter.com\/",
    "description": "Your official source for Twitter Platform news, updates & events. Need technical help? Visit https:\/\/twittercommunity.com\/ \u2328\ufe0f #TapIntoTwitter"
  },
  "place": {   
  },
  "entities": {
    "hashtags": [      
    ],
    "urls": [
      {
        "url": "https:\/\/t.co\/XweGngmxlP",
        "unwound": {
          "url": "https:\/\/cards.twitter.com\/cards\/18ce53wgo4h\/3xo1c",
          "title": "Building the Future of the Twitter API Platform"
        }
      }
    ],
    "user_mentions": [     
    ]
  }
}
```

<blockquote>Q12: Decipher what we're seeing in the JSON here. What are some of the name/value pairs, and how are they organized in this object?</blockquote>

## Reading JSON into Python

124. We can read JSON into Python using the `json` module.

<blockquote><a href="https://docs.python.org/3/library/json.html">Click here</a> to learn more about the <code>json</code> module.</blockquote>

125. The JSON module includes a few key functions for loading JSON data into Python:
- `json.loads()` takes a single string of JSON and loads it as a Python value
- `json.load()` takes a JSON file (or file-like object) and loads it as a Python value
- `json.dumps()` takes a Python value and transforms it to a JSON object.

126. Translation table:

JSON | Python
--- | ---
object | dict
array | list
string | str
number (int) | int
number (real) | float
true | True
false | False
null | None

127. To translate a string of JSON data into a Python value, we pass it to the `json.loads()` function.

```Python
# import json module
import json

# string of JSON data
stringOfJsonData = '{"name": "Zophie", "isCat": true, "miceCaught": 0, "felineIQ": null}'

# load JSON data as Python value 
jsonDataAsPythonValue = json.loads(stringOfJsonData)

# output JSON string as Python value
jsonDataAsPythonValue
```

128. This block of code imports the `json` module, calls the `loads()` function and passes a string of JSON data to the `loads()` function.

129. A few notes on this workflow:
- JSON strings always use double quotes, which is rendered in Python as a dictionary. Because Python dictionaries are not ordered, the order of the Python dictionary may not match the original JSON string order.
- In this example, we are loading a single string of JSON, which means we use the `json.loads()` function. When loading a JSON file (or file-like object), we would need to use the `json.load()` argument.

## Working with JSON in Python

130. Now that the JSON data is stored as a dictionary in Python, we can interact with it via the functionality avaialble via Python dictionaries.

131. We could get all of the keys in the dictionary using the `keys()` method.

```Python
# import json module
import json

# string of JSON data
stringOfJsonData = '{"name": "Zophie", "isCat": true, "miceCaught": 0, "felineIQ": null}'

# load JSON data as Python value 
jsonDataAsPythonValue = json.loads(stringOfJsonData)

# print list of keys
print(jsonDataAsPythonValue.keys())
```

132. We could get all of the values in the dictionary using the `values()` method.

```Python
# import json module
import json

# string of JSON data
stringOfJsonData = '{"name": "Zophie", "isCat": true, "miceCaught": 0, "felineIQ": null}'

# load JSON data as Python value 
jsonDataAsPythonValue = json.loads(stringOfJsonData)

# print list of values
print(jsonDataAsPythonValue.values())
```

133. We could iterate by keys over the items in the dictionary.

```Python
# import json module
import json

# string of JSON data
stringOfJsonData = '{"name": "Zophie", "isCat": true, "miceCaught": 0, "felineIQ": null}'

# load JSON data as Python value 
jsonDataAsPythonValue = json.loads(stringOfJsonData)

# iterate by keys using for loop
for key in jsonDataAsPythonValue.keys():
  print(key, jsonDataAsPythonValue[key])
```

134. We could also iterate over items in dictionary using key-value pairs.

```Python
# import json module
import json

# string of JSON data
stringOfJsonData = '{"name": "Zophie", "isCat": true, "miceCaught": 0, "felineIQ": null}'

# load JSON data as Python value 
jsonDataAsPythonValue = json.loads(stringOfJsonData)

# iterate by key value pairs using for loop
for key, value in jsonDataAsPythonValue.items():
  print(key, value)
```

135. We can read the value for a particular key using the index operator. The command `jsonDataAsPythonValue['name']` will return `Zophie`.

136. In situations where JSON data includes nested or hierarchical objects and arrays, we will end up with a list of dictionaries in Python.

137. For example, let's say we have a different JSON example and want to use more complex expressions in Python.

```Python
# import json module
import json

# new json data
data = '''
[
  { "id" : "001",
    "x" : "2",
    "name" : "Chuck"
  } ,
  { "id" : "009",
    "x" : "7",
    "name" : "Brent"
  }
]'''

#load data as json
info = json.loads(data)

# print number of users
print('User Count:', len(info))

# use for loop to print list of names, IDs, and attributes
for item in info:
  print('Name', item['name'])
  print('Id', item['id'])
  print('Attribute', item['x'])
```

138. For more on working with dictionaries in Python:
- [Elements of Computing I lab](https://github.com/kwaldenphd/python-lab6/blob/master/README.md#working-with-dictionaries)
- [W3 Schools tutorial](https://www.w3schools.com/python/python_dictionaries.asp)

## Writing to JSON from Python

139. The `json.dumps()` function will translate a Python dictionary into a string of JSON-formatted data.

```Python
# import json module
import json

# Python dictionary
pythonValue = {'isCat': True, 'miceCaught': 0, 'name': 'Zophie', 'felineIQ': None}

# translate Python value to JSON string
stringOfJsonData = json.dumps(pythonValue)

stringOfJsonData
```

140. We can also write data in a Python dictionary to a JSON file also using `json.dump()`.

```Python
# import json module
import json

# Python dictionary
pythonValue = {'isCat': True, 'miceCaught': 0, 'name': 'Zophie', 'felineIQ': None}

# create new JSON file and write dictionary to file
with open('output.json', 'w') as json_file:
	json.dump(pythonValue, json_file)
```

141. Later in the semester we will talk about how to read JSON data into Python and convert it to a tabular data structure (called a data frame in Python), using a library called `pandas`. Stay tuned!

<blockquote>Q13: Create a string of JSON data and write it to a JSON file. Include code + comments.</blockquote>

## Additional JSON Lab Notebook Questions

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=39ca985f-224f-4e6d-9f8a-add3016c37a8">Lab Notebook Questions 14-16</a></td>
  </tr>
  </table>

Q14: Navigate to an open data portal and download a JSON file. 

Some options that can get you started:
- [Data.gov](https://www.data.gov/)
- [City of Chicago Data Portal](https://data.cityofchicago.org/)
- [City of South Bend Open Data](https://data-southbend.opendata.arcgis.com/)

These open data portals are catalogs of datasets- you will need to explore the websites to identify and then download a specific dataset.

Open the data in a spreadsheet program and/or text editor.

Describe what are you seeing. How can we start to make sense of this data? What documentation is available?

Q15: Write code + comments that accomplish the following tasks:
- Load the JSON data into Python
- Convert to a Python value

Steps 124-129 in the lab procedure provide sample code and additional considerations for loading a JSON file in Python.

- In the JSON example in the lab, we loaded a single string of JSON, which means we use the `json.loads()` function. 
- When loading a JSON file (or file-like object), we would need to use the `json.load()` argument.

Q16: What challenges did you encounter for Q14 and Q15? How did you address or solve them? 

Q17: Include a link to your Replit project.

# Lab Notebook Questions

Lab notebook template:
- [`.py` file](https://drive.google.com/file/d/1Dacp329cBMosmJvJcD10qSavgHpP3rYN/view?usp=sharing)
- [Jupyter Notebook](https://colab.research.google.com/drive/1sL-GUG-NtBguee6NaYoazgPQmdKxmWpV?usp=sharing)

Q1: Open the `example.xlsx` file in a text editor. Describe what you see.

Q2: How does your answer to Q1 compare to what you see when you open the `example.csv` file in a text editor?

Q3: Open the `example.xlsx` file in a spreadsheet program. What happens when you try to save the file as a `.csv` format? What happens when you open the newly-created `csv` file in a spreadsheet program or text editor?

Q4: Modify the code provided to load the `example.txt` file.

```Python
# import csv module
import csv

# load tab-separated value file
tsv_file = open(FILE NAME)

# create a reader object and specify the new delimiter
read_tsv = csv.reader(tsv_file, delimiter=SPECIFY DELIMITER HERE)

# use a for loop to read in the data
for row in read_tsv:
  print(row)
```

Q5: Define escape characters or quote characters in your own words. Describe a situation in which escape characters would be needed, and how you would address that challenge using Python syntax.

Q6: Describe in your own words how `csv_DictReader` interacts with structured data.

Q7: Create a small data structure and write it to a CSV file. Include code + comments.

Q8: Create a small dictionary and write it to a CSV file. Include code + comments.

Q9: Navigate to an open data portal and download a `.csv` file. 

A few places to start:
- [Data.gov](https://www.data.gov/)
- [City of Chicago Data Portal](https://data.cityofchicago.org/)
- [City of South Bend Open Data](https://data-southbend.opendata.arcgis.com/)
- [Sports Reference](https://www.sports-reference.com/)

Open the data in a spreadsheet program and/or text editor. 
- What do you see?
- How can we start to make sense of the data based on available documentation?

Q10: Write code + comments that load the data in Python using the two different approaches highlighted in this lab:
- Lists and sublists (steps 51-60, or steps 61-69 for loading the file using a for loop)
- Dictionaries (steps 92-98, and steps 99-100 cover how to deal with a file that does not include a header row)

Q11: What challenges did you encounter for Q9 and Q10? How did you address or solve them? 

Q12: Decipher what we're seeing in the JSON here. What are some of the name/value pairs, and how are they organized in this data object?

Q13: Create a string of JSON data and write it to a JSON file. Include code + comments.

Q14: Navigate to an open data portal and download a JSON file. 

Some options that can get you started:
- [Data.gov](https://www.data.gov/)
- [City of Chicago Data Portal](https://data.cityofchicago.org/)
- [City of South Bend Open Data](https://data-southbend.opendata.arcgis.com/)

Open the data in a spreadsheet program and/or text editor 

Describe what are you seeing. How can we start to make sense of this data? What documentation is available?

Q15: Write code + comments that accomplish the following tasks:
- Load the JSON data into Python
- Convert to a Python value

The lab procedure provides sample code and additional considerations for loading a JSON file in Python.

- In the JSON example in the lab, we loaded a single string of JSON, which means we use the `json.loads()` function. 
- When loading a JSON file (or file-like object), we would need to use the `json.load()` argument.

Q16: What challenges did you encounter for Q14 and Q15? How did you address or solve them? 

Q17: Include a link to your Replit project.