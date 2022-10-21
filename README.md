# Structured Data & File I/O in Python

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>This tutorial was written by Katherine Walden and is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Overview & Goals

This lab provides an overview of fundamental programming concepts in the areas of file I/O and working with structured data, with a focus on Python syntax. Topics covered include:
- Delimited (`.csv`, `.tsv`) and name-value (`.json`, `.xml`) data structures
- Escape characters in relation to delimited data structures
- Working with delimited and name-value data structures in the Python programming environment, with a focus on the `csv` + `json` modules and `list` + `dictionary` data structures
- File I/O and file methods/access modes, with a focus on Python workflows

## Acknowledgements

Peer review and editing on the CSV portion of this lab was provided by Spring 2021 graduate teaching assistant [Aidan Draper](https://github.com/adraper2).

Peer review and editing on the JSON portion of this lab was provided by Spring 2021 graduate teaching assistant [Subhadyuti Sahoo](https://github.com/SDSAHOO703).

When building this lab, the author consulted the following materials:
- Al Sweigart [*Automate the Boring Stuff With Python*](https://nostarch.com/automatestuff2) (No Starch Press, 2020).
  * Chapter 16 "Working With CSV Files and JSON Data" (371-388)
- Wes McKinney, "Chapter 6.1, Reading and Writing Data in Text Format" in [*Python for Data Analysis*](https://www.oreilly.com/library/view/python-for-data/9781491957653/) (O'Reilly, 2017): 169-184.
- Wes McKinney, Chapter 6 "Data Loading, Storage, and File Formats" from [*Python for Data Analysis*](https://www.oreilly.com/library/view/python-for-data/9781491957653/) (O'Reilly, 2018): 169-193

# Table of Contents
- [Key Terms](#key-terms)
- [Lab Notebook Template](#lab-notebook-template)
- [Data](#data)
- [Overview](#overview)
- [File I/O](#file-io)
  * [Access Modes](#access-modes)
  * [File I/O in Python](#file-io-in-python)
- [Structured Data](#structured-data)
  * [Delimited Data](#delimited-data)
    * [CSV Files in Python](#csv-files-in-python)
    * [Delimiters & Escape Characters](#delimiters--escape-characters)
  * [JavaScript Object Notation](#javascript-object-notation)
- [Putting It All Together](#putting-it-all-together)
- [How to Submit This Lab (and show your work)](#how-to-submit-this-lab-and-show-your-work)
- [Lab Notebook Questions](#lab-notebook-questions)

[Click here](https://colab.research.google.com/drive/1V39jWVaHQUH07xlu8ADqHkrZDnFCWCTC?usp=sharing) to access this lab procedure as a Jupyter Notebook.

## Key Concepts

[Click here](https://github.com/kwaldenphd/python-structured-data/blob/main/key-concepts.md) for a full list of key concepts and definitions from this lab.

## Lab Notebook Template

[Click here](https://replit.com/team/eoc-f22/Structured-Data-and-File-IO-in-Python) to make a copy of the Replit template for this lab.

Lab notebook template:
- [`.py` file](https://drive.google.com/file/d/1ZlulPt8G57dZSvKgcmoZCF7x4uX5YjcD/view?usp=sharing)
- [Jupyter Notebook](https://colab.research.google.com/drive/1w6rrEM6I69TIdm-WpSDrEMgMC26bTzdj?usp=sharing)

## How to submit this lab (and show your work)

Moving forward, we'll submit lab notebooks as `.py` files. 

One option is to have a `.py` file that you use to run code and test programs while working through the lab. When ready to submit the lab notebook, you add comments and remove extraneous materials.

Another option is to have an "official" `.py` file that you are using as a lab notebook (separate from your working/testing file). Use comments in Python to note when you are starting a new question (as well as answering a question).
  * Example: `Lab_Notebook_Walden.py`

What gets submitted as the lab notebook is the `Lab_Notebook_Walden.py` file.
- When in doubt, use comments
- Be sure you are using comments to note what question you're responding to

## Data

You'll need four data files for this lab.
- `example.csv`
- `example.txt`
- `example.xlsx`
- `exampleWithHeader.csv`

These files are already loaded in the Replit project template for this lab.

You can also access them [via Google Drive](https://drive.google.com/drive/folders/1Sp_N34753ONJRU2AFKcocQ2DhCEhyL-m?usp=sharing) (ND users only).

# Overview

In programming languages and computing more broadly, `I/O` stands for `Input` and `Output`. 

We've seen `I/O` at work in previous labs, where we provided inputs to the computer (using a CPU simulator or working at the terminal), a task or operation was performed, and there was an endpoint or output for that process. A concrete example would be the assembly language program we wrote for Lab #2: How Comptuters Work (Hardware). We wrote assembly language instructions which served as inputs for the fetch-execute cycle, and the final output for the program was a data value stored in main memory.

Similarly, programming languages can take a variety of inputs (user-provided values, data, files, etc) and return outputs in a variety of formats (data stored in memory, output that shows up in the console, newly-created or -modified files, etc). We've seen `I/O` in action in previous labs, with Python's `print()` and `input()` functions.

In this lab, we're going to look at aspects of `I/O` that have to do with reading and writing files, with a focus on two key data structures:
- Tabular data, or data stored as a table consisting of rows and columns
- Data stored as name-value pairs, specifically in the JavaScript Object Notation (`.json`) format

# File I/O & Access Modes

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

## Comprehension Check

<table>
 <tr><td>
<img src="https://github.com/kwaldenphd/internet/blob/main/images/clipboard.png?raw=true" alt="Clipboard icon" width="50"/></td>
  <td><a href="https://docs.google.com/forms/d/e/1FAIpQLSettmkYgldWFwWb7taUc2aRVD7r5wHRwz_G9bQOE9KC8SgeiA/viewform?usp=sf_link">File I/O in Python Comprehension Check</a></td>
  </tr>
  </table>

What is NOT one of the core file handling tasks in programming language

Describe access modes

Correct syntax for opening an existing file

Correct syntax for creating a new file

Correct syntax for writing to a file

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

### Application

Q1A: Open the `example.xlsx` file in a text editor. Describe what you see.

Q1B: How does your answer to Q1A compare to what you see when you open the `example.csv` file in a text editor?

Q1C: Open the `example.xlsx` file in a spreadsheet program. Save the file as a `.csv` format. What happens? Or what happens when you open the newly-created `.csv` file in a spreadsheet program or text editor?

### `.csv` Files in Python

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

# Delimiters & Escape Characters 

But what happens if the values in your dataset include the same character that's being used as a delimiter? For example, let's say you have address data in the following structure:

Name | Age | Address
--- | --- | ---
Jerry | 10 | 2776 McDowell Street, Nashville, Tennessee
Tom | 20 | 3171 Jessie Street, Westerville, Ohio
Mike | 30 | 1818 Sherman Street, Hope, Kansas

In this example, we want to keep `Address` as an intact field and not separate based on the commas located within the address. In order to do this, we need to specify how the programming language parses fields that include the delimiter character.

In Python, the `quotechar` attribute in the `Dialect` class specifies what character will be used to enclose fields that should be treated as distinct entities and not be split into columns or fields based on the presence of the delimiter character within the field.

The default for `quotechar` is `"` (double quotation marks). So what does that mean? We put double quotation marks around the field that includes the delimiter character.

Modified data structure:

Name | Age | Address
--- | --- | ---
Jerry | 10 | "2776 McDowell Street, Nashville, Tennessee"
Tom | 20 | "3171 Jessie Street, Westerville, Ohio"
Mike | 30 | "1818 Sherman Street, Hope, Kansas"

Then we can read the modified data into Python using the workflows covered in previous sections of the lab.

But what happens if we have quotation marks within a field that needs to be treated as a distinct entity? For example, the following data structure would run into problems when read into Python.

Id | User | Comment
--- | --- | ---
1 | Bob | "John said "Hello World""
2 | Tom | ""The Magician""
3 | Harry | ""walk around the corner" she explained to the child"
4 | Louis | "He said, "stop pulling the dog's tail""

See our problem? The `Comment` field is enclosed with double quotation marks but also includes quotation marks in the field. We need the programming language to understand the enclosing double quotation marks serve a different purpose than the double quotation marks contained within the `Comment` field.

In Python, we can use a blackslash `\` character to escape the embedded double quotes.

Modified data structure:

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

Since the default for `quotechar` is `"`, we need to modify that default to reflect the new data structure.

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

## Application

Q4: Describe the concept of escape characters or quote characters in your own words. Describe a situation in which escape characters would be needed, and how you would address that challenge using Python syntax.

# JavaScript Object Notation

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

<blockquote>Q5: Decipher what we're seeing in the JSON here. What are some of the name/value pairs, and how are they organized in this object?</blockquote>

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
- [Elements of Computing I lab](https://github.com/kwaldenphd/python-data-structures#dictionaries)
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

Q6: Create a string of JSON data and write it to a JSON file. Answer to this question includes program + comments that document process and explain your code.

Q7A: Navigate to an open data portal and download a JSON file. 

Some options that can get you started:
- [Data.gov](https://www.data.gov/)
- [City of Chicago Data Portal](https://data.cityofchicago.org/)
- [City of South Bend Open Data](https://data-southbend.opendata.arcgis.com/)

These open data portals are catalogs of datasets- you will need to explore the websites to identify and then download a specific dataset. Open the data in a spreadsheet program and/or text editor. Describe what are you seeing. How can we start to make sense of this data? What documentation is available?

Q7B: Write programs that accomplish the following tasks:
- Load the JSON data into Python
- Convert to a Python value

The previous sections of the lab procedure provide sample code and additional considerations for loading a JSON file in Python.
- NOTE: In the JSON example in the lab, we loaded a single string of JSON, which means we use the `loads()` function. When loading a JSON file (or file-like object), we would need to use the `load()` argument.

Answer to this question includes program + comments that document process and explain your code.

Q7C: What challenges did you encounter? How did you address or solve them? 

## How to submit this lab (and show your work)

Moving forward, we'll submit lab notebooks as `.py` files. 

One option is to have a `.py` file that you use to run code and test programs while working through the lab. When ready to submit the lab notebook, you add comments and remove extraneous materials.

Another option is to have an "official" `.py` file that you are using as a lab notebook (separate from your working/testing file). Use comments in Python to note when you are starting a new question (as well as answering a question).
  * Example: `Lab_Notebook_Walden.py`

What gets submitted as the lab notebook is the `Lab_Notebook_Walden.py` file.
- When in doubt, use comments
- Be sure you are using comments to note what question you're responding to

# Lab Notebook Questions

[Click here](https://replit.com/team/eoc-f22/Structured-Data-and-File-IO-in-Python) to make a copy of the Replit template for this lab.

Lab notebook template:
- [`.py` file](https://drive.google.com/file/d/1ZlulPt8G57dZSvKgcmoZCF7x4uX5YjcD/view?usp=sharing)
- [Jupyter Notebook](https://colab.research.google.com/drive/1w6rrEM6I69TIdm-WpSDrEMgMC26bTzdj?usp=sharing)

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

Q4: Describe the concept of escape characters or quote characters in your own words. Describe a situation in which escape characters would be needed, and how you would address that challenge using Python syntax.

Q5: Decipher what we're seeing in the JSON here. What are some of the name/value pairs, and how are they organized in this object?

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

Q6: Create a string of JSON data and write it to a JSON file. Answer to this question includes program + comments that document process and explain your code.

Q7A: Navigate to an open data portal and download a JSON file. 

Some options that can get you started:
- [Data.gov](https://www.data.gov/)
- [City of Chicago Data Portal](https://data.cityofchicago.org/)
- [City of South Bend Open Data](https://data-southbend.opendata.arcgis.com/)

These open data portals are catalogs of datasets- you will need to explore the websites to identify and then download a specific dataset. Open the data in a spreadsheet program and/or text editor. Describe what are you seeing. How can we start to make sense of this data? What documentation is available?

Q7B: Write programs that accomplish the following tasks:
- Load the JSON data into Python
- Convert to a Python value

The previous sections of the lab procedure provide sample code and additional considerations for loading a JSON file in Python.
- NOTE: In the JSON example in the lab, we loaded a single string of JSON, which means we use the `loads()` function. When loading a JSON file (or file-like object), we would need to use the `load()` argument.

Answer to this question includes program + comments that document process and explain your code.

Q7C: What challenges did you encounter? How did you address or solve them? 
