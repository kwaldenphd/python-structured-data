# Structured Data & File I/O in Python

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>This tutorial was written by Katherine Walden and is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Overview & Goals

This lab provides an overview of fundamental programming concepts in the areas of file I/O and working with structured data, with a focus on Python syntax. Topics covered include:
- Delimited (`.csv`, `.tsv`) and name-value (`.json`, `.xml`) data structures
- Escape characters in relation to delimited data structures
- Working with delimited and name-value data structures in the Python programming environment, with a focus on the `csv` + `json` modules and `list` + `dictionary` data structures
- File I/O and file methods/access modes, with a focus on Python workflows

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=304f6392-3cee-4ba6-8da5-af36013a4191">Lab overview</a></td>
  </tr>
  </table>
  
<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=d6f4dc20-0976-42ef-b453-af36012ed588">Lecture/live coding playlist</a></td>
  </tr>
  </table>

## Acknowledgements

Peer review and editing on the CSV portion of this lab was provided by Spring 2021 graduate teaching assistant [Aidan Draper](https://github.com/adraper2).

Peer review and editing on the JSON portion of this lab was provided by Spring 2021 graduate teaching assistant [Subhadyuti Sahoo](https://github.com/SDSAHOO703).

When building the CSV, JSON & file methods sections, the author consulted the following materials:
- Al Sweigart [*Automate the Boring Stuff With Python*](https://nostarch.com/automatestuff2) (No Starch Press, 2020).
  * Chapter 16 "Working With CSV Files and JSON Data" (371-388)
- Wes McKinney, "Chapter 6.1, Reading and Writing Data in Text Format" in [*Python for Data Analysis*](https://www.oreilly.com/library/view/python-for-data/9781491957653/) (O'Reilly, 2017): 169-184.
- Wes McKinney, Chapter 6 "Data Loading, Storage, and File Formats" from [*Python for Data Analysis*](https://www.oreilly.com/library/view/python-for-data/9781491957653/) (O'Reilly, 2018): 169-193

Information and exercises in the pandas sections were developed in consultation with the following resources:
- `pandas` package ["Getting started"](https://pandas.pydata.org/pandas-docs/stable/getting_started/intro_tutorials/) documentation.
- Wes McKinney's [*Python for Data Analysis: Data Wrangling With pandas, Numpy, and IPython*](https://www.oreilly.com/library/view/python-for-data/9781491957653/) (O'Reilly, 2017)
  * Chapter 5 "Getting Started with pandas" (125-168)
  * Chapter 7 "Data Cleaning and Preparation" (195-224)
  * Chapter 8 "Data Wrangling: Join, Combine, and Reshape" (225-256)
  * Chapter 10 "Data Aggregation and Group Operations" (293-322)

# Table of Contents
- [Lecture & Live Coding](#lecture--live-coding)
- [Key Terms](#key-terms)
- [Lab Notebook Template](#lab-notebook-template)
- [Data](#data)
- [Overview](#overview)
- [File I/O](#file-io)
- [Structured Data](#structured-data)
  * [Delimited Data](#delimited-data)
  * [JavaScript Object Notation](#javascript-object-notation)
- [Pandas](#pandas)
- [Putting It All Together](#putting-it-all-together)
- [How to Submit This Lab (and show your work)](#how-to-submit-this-lab-and-show-your-work)
- [Lab Notebook Questions](#lab-notebook-questions)

[Click here]() to access this lab procedure as a Jupyter Notebook.

# Lecture & Live Coding

Throughout this lab, you will see a Panopto icon at the start of select sections.

This icon indicates there is lecture/live coding asynchronous content that accompanies this section of the lab. 

You can click the link in the figure caption to access these materials (ND users only).

Example:

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=304f6392-3cee-4ba6-8da5-af36013a4191">Lab overview</a></td>
  </tr>
  </table>
  
<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=d6f4dc20-0976-42ef-b453-af36012ed588">Lecture/live coding playlist</a></td>
  </tr>
  </table>

## Key Concepts

[Click here](https://github.com/kwaldenphd/python-structured-data/blob/main/key-concepts.md) for a full list of key concepts and definitions from this lab.

## Lab Notebook Template

[Click here]() to access the lab notebook template as a Jupyter Notebook (Google CoLab, ND Users).

To download the notebok from Google Colaboratory (as a `.ipynb` file): 
- `File` (top-left corner) -> `Download` -> `Download as .ipynb`
- Once you have downloaded the file on your local computer, you can move it into a designated folder for this lab/class.

What folks will submit for this lab will include a Jupyter Notebook (`.ipynb`) file with responses to the lab questions. Upload the file to the Canvas assignment.
- If working in Google Colab, a shared link submission is fine.

## How to submit this lab (and show your work)

Moving forward, we're going to be submitting lab notebooks using the provide Jupyter Notebook template ([link for this lab's template](https://colab.research.google.com/drive/1e5SDiIxZVpMU_t_uQqv3MeTC0hYBwEYE?usp=sharing)).
- If working in JupyterLab (or another desktop IDE), download the `.ipynb` file to your local computer
  * `File` - `Download` - `Download as .ipynb`
- If working in Google Colaboratory, MAKE SURE you save a copy to your local drive. Otherwise your changes will not be saved.
  * `File` - `Save a copy in Drive`

The lab notebook template includes all of the questions as well as pre-created markdown cells for narrative text answers and pre-created code cells for any programs you may need to create. 
- Double click on these cells to edit and add your own content
- If questions do not require a code component, you can ignore those cells
- If questions to not require a narrative component, you can ignore those cells

If working in JupyterLab or another desktop IDE, upload the lab notebook template `.ipynb` file to Canvas as your lab submission.

If working in Google Colaboratory, submit the link to your notebook (checking sharing permissions, similar with Google Docs).

## Data

You'll need four data files for this lab.
- `example.csv`
- `example.txt`
- `example.xlsx`
- `exampleWithHeader.csv`

The lab procedure Jupyter Notebook as code to download these files. You can also access them [via Google Drive](https://drive.google.com/drive/folders/1Sp_N34753ONJRU2AFKcocQ2DhCEhyL-m?usp=sharing) (ND users only).

# Overview

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=304f6392-3cee-4ba6-8da5-af36013a4191">Lab overview</a></td>
  </tr>
  </table>

In programming languages and computing more broadly, `I/O` stands for `Input` and `Output`. 

We've seen `I/O` at work in previous labs, where we provided inputs to the computer (using a CPU simulator or working at the terminal), a task or operation was performed, and there was an endpoint or output for that process. A concrete example would be the assembly language program we wrote for Lab #2: How Comptuters Work (Hardware). We wrote assembly language instructions which served as inputs for the fetch-execute cycle, and the final output for the program was a data value stored in main memory.

Similarly, programming languages can take a variety of inputs (user-provided values, data, files, etc) and return outputs in a variety of formats (data stored in memory, output that shows up in the console, newly-created or -modified files, etc). We've seen `I/O` in action in previous labs, with Python's `print()` and `input()` functions.

In this lab, we're going to look at aspects of `I/O` that have to do with reading and writing files, with a focus on two key data structures:
- Tabular data, or data stored as a table consisting of rows and columns
- Data stored as name-value pairs, specifically in the JavaScript Object Notation (`.json`) format

We'll do so by interacting with Python's `csv` module and `json` package, along with the `pandas` Python library.

# File I/O & Access Modes

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=73668810-b5ed-4fc2-b606-af36012da392">File I/O in Python</a></td>
  </tr>
  </table>

Before we start loading data files in Python, let's talk more about how programming languages handle creating, reading, and writing files.

From Busbee and Braunschweig's "[File Input and Output](https://press.rebus.community/programmingfundamentals/chapter/file-input-and-output/)," in *Programming Fundamentals*:

<blockquote>"A computer file is a computer resource for recording data discretely in a computer storage device. Just as words can be written to paper, so can information be written to a computer file. 
<br><br>
"There are different types of computer files, designed for different purposes. A file may be designed to store a picture, a written message, a video, a computer program, or a wide variety of other kinds of data. Some types of files can store several types of information at once.
<br><br>
"By using computer programs, a person can open, read, change, and close a computer file. Computer files may be reopened, modified, and copied an arbitrary number of times."</blockquote>

To break that down:
- Files store information
- Files have different formats or types
- Core file tasks (when working in a programming environment): `open`, `read`, `modify` or `change`, `close`

We will be focusing on a few key Python functions for working with files.
- `open()`
- `read()`
- `write()`

### `open()`

The `open()` function lets us open an existing file or create a new file in Python. For either version of `open()` (new file or existing file), we need to specify the file name (with the file type extension) and access mode.

Core syntax for opening an existing file:

```Python
open(file_name.extension, access_mode)
```

The file type extension is the string of characters that follows the period after the file name. Examples include `.py`, `.csv`, `.txt`, etc. The types of file handling functions we are covering in this lab will generally only support reading and writing plain-text (or machine-readable) files.

### Access Modes

The access mode parameter specifies the types of modifications that can be made to the file. It can also specify the type of data or information contained in the file.

Possible access mode parameters:

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

Additionally, we can specify the type of data contained in the file, or how Python should handle the information in the file.

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
 
If you run these examples, you will see a newly-created file appear in your environment or project workspace. 

### `write()`

Now that we have a newly-created file in Python, we can use the `write()` function to ***write*** content to that file. Let's say we want to create a `.txt` (plain text) file and write a string to that file. We can do that using `write()`.

An example:

```Python
# creates new txt file with write permission
f = open("new_file.txt", "w")

# writes string to new file
f.write("Hello world!")

# closes file
f.close()
```

<blockquote>NOTE: It is <strong><em>very important</em></strong> to <code>close()</code> the file once you are done writing content or making modifications.</blockquote>

Another example where we have assigned a string to a variable and write the variable to the `.txt` file:

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

We can open the `new_file.txt` file to see the newly-added content.

For more on file handling methods in Python:
- [Python File Handling, W3Schools](https://www.w3schools.com/python/python_file_handling.asp)
- [Python File Write, W3Schools](https://www.w3schools.com/python/python_file_write.asp)
- [Python open() Function](https://www.w3schools.com/python/ref_func_open.asp)

# Structured Data

<table>
<tr><td><p align="center"><img src="https://github.com/kwaldenphd/python-structured-data/blob/main/images/One_Dimensional_Array.jpg?raw=true" width="500"></p></td><td><p align="center"><img src="https://github.com/kwaldenphd/python-structured-data/blob/main/images/Associative_Arrays.png?raw=true" width="500"></p></td></tr>
	<tr><td align="center">Linear Array</td><td align="center">Associative Array</td></tr></table>

In this lab, we're going to look at aspects of `I/O` that have to do with reading and writing files, with a focus on two key data structures:
- Tabular data, or data stored as a table consisting of rows and columns
- Data stored as name-value pairs, specifically in the JavaScript Object Notation (`.json`) format

We can connect these two types of data structures back to the concepts of linear and associative arrays covered previously in the course. A quick refresher:
- "In computer science, an array is a data structure consisting of a collection of elements (values or variables), each identified by at least one array index or key...The simplest type of data structure is a linear array, also called one-dimensional array" ([Wikipedia, "Array (data structure)](https://en.wikipedia.org/wiki/Array_(data_structure))")
- Associative arrays are "an abstract data type that stores a collection of (key, value) pairs, such that each possible key appears at most once in the collection" ([Wikpedia, Associative Array](https://en.wikipedia.org/wiki/Associative_array))

## Delimited Data

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=e87a9417-2ac4-47ed-ab74-af36012dc605">CSV Files</a></td>
  </tr>
  </table>

<p align="center"><img src="https://github.com/kwaldenphd/python-structured-data/blob/main/images/table_diagram.png?raw=true" width="1000"></p>

"A delimited file is a sequential file with column delimiters. Each delimited file is a stream of records, which consists of fields that are ordered by column. Each record contains fields for one row. Within each row, individual fields are separated by column delimiters. All fields must be delimited character strings, non-delimited character strings, or external numeric values. Delimited character strings can contain column delimiters and can also contain character string delimiters when two successive character string delimiters are used to represent one character." (IBM, "[Delimited File Format](https://www.ibm.com/docs/en/db2-for-zos/11?topic=utilities-delimited-file-format)", 5 February 2022)

One of the most common examples of a delimited data structure is a table, with file formats you may open using spreadsheet programs like Microsoft Excel, Google Sheets, or Apple Numbers. However, the file formats associated with spreadsheet programs (`.xlsx` for Microsoft Excel and `.numbers` for Numbers) are NOT plain-text formats. Try to open these file types in a text editor and you'll quickly see the additional content and markup added by the spreadsheet program.

For this lab, we'll be working with the `.csv` file type. CSV stands for "comma-separated values." CSV files are tabular data structures (i.e. a spreadsheet), stored in a plain-text format. In `.csv` files, each line represents a row in the spreadsheet, and commas separate cells in each row (thus the file format name comma-separated values). At first glance, `.csv` files look similar to proprietary spreadsheet program file formats, such as files saved in Microsoft Excel or Apple Numbers. 

A few characteristics that distinguish `.csv` files (or other plain-text delimited data formats) from proprietary spreadsheet file types:
- Columns in a `.csv` file don't have a value type. Everything is a string.
- Values in a `.csv` file don't have font or color formatting
- `.csv` files only contain single worksheets
- `.csv` files don't store formatting information like cell width/height
- `.csv` files don't recognize merged cells or other kinds of special formatting (frozen or hidden rows/columns, embedded images, etc.)

Given these limitations, especially compared to the way we often interact with spreadsheet programs like Microsoft Excel or Google Sheets, what's the advantage of working with `.csv` files? One key advantage of `.csv` files is their simplicity. You can load or open a `.csv` file in a text editor and be able to quickly see the values in the file. When working with data in a programming environment, `.csv` files as a plain-text format simplify the process of loading structured data.

### `.csv` Files in Python

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=daa7977b-0124-4031-bd4c-af36012de8a0">Reading a CSV File into Python</a></td>
  </tr>
  </table>

To recap: `CSV` stands for comma-separated values, and `CSV` files are the plain-text, machine-readable file type for tabular data (table data, or data in a spreadsheet structure)

For example, a table that looks like this in a spreadsheet program like Excel or Google Sheets:

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

Would look like this as a `.csv`:

```CSV
Parameter, Name, Description
"t", Text, Treats file as text data; also the default value
"b", Binary, Treats the file as binary data
```

So when writing data to a `.csv` file, we need Python to understand the row structure and comma-separated syntax for the file type. Specifically, we need Python to understand we are writing individual rows of data to the file, and we need Python to understand that those rows consist of columns of data separated by columns.

Thankfully, Python has a built-in [`CSV` module](https://docs.python.org/3/library/csv.html) with specialized functions designed to help with writing `CSV` files. We can import the module using an `import` statement a the start of our program.

```Python
import csv
```

<blockquote>Remember Python includes modules, packages, and libraries we can import and use in our programs. A module is a Python file that typically includes specialized functions and variables. Modules typically have <code>.py</code> file extensions. A single or simple directory of modules is called a package. Packages are typically a simple directory with multiple modules.</blockquote>

#### `open` & `write`

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=8fb9b7e3-5ed0-42d0-bfc3-af36012e4924">Writing to a CSV File into Python</a></td>
  </tr>
  </table>

We can create a file using the `open()` function covered in a previous section of the lab.

```Python
 # create new CSV file with write privileges
 f = open("new_file.csv", "w")
```
 
The next step is to create the `writer` object using the `writer()` function from the `csv` module.

```Python
# create writer object
outputWriter = csv.writer(f)
```

Next, we can use the `.writerow()` method to write individual lists as rows in our `.csv` file.

```Python
# write first row
outputWriter.writerow(['Parameter', 'Name', 'Description')]

# write second row
outputWriter.writerow(['t', 'Text', 'Treats file as text data; also the default value'])

# write third row
outputWriter.writerow(['b', 'Binary', 'Treats the file as binary data')]
```

After we have finished writing new rows of data, we can close the file using the `close()` function.

```Python
f.close()
```

Putting that all together:

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

Check out `new_file.csv` to see the newly-created file with rows of data.

#### `read`

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=daa7977b-0124-4031-bd4c-af36012de8a0">Reading a CSV File into Python</a></td>
  </tr>
  </table>

We'll also use the `csv` module to read or load an existing `.csv` file into Python. The `csv` module allows us to create a `reader` object that iterates over lines in a `.csv` file.

What does this workflow look like? 
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
print(exampleData)
```

You'll notice that the `exampleData` output is a list of lists, or a list that contains sub-lists. Each row of data from the original `example.csv` file is a sub-list (with field values separated by commas) within the `exampleData` list.

Now we can access the value at a particular row and column using the expression `exampleData[row][col]`.
- `row` is the index position of one of the lists in `exampleData`. 
- `col` is the index position of the item located in that list.

For example, `exampleData[0][0]` would give us the first string from the first list. `exampleData[0][1]` would give us the second string from the first list.

##### Reading `.csv` data using a `for` loop

The method we just used to read data from a `.csv` file into Python loads the entire file into memory at once. If we use this method on a large `.csv` file, Python is going to try to load the entire file into memory at once. Which does not bode well for Python or your computer's performance. We can use a `reader` object as part of a `for` loop to iterate through the lines in a `.csv` file and load the file line-by-line.

<blockquote>Remember <code>for</code> loops iterate through each item in a series or list of items and performs the content of the loop on each item.</blockquote>

What does this workflow look like?
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

This program imports the `csv` module, makes a `reader` object from the `example.csv` file, and loops through each of the rows in the `reader` object. Each row is a list of values, and each value represents a cell. 
- The `print()` function prints the current row number and that row's contents. 
- The `reader` object includes a `line_num` variable, which contains the number of the current line.

<blockquote>NOTE: The <code>reader</code> object can only be looped over once. If you need to re-read the same <code>.csv</code> file, you'll use <code>csv.reader()</code> to create a new <code>reader</code> object.</blockquote>

##### Reading `.csv` data as a `dictionary`

For `.csv` files that contain header rows, we might want to connect the header row values with subsequent row values. We can do this by reading the `.csv` file as a dictionary, rather than a list containing row sub-lists. Remember dictionaries have key-value pairs, where we can access a value by using its key name. For tabular data, we can think of the key as the field name contained in the header row and the value as column or field values.

We read a `.csv` file to a dictionary using a `DictReader` object (versus the `csv.reader` object).

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

Within the `for` loop, the `DictReader` object sets `row` to a dictionary object with keys derived from the headers in the first row. The `DictReader` object means we don't have to separate the header information from the rest of the data contained in the file, because the `DictReader` object does this for us.

But what can we do if we want to read to a dictionary a `.csv` file that doesn't incldue a header row? We can pass a second argument to the `DictReader()` function to manually set header names.
 
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

#### `write`

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=8fb9b7e3-5ed0-42d0-bfc3-af36012e4924">Writing to a CSV File into Python</a></td>
  </tr>
  </table>

To write data to a `.csv` file in Python, we can create a `writer` object using the `csv.writer()` function to write data to a `.csv` file.

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

The `writerow()` method takes a list argument and writes that to a new row in the `writer` object, that is added to the `.csv` file.

##### Writing from a dictionary to a `.csv` file

We can use a `DictWriter` object to write data in a dictionary to a `.csv` file.

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

Note that the order of the key-value pairs in the dictionaries created manually using `writerow()` doesn't matter. Python writes the dictionaries to the `.csv` file using the order of the keys given to `DictWriter()`. Missing keys will be empty in the newly-created `.csv` file.

### Application

Q1A: Create a small list data structure and write it to a CSV file. Answer to this question includes program + comments that document process and explain your code.

Q1B: Create a small dictionary and write it to a CSV file. Answer to this question includes program + comments that document process and explain your code.

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=75282aad-8ad0-4b99-be00-af36012e6021">Lab Notebook Question 3</a></td>
  </tr>
  </table>

# Delimiters & Escape Characters 

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=7a0e11d5-7d94-407f-88bf-af36012e2496">Delimiters & Escape Characters</a></td>
  </tr>
  </table>

## Other delimiters

What happens if you need to load in structured data that uses another delimiter, not a comma? Remember when we opened a `.csv` file in a plain-text editor, the value fields are separated by a comma.

But commas are not the only possible delimiter. Tabs, spaces, pipes, or other characters can be used to separate or delimit fields in a dataset.

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

The `csv` module includes a range of formatting parameters, known as a `Dialect` class. The `Dialect` class includes a range of methods you can use to specify alternate delimiters and (as we'll discover shortly), handle situations like special characters, line breaks, etc.

The `delimiter` attribute in the `Dialect` class lets us specify what delimiter is being used in the data we want to load. An example we'll come back to in application questions for this section of the lab:

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

# JavaScript Object Notation

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=ce1a1c2b-8fcb-4901-9bb5-af36012e81fe">JavaScript Object Notation Files</a></td>
  </tr>
  </table>

<p align="center"><img src="https://github.com/kwaldenphd/python-structured-data/blob/main/images/JSONSample.jpg?raw=true" width="500"></p>

JavaScript Object Notation (JSON) is as popular way to format data as a single (purportedly human-readable) string. JavaScript programs use JSON data structures, but we can frequently encounter JSON data outside of a JavaScript environment.

Websites that make machine-readable data available via an application programming interface (API- more on these in an upcoming lab) often provide that data in a JSON format. Examples include Twitter, Wikipedia, Data.gov, etc. Most live data connections available via an API are provided in a JSON format.

JSON structures can vary WIDELY depending on the specific data provider, but this lab will cover some basic elements of working with JSON in Python. The easiest way to think of JSON data as a plain-text data format made up of something like key-value pairs, like we've encountered previously in working with dictionaries (as a type of associative array).

Example JSON string: `stringOfJsonData = '{"name": Zophie", "isCat": true, "miceCaught": 0, "felineIQ": null}'`. From looking at the example string, we can see field names or keys (`name`, `isCat`, `miceCaught`, `felineIQ`) and values for those fields.

To use more precise terminology, JSON data has the following attributes:
- uses name/value pairs
- separates data using commas
- holds objects using curly braces `{}`
- holds arrays using square brackets `[]`

In our example `stringOfJsonData`, we have an object contained in curly braces. An object can include multiple name/value pairs. Multiple objects together can form an array.

How is data stored in a JSON format different than a `.csv`? 
- A `.csv` file uses characters as delimiters and has more of a tabular (table-like) structure.
- `.json` data uses characters as part of the syntax, but not in the same way as delimited data files. 
- The data stored in a JSON format has values that are attached to names (or keys).
  * NOTE: We can mimic this structure somewhat by loading a `.csv` as a dictionary data structure
- JSON can also have a hierarchical or nested structure, in that objects can be stored or nested inside other objects as part of the same array.

For example, take a look at sample JSON data from Twitter's API:

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

<blockquote>Q2: Decipher what we're seeing in the JSON here. What are some of the name/value pairs, and how are they organized in this object?</blockquote>

## Reading JSON into Python

We can read JSON into Python using the `json` module, which includes a few key functions for loading JSON data into Python:
- `json.loads()` takes a single string of JSON and loads it as a Python value
- `json.load()` takes a JSON file (or file-like object) and loads it as a Python value
- `json.dumps()` takes a Python value and transforms it to a JSON object.

<blockquote><a href="https://docs.python.org/3/library/json.html">Click here</a> to learn more about the <code>json</code> module.</blockquote>

Values stored in JSON format must be one of the following data types:
- string
- number
- object (JSON object)
- array
- boolean
- null

Translation table for how Python's `json` module interprets or renders these data types:

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

To translate a string of JSON data into a Python value, we pass it to the `loads()` function contained in the `json` module.

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

This block of code imports the `json` module, calls the `loads()` function and passes a string of JSON data to the `loads()` function. A few notes on this workflow:
- JSON strings always use double quotes, which is rendered in Python as a dictionary. Because Python dictionaries are not ordered, the order of the Python dictionary may not match the original JSON string order.
- In this example, we are loading a single string of JSON, which means we use the `json.loads()` function. When loading a JSON file (or file-like object), we would need to use the `json.load()` argument.

## Working with JSON in Python

Now that the JSON data is stored as a dictionary in Python, we can interact with it via the functionality avaialble via Python dictionaries. We could get all of the keys in the dictionary using the `keys()` method.

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

We could get all of the values in the dictionary using the `values()` method.

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

We could iterate by keys over the items in the dictionary.

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

We could also iterate over items in dictionary using key-value pairs.

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

We can read the value for a particular key using the index operator. The command `jsonDataAsPythonValue['name']` will return `Zophie`. 

In situations where JSON data includes nested or hierarchical objects and arrays, we will end up with a list of dictionaries in Python. For example, let's say we have a different JSON example and want to use more complex expressions in Python.

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

In this example, we loaded a single string of JSON, which means we use the `loads()` function. When loading a JSON file (or file-like object), we would need to use the `load()` argument.

For more on working with dictionaries in Python:
- [Elements of Computing I lab](https://github.com/kwaldenphd/python-next-steps/blob/main/part-i.md#dictionaries)
- [W3 Schools tutorial](https://www.w3schools.com/python/python_dictionaries.asp)

## Writing to JSON from Python

The `json` module's `dumps()` function will translate a Python dictionary into a string of JSON-formatted data.

```Python
# import json module
import json

# Python dictionary
pythonValue = {'isCat': True, 'miceCaught': 0, 'name': 'Zophie', 'felineIQ': None}

# translate Python value to JSON string
stringOfJsonData = json.dumps(pythonValue)

stringOfJsonData
```

We can also write data in a Python dictionary to a JSON file also using `dump()`.

```Python
# import json module
import json

# Python dictionary
pythonValue = {'isCat': True, 'miceCaught': 0, 'name': 'Zophie', 'felineIQ': None}

# create new JSON file and write dictionary to file
with open('output.json', 'w') as json_file:
	json.dump(pythonValue, json_file)
```

Later in the semester we will talk about how to read JSON data into Python and convert it to a tabular data structure (called a data frame in Python), using a library called `pandas`. Stay tuned!

## Application

Q3: Create a string of JSON data and write it to a JSON file. Answer to this question includes program + comments that document process and explain your code.

# `pandas`

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=1a39dca8-2d61-4f20-b6e8-af360144f447">Overview</a></td>
  </tr>
  </table>

<p align="center"><img src="https://github.com/kwaldenphd/pandas-intro/blob/main/images/Peebo.png?raw=true" width="1000"></p>

Some of you may be wondering why we are talking about pandas in a Computer Science course....

Panda: "a large black-and-white mammal (Ailuropoda melanoleuca) of chiefly central China that feeds primarily on bamboo shoots and is now usually classified with the bears (family Ursidae)" ([Merriam-Webster](https://www.merriam-webster.com/dictionary/panda))

Wait that's not right....

`pandas`: "a fast, powerful, flexible and easy to use open source data analysis and manipulation tool, built on top of the Python programming language" ([`pandas` documentation](https://pandas.pydata.org/))

That makes more sense.

There are limitations to the kinds of things we can do with structured data using the `csv` module. Particularly if we want to analyze and visualze structured data in a Python programming environment, we aren't going to get very far loading `csv` files as lists or dictionaries. We need Python to understand or interact with structured data as structured data.

Software developers at AQR Capital Management began working on a Python-based tool (written in a combination of C and Python) for quantitative data analysis in 2008. The initial open-source version of `pandas` was released in 2008.

At its core, "`pandas` is a software library written for the Python programming language for data manipulation and analysis. In particular, it offers data structures and operations for manipulating numerical tables and time series" ([Wikipedia](https://en.wikipedia.org/wiki/Pandas_(software)). The name `pandas` is derived from "panel data," an econometrics term used to describe particular types of datasets. The name `pandas` is also a play on "Python data analysis."

- For more on the history and origins of `pandas`, check out Wes McKinney's ["pandas: a Foundational Python Library for Data Analysis and Statistics"](https://www.dlr.de/sc/Portaldata/15/Resources/dokumente/pyhpc2011/submissions/pyhpc2011_submission_9.pdf) 2011 paper.

`pandas` is based on and has some similarities with another Python package, `NumPy`. According to [package documentation](https://numpy.org/doc/stable/user/whatisnumpy.html), "`NumPy` is the fundamental package for scientific computing in Python. It is a Python library that provides a multidimensional array object, various derived objects (such as masked arrays and matrices), and an assortment of routines for fast operations on arrays, including mathematical, logical, shape manipulation, sorting, selecting, I/O, discrete Fourier transforms, basic linear algebra, basic statistical operations, random simulation and much more."

In `NumPy`, data are stored as list-like objects called arrays. `NumPy` allows users to access, split, reshape, join, etc. data stored in arrays. `pandas` takes a similar approach to structured data, or data organized in a tabular (i.e. table-like) format. "pandas adopts significant parts of NumPy's idiomatic style of array-based computing, especially array-based functions and a preference for data processing without for loops...the biggest difference is that pandas is designed for working with tabular or heterogeneous data. NumPy, by contrast, is best suited for working with homogenous numerical array data" (Wes McKinney, Chapter 5 "Getting Started with Pandas" in *Python for Data Analysis*, pg. 125)

For more on `NumPy`:
- [NumPy website](https://numpy.org/)
- [NumPy documentation](https://numpy.org/doc/stable/)
- ["NumPy Introduction," W3Schools](https://www.w3schools.com/python/numpy_intro.asp)
- ["Introduction to NumPy Tutorial," Software Carpentry](https://software-carpentry.org/blog/2012/06/introduction-to-numpy-tutorial.html)

## Data Structures in `pandas`

<p align="center"><img src="https://github.com/kwaldenphd/pandas-intro/blob/main/images/series_df_diagram.png?raw=true" width="1000"></p>

`pandas` has two main data structures: `Series` and `DataFrame`.
- "A `Series` is a one-dimensional, array-like object containing a sequence of values...and an associated array of data labels, called its index" (McKinney, 126)
- A `DataFrame` includes a tabular data structure "and contains an ordered collection of columns, each of which can be a different value type" (McKinney, 130).

### `Series`

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=a6057ced-9dd1-426c-a063-af360146b0dd">Series</a></td>
  </tr>
  </table>

In `pandas`, "a `Series` is a one-dimensional, array-like object containing a sequence of values...and an associated array of data labels, called its index" (McKinney, 126). At first glance, a `Series` looks a lot like a Python list.

```Python
# import pandas package
import pandas as pd

# import Series and Data Frame components from pandas
from pandas import Series, DataFrame

# create a Series using pandas
obj = pd.Series([4, 7, -5, 3])

# show obj Series 
obj
```

A few notes on what's happening in this example:
- We imported the `pandas` package (using the `pd` alias) as well as the specific `Series` and `DataFrame` components.
- We created a `Series` object containing four integer values.

We could create a list with these values, but for data analysis we needed the functionality `pandas` provides for working with series. To verify `obj` is stored as an array-like object, we can use `pd.Series(obj).values` which should return `array([4, 7, -5, 3])`

We can also get the index attributes for `obj` using `pd.Series(obj).index`, which should return `RangeIndex(start=0, stop=4, step=1)`. The default index attributes assigned to objects in an array are integers `0` through `N-1`, where `N` is the length of the data. We can create our own index attributes for the data points by manually creating index labels.

```Python
# create obj2 series with index attributes
obj2 = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])

# show obj2 series
obj2
```

The index-value link lets us interact with a `Series` object similar to how we would work with Python dictionary key-value pairs.

```Python
# access Series value using index label
obj2['a'] 

# this returns -5
```

```Python
# assign value for index
obj2['d'] = 6

obj2['d']

# this returns 6, our newly-assigned value for index 'd'
```

```Python
# access multiple values in Series object using index
obj2[['c', 'a', 'd']]

# this returns the index-value pairs for the specified index labels
```

We can also use Python's built-in arithmetic functionality for values in a `Series` object. 

```Python
# select values in the Series that meet a specific condition
obj2[obj2 > 0]

# returns index-value pairs for values greater than 0
```

```Python
# multiply all values in Series
obj * 2

# returns modified values
```

```Python
# perform NumPy's exponent calculation functionality on Series values
np.exp(obj2)

# returns exponent float values
```

Try to perform similar mathematical operations on values stored in a Python dictionary or list and you'll run into all kinds of data type errors. The `Series` object uses a similar data structure and opens up a wide range of analysis possibilities.

To create a `Series` from data in a Python dictionary:

```Python
# create dictionary
sdata = {'Ohio': 35000, 'Texas': 71000, 'Oregon': 16000, 'Utah': 5000}

# create Series from dict dictionary
obj3 = pd.Series(sdata)
```

Let's say we wanted to have the `Series` values appear in a specific order. We can specify the index (or key) label order when converting a dictionary to a Series.

```Python
# create dictionary
sdata = {'Ohio': 35000, 'Texas': 71000, 'Oregon': 16000, 'Utah': 5000}

# list of index labels
states = ['California', 'Ohio', 'Oregon', 'Texas']

# create Series from dict dictionary
obj4 = pd.Series(sdata, index=states)

# see output for new obj4 series
obj4
```

A few things have happened here.
- The `California` index is returning `NaN` for its value, which is "not a number" or "NA".
- The `Utah` value in `sdata` is not in the `obj4` series, because the idex label `Utah` was not in the manually assigned list of index values passed to the series through `index=true`.

We can use the `isnull()` or `notnull()` functions in `pandas` to detect missing data. These functions will return `TRUE` or `FALSE`.

```Python
# test for null values for each index label
pd.isnull(obj4)

# output will be FALSE for all but California
```

```python
# test for not null values
pd.notnull(obj4)

# output will be TRUE for all but California
```

We can assign a name for our `Series` object and its index values using the `name` attribute.

```Python
# assign name to Series object
obj4.name = 'population'

# assign name to index
obj4.index.name = 'state'

# view updated Series
obj4
```

The output for `obj4` now reflects our newly-assigned `name` attribute values.

#### Application

Q4: Create your own `Series` object. Write code the accomplishes the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.
- Assign unique index attributes for each series value
- Access a series value(s) using the index label
- Perform at least two unique arithmetic operations on the Series
- Test for null values in your series

### `DataFrame`

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=96293510-c88d-4444-a8d0-af360146c587">DataFrame</a></td>
  </tr>
  </table>

While a `Series` object is a one-dimensional array, a `DataFrame` includes a tabular data structure "and contains an ordered collection of columns, each of which can be a different value type" (McKinney, 130). A `pandas` `DataFrame` has a row and column index--we can think of these as Series that all share the same index. Behold, a two-dimensional data structure!

In most situations, you'll create a `DataFrame` by reading in a structured data file. But we're going to manually create a `DataFrame` to better understand how they work in `pandas`. Let's go back to our state population data example. Say we have two dictionaries that include equal-length lists:

```Python
# create dictionary with three equal-length lists
data = {'state': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'], 
        'year': [2000, 2001, 2002, 2001, 2002, 2003],
        'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

# write data dictionary values to data frame
frame = pd.DataFrame(data)

# show newly-created frame
frame
```

Behold, a two-dimensional `DataFrame` object with rows, columns, labels, and values. The first object from each of the lists in our `data` dictionary now populate the first row of our `frame` DataFrame. This pattern continues for subsequent rows.

We can start to explore the dimensions or overall characteristics of our DataFrame:
```Python
# shows index labels and values for first 5 rows
frame.head(5)

# shows list of column labels
frame.columns.values

# shows basic statistical information for the data frame
frame.describe()
```

The last command `.describe()` returns some statistical information about values in our dataset, including:
- count
- mean
- standard deviation
- minimum
- 25th percentile
- 50th percentile
- 75th percentile
- maximum

Let's say we want to specify the column sequence or the order in which columns are arranged in the `DataFrame`:
```Python
pd.DataFrame(data, columns=['year', 'state', 'pop'])
```

What happens if we specify a column that isn't represented in the data passed to the `DataFrame`? 
```Python
# create new dataframe from data dictionary with specific columns and index labels
frame2 = pd.DataFrame(data, columns=['year', 'state', 'pop', 'debt'], index=['one', 'two', 'three', 'four', 'five', 'six'])

# show frame2 DataFrame
frame2
```

We see only `NaN` missing values for the `debt` column since that column is not represented in the `data` dictionary used to create our `frame2` DataFrame.

We can select columns in our `DataFrame` using their index labels.
```Python
frame2['state']

# returns state column
```

We can also select a column using the `name` attribute.
```Python
frame2.year

# returns year column
```

We can retrieve rows based on their position using the `loc` (location) attribute.
```Python
frame2.loc['three']

# returns the third row in the dataframe
```

```Python
frame2.iloc[0:3, :]

# uses numerical index values to retrieve first four rows
```

Let's say we wanted to manually assign the values in a particular column, for example the `debt` missing data column.
```Python
frame2['debt'] = 16.5

frame2

# returns frame2 DataFrame with newly-assigned 16.5 value for all rows in debt column
```

We could also manually insert values for specific rows using their index labels. If we wanted to add debt values for rows two, four, and five:

```Python
# variable with Series object
val = pd.Series([-1.2, -1.5, -1.7], index=['two', 'four', 'five'])

# assign val Series object to debt column in frame2 DataFrame
frame2['debt'] = val

# show modified DataFrame
frame2
```

We now see the modified `debt` values for the rows specified in the `index=` portion of our code.

We can remove a column using the `del` keyword.
```Python
del frame2['debt']

# returns updated list of columns
frame2.columns

# result will be 'year', 'state', and 'pop'
```

#### Application

Q5: Create your own small DataFrame. Write code that accomplishes the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.
- Change the original column order
- Select a specific column(s) using its index label or name attribute
- Select a specific row(s) using its index label or index value
- Remove a column from the DataFrame
- Determine summary statistics for values in the DataFrame

# From Data File to `DataFrame`

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=01168562-ebe4-4516-89ef-af3601451832">From Data File to DataFrame</a></td>
  </tr>
  </table>

It's far more likely that you will load structured data from a file into Python, rather than manually creating a `DataFrame`. For this section of the lab, we're going to work with data about *Titanic* passengers. Navigate to https://raw.githubusercontent.com/kwaldenphd/pandas-intro/main/data/titanic.csv in a web browser to see the dataset.

We can load structured data into Python from a file located on our computer or from a URL, using `pd.read_csv()`. An example of how we would load the `titanic.csv` file in Python as a `Pandas` DataFrame:

```Python
# import pandas
import pandas as pd

# load titanic data from csv file
# titanic = pd.read_csv("titanic.csv")

# load titanic data from url
titanic = pd.read_csv("https://raw.githubusercontent.com/kwaldenphd/pandas-intro/main/data/titanic.csv")

# show first 5 rows of newly-loaded dataframe
titanic.head(5)
```

`pandas` provides the `read_csv()` function which stores `.csv` data as a `pandas` `DataFrame`. This `read_` prefix can be used with other structured data file formats, as we'll explore with JSON later.

Other parsing functions in `pandas`:
- `read_fwf`: fixed-width data with no delimiter
- `read_clipboard`: reads in data from clipboard
- `read_excel`: reads in data from `.xls` or `.xlsx` files
- `read_html`: reads in any tables contained in an HTML document
- `read_json`: reads in JSON data
- `read_sql`: reads in results of an SQL query as a pandas dataframe
- `read_sas`: reads in SAS dataset
- `read_stata`: reads in Stata file format

To check the first and last five rows of the `titanic` data frame:
```Python
titanic
```

We can also check the data type for each column using `.dtypes`.
```Python
titanic.dtypes
```

From this output, we know we have integers (`int64`), floats (`float64`), and strings (`object`). Maybe we want a more technical summary of this `DataFrame`.

```Python
titanic.info()
```

`.info()` returns row numbers, the number of entries, column names, column data types, and the number of non-null values in each column. We can see from the `Non-Null Count` values that some columns do have null or missing values. `.info()` also tells us how much memory (RAM) is used to store this `DataFrame`.

## Application

Reuse your Q4 DataFrame, or load another data file as a DataFrame to use for this question.

Write code accomplishes each of the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.
- Shows the first five rows
- Shows the last five rows
- Checks the data types for each column
- Returns a technical summary for the DataFrame

## Other Data Loading Challenges

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=7947cc62-3264-43da-afe4-af360147f936">Other Data Loading Challenges</a></td>
  </tr>
  </table>

`pd.read_csv` includes other function arguments that can help with other common data formatting issues.

Argument | Description
--- | ---
`sep` or `delimiter` | Specifies the character sequence or regular expression used as a separator or delimiter
`header` | Specifies the row number to use as column names; `0` is default (does not need to be specified); `header=None` if no header
`index_col` | Specifies the column numbers or names to use as row index 
`names` | Specifies list of column names for result
`skiprows` | Row numbers (starting at 0) for rows to skip
`na_values` | Sequence of characters that represent missing or NA data
`comment` | Characters used to mark or split off comments that occur at end of lines of data
`parse_dates` | Specifies how date and time data will be parsed; `False` by default; `True` will attempt to parse all columns as `datetime` format; can also apply to select columns
`dayfirst` | Specifies international date format (DD/MM/YYYY); `False` by default
`date_parser` | Function used to parse dates
`nrows` | Number of rows to read starting at the beginning of the file; especially helpful when only needing part of a large file
`skipfooter` | Number of lines to ignore at the end of the file
`encoding` | Specifies encoding schema
`thousands` | Specifies `,` or `.` separater for thousands

Other elements of `.csv` dialect we might encounter when loading a file to a `DataFrame`:

Argument | Description
--- | ---
`na_values` | Values to recognize as `NA`/`NaN`. Can be a dictionary or list. 
`delimiter` | One character string used to separate fields; default is `,`
`quotechar` | Quote character for fields with specific characters or fields that inclde the delimiter character
`skippinitialspace` | Instructs program to ignore whitespace after delimiter; default is `False`
`doublequote` | Specifies how to handle quoting character within a field
`escapechar` | Specifies the string used to escape the delimiter character if `quoting` is set to `QUOTE_NONE`

[Link to the full [`pandas.read-csv()`](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html) documentation.

### Application

For the Q6 programs, you do not need to write code that actually loads an existing data file. That is, the lab does not provide data files that include these structures/attributes.

Write sample code that shows the syntax you would use to load a file with the structures/attributes described in the question.
- HINT: Be prepared to reference and consult the additional pd.read_csv function arguments listed in the previous lab section's tables.

Q6A: Write code that loads in a structured data file that uses a pipe symbol (|) as a delimiter. Include code + comments.
 
Q6B: Write code that loads in structured data file in which missing data values are represented by "?", "??", and "-" characters. Include code + comments.

Q6C: Write code that ignores the last 6 rows of a structured data file. Include code + comments.

Q6D: Write code that parses a structured data file in which commas "," are used as a thousands separator. Include code + comments

# Interacting with a `DataFrame`

## Sorting

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=480927f9-34c6-436d-8971-af360146f634">Sorting</a></td>
  </tr>
  </table>

`pandas` includes a few different built-in sorting operations. We can sort by an index for either axis of our `DataFrame` (i.e. we can sort based on row index labels or by column name). Going back to our Titanic passenger data, let's say we wanted to sort by passenger age.

```Python
# import pandas
import pandas as pd

# load titanic data from url
titanic = pd.read_csv("https://raw.githubusercontent.com/kwaldenphd/eda-pandas/main/data/titanic.csv")

# show first 5 rows of newly-loaded dataframe
titanic.head(5)

# sort by passenger age and show first five rows of the sorted data
titanic.sort_values(by="Age").head()
```

The default for `.sort_values` is to sort in ascending order. We can use `ascending=False` to sort in descending order.

```Python
titanic.sort_values(by=['Age'], ascending=False)
```

NOTE: When sorting, we are returning a sorted `DataFrame`. We ARE NOT updating the `DataFrame` in place. We have a couple of options to sort in place.

```Python
# create new dataframe with sorted results
titanic_by_age = titanic.sort_values(by="Age")

# check newly-created dataframe
titanic_by_age.head()
```

```
# sort values in place
titanic.sort_values(['Age'], inplace=True)

# check newly-created dataframe
titanic.head()
```

We can also sort by multiple fields. To sort by class cabin and age, in descending order:

```Python
titanic.sort_values(by=['Pclass', 'Age'], ascending=False).head()
```

When sorting by fields with string data, `a-z` is considered `ascending` and `z-a` would be `descending`.

## Subsetting

### Select

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=b2805333-207c-4cc2-9238-af360146fd12">Select</a></td>
  </tr>
  </table>

To review, we can select specific columns from a `DataFrame`. 
```Python
# creates Series object with age values
ages = titanic["Age"]

# show new object
ages
```

We can use `[" "]` to select a specific single column of interest. Python returns this single column's data as a `Series` object. We can also create a new data frame based on multiple columns.

```Python
# selects multiple columns to form new dataframe
age_sex = titanic[["Age", "Sex"]]

# checks first five rows of new dataframe
age_sex.head()
```

When selecting multiple columns, the inner brackets (`[]`) define the column names to subset or select. The outer brackets select data from a dataframe. In this multi-column example, `age_sex` is a `DataFrame` because it is a two-dimensional object.

For more on sorting operations in `pandas`, check out the package's ["Sorting" documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/basics.html#sorting).

### Filter

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=9570d7eb-5363-4bca-89ef-af360147074d">Filter</a></td>
  </tr>
  </table>

We can use Python's comparison operators to return rows in our `DataFrame` that meet specific conditions. Let's say we wanted to create a new `DataFrame` only containing data for passengers older than 35 years.

```Python
above_35 = titanic[titanic["Age"] > 35]

# check first five rows of newly-created dataframe
above_35.head()
```

We use brackets (`[]`) to set a condition rows must meet to be assigned to the new dataframe. If we just wanted to see whether rows meet this condition in the original `DataFrame`, we could just test for the condition without creating a new `DataFrame`.

```Python
titanic["Age"] > 35
```

Maybe we want to create a new data frame containing data on passegers in cabin class 2 and 3.
```Python
class_23 = titanic[titanic["Pclass"].isin([2, 3])]

# check first five rows of newly-created dataframe
class_23.head()
```

The `isin()` conditional function on its own would return a `True` or `False` value. By nesting the `isin()` function in brackets (`[]`), we are filtering rows based on rows  that meet the function critera, or return as `True` from this function.

We could also break out the chained or compound conditional statement using an `OR` operator, `|`.
```Python
class_23_alternate =  titanic[(titanic["Pclass"] == 2) | (titanic["Pclass"] == 3)]

class_23_alternate.head()
```

For more on Boolean indexing and the `isin()` function:
- ["Boolean indexing," Pandas documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#indexing-boolean)
- ["Indexing with isin," Pandas documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#indexing-basics-indexing-isin)

We could also create a new dataframe with passenger data for only passengers that have a known age.
```Python
age_known = titanic[titanic["Age"].notna()]

age_known.head()
```

`.notna()` is a conditional function that returns `True` for rows that do not have a `Null` value. For more on missing values and related functions, check out [the "Working with missing data" package documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/missing_data.html#missing-data).

### Selecting specific rows and columns

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=a2d95af5-1c38-427b-8251-af360147393c">Selecting Specific Rows & Columns</a></td>
  </tr>
  </table>

Selecting lets us isolate columns, and filtering identifies specific rows. But we can imagine a scenario in which we would want to combine these elements. We might want to create a new dataframe containing only the names of passengers who are over 35 years old.

```Python
over_35_names = titanic.loc[titanic["Age"] > 35, "Name"]

over_35_names
```

`.loc` identifies the rows we are writing to the new dataframe. What we are passing to the `loc` operator includes the row filter condition (`titanic["Age"] > 35`) and the column we are writing to the new dataframe (`Name`). 

We can also select rows and columns based on their index position. We could isolate rows 10-25 and columns 3-5 with the following expression:
```Python
titanic.iloc[9:25, 2:5]
```

We can also assign new values to our selection using `loc` or `iloc`. `loc` isolates rows based on their value, while `iloc` isolates rows based on their index position or label. Let's say we wanted to anonymize the first three names in the dataset. We could do this using `titanic.iloc[0:3, 3] = "anonymous"`.

Consult the ["Different choices for indexing"](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#indexing-choice) documentation for more on indexing options.

A few key takeaways:
- We use square brackets `[]` to subset data.
- We can specify single rows or columns, a list of rows/columns, or conditional expression within those brackets
- Select specific rows and/or columns using `loc` when working with row/column names
- Select specific rows and/or columns usign `iloc` when working with index positions
- You can assign new values to selection using `loc` or `iloc`

## From `DataFrame` to Data File

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=bbd847e6-f649-43fb-ad8c-af3601480776">Selecting From DataFrame to Data File</a></td>
  </tr>
  </table>

Let's say we have data in a `DataFrame` and want to write that to a file. While `.read_` loads data, `.to_` writes data. 

Let's say we want to save our filtered `DataFrame` as an Excel file.
```Python
df.to_excel("df.xlsx", sheet_name="data", index=False)
```

In this example, we create a new Excel file with a single sheet (`data`) that stores the data from our `df` `DataFrame`. `index=False` means that row index labels are not included in the new spreadsheet.

We could load back in the new Excel file and write it to a `.csv` file, dropping the header row:
```Python
# load Excel file as dataframe
df = pd.read_excel("df.xlsx", sheet_name="data")

# write dataframe to CSV file with no header
df.to_csv("df.csv", header=False, index=False)
```

## Application

Q7A: Using the DataFrame you created for Q5, write code that executes AT LEAST FOUR of the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.
- Sorts a column by ascending values
- Sorts a column by descending values
- Selects a specific column in the DataFrame
- Creates a new DataFrame with select columns from existing DataFrame
- Uses a comparison operator to filter rows in the DataFrame
- Uses an isin statement to filter rows in the DataFrame
- Selects specific rows and columns

Q7B: Write your modified `DataFrame` from Q7A to a `.csv` file. Your answer for these items should include a Python program + comments that document process and explain your code.

# Other `DataFrame` Tasks

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=71580603-99cd-46f6-bfa3-af360147553e">Other DataFrame Tasks</a></td>
  </tr>
  </table>

## Removing Duplicates

A useful place to start is identifying and removing any duplicate rows in a dataframe. We can do this using a few key functions. `.duplicated()` will return a `True` or `False` value indicating if a row is a duplicate of a previously occuring row.
```Python
data_frame.duplicated()
```

`.drop_duplicates()` will return a dataframe containing only rows that are not duplicated.
```Python
new_data_frame = old_data_frame.drop_duplicates()
```

## Handling Missing Data

As mentioned previously, we can specify how `pandas` handles missing values when working with a data frame object.

### `.dropna()`

We can use `.dropna()` to drop any row containing a missing value:
```Python
no_na = data_frame.dropna()
```

To drop any column containing a missing value, we can specify the axis:
```Python
no_na_columns = data_frame.dropna(axis=1, how='all')
```

### `.fillna()`

But we can imagine a scenario in which you don't want to filter out missing data. The `.fillna()` function will replace missing data with a specified value. The default function will replace all missing data in the dataframe:

```Python
# replaces all missing data with 0
df.fillna(0)
```

We can also specify a different missing fill value for specific columns using a dictionary.

```Python
# replace missing data in column 1 with 0.5 value and in column 2 with 0
df.fillna({1: 0.5, 2: 0})
```

In these examples, `.fillna()` returns a new object, but we can also modify the existing object in-place by setting `inplace` to `True`.
```Python
# modify existing object in-place
df.fillna(0, inplace=True)
```

We can also copy (or propogate) the last valid observation into missing data using specific methods that go along with `.fillna()`.
- Fill Forward (`ffill`) will take the "last known value" and apply it to missing data entries, until you hit the next non-null observation in the data frame.
- Back Fill (`bfill`) goes the other direction, starting from the last row in the dataset. The "last known value" is applied to missing data entries until you hit the next non-null observation.

To use forward fill on all missing values in a dataframe:
```Python
df.fillna(method='ffill')
```

To use back fill on all missing values in a dataframe:
```Python
df.fillna(method='bfill')
```

## Application

Q8A: Using the DataFrame you created for Q4 (or Q7), write code that executes AT LEAST ONE of the following tasks. Your answer for these items should include a Python program + comments that document process and explain your code.

- Removes duplicate rows
- Removes rows with missing values
- Fills missing values using .fillna, ffill, or bfill

Q8B: Write your modified `DataFrame` from Q8A to a `.csv` file. Your answer for these items should include a Python program + comments that document process and explain your code.

## How to submit this lab (and show your work)

Moving forward, we're going to be submitting lab notebooks using the provide Jupyter Notebook template.
- If working in JupyterLab (or another desktop IDE), download the `.ipynb` file to your local computer
  * `File` - `Download` - `Download as .ipynb`
- If working in Google Colaboratory, MAKE SURE you save a copy to your local drive. Otherwise your changes will not be saved.
  * `File` - `Save a copy in Drive`

The lab notebook template includes all of the questions as well as pre-created markdown cells for narrative text answers and pre-created code cells for any programs you may need to create. 
- Double click on these cells to edit and add your own content
- If questions do not require a code component, you can ignore those cells
- If questions to not require a narrative component, you can ignore those cells

If working in JupyterLab or another desktop IDE, upload the lab notebook template `.ipynb` file to Canvas as your lab submission.

If working in Google Colaboratory, submit the link to your notebook (checking sharing permissions, similar with Google Docs).

# Lab Notebook Questions

LAB NOTEBOOK TEMPLATE

Q1A: Open the `example.xlsx` file in a text editor. Describe what you see.

Q1B: How does your answer to Q1A compare to what you see when you open the `example.csv` file in a text editor?

Q1C: Open the `example.xlsx` file in a spreadsheet program. Save the file as a `.csv` format. What happens? Or what happens when you open the newly-created `.csv` file in a spreadsheet program or text editor?

Q2A: Create a small list data structure and write it to a CSV file. Answer to this question includes program + comments that document process and explain your code.

Q2B: Create a small dictionary and write it to a CSV file. Answer to this question includes program + comments that document process and explain your code.

Q3A: Navigate to an open data portal and download a `.csv` file. 

A few places to start:
- [Data.gov](https://www.data.gov/)
- [City of Chicago Data Portal](https://data.cityofchicago.org/)
- [City of South Bend Open Data](https://data-southbend.opendata.arcgis.com/)
- [Sports Reference](https://www.sports-reference.com/)

These open data portals are catalogs of datasets- you will need to explore the websites to identify and then download a specific dataset.

Open the data in a spreadsheet program and/or text editor. 
- What do you see?
- How can we start to make sense of the data based on available documentation?

Q3B: Write two programs that load the data in Python using the two different approaches highlighted in this lab:
- Lists and sublists
- Dictionaries

Answer to this question includes program + comments that document process and explain your code.

Q3C: What challenges did you encounter? How did you address or solve them? 

Q4: Modify the code provided below to load the example.txt file provided in this lab. Answer to this question includes program + comments that document process and explain your code.

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

Q5: Describe the concept of escape characters or quote characters in your own words. Describe a situation in which escape characters would be needed, and how you would address that challenge using Python syntax.

Q6: Decipher what we're seeing in the JSON here. What are some of the name/value pairs, and how are they organized in this object?

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

Q7: Create a string of JSON data and write it to a JSON file. Answer to this question includes program + comments that document process and explain your code.

Q8A: Navigate to an open data portal and download a JSON file. 

Some options that can get you started:
- [Data.gov](https://www.data.gov/)
- [City of Chicago Data Portal](https://data.cityofchicago.org/)
- [City of South Bend Open Data](https://data-southbend.opendata.arcgis.com/)

These open data portals are catalogs of datasets- you will need to explore the websites to identify and then download a specific dataset. Open the data in a spreadsheet program and/or text editor. Describe what are you seeing. How can we start to make sense of this data? What documentation is available?

Q8B: Write programs that accomplish the following tasks:
- Load the JSON data into Python
- Convert to a Python value

The previous sections of the lab procedure provide sample code and additional considerations for loading a JSON file in Python.
- NOTE: In the JSON example in the lab, we loaded a single string of JSON, which means we use the `loads()` function. When loading a JSON file (or file-like object), we would need to use the `load()` argument.

Answer to this question includes program + comments that document process and explain your code.

Q8C: What challenges did you encounter? How did you address or solve them? 
