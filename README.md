# Working With Structured Data in Python

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

This lab covers various methods for reading structured data into Python, focusing on `csv` and `json`. It covers other types of delimiters and escape characters. It also provides an overview of web APIs and how to construct an API call in Python. 

By the end of this lab, students will be able to:
- Describe the structure and components of a `.csv` file
- Read a `.csv` file into Python using the `csv` module and a `for` loop
- Understand how to approach other types of delimited files
- Understand how to work with escape characters when loading structured data
- Read a JSON file file into Python using the `json` module
- Describe the basic components and functionality of a web API
- Write a basic API call in Python
- Work with the results of an API call in Python
- Write the results of an API call to a JSON file

[Click here](https://raw.githubusercontent.com/kwaldenphd/python-structured-data/main/structured-data-python.ipynb) and select the "Save As" option to download this lab as a Jupyter Notebook.

[Link to lab overview video](https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=9833ffdf-c071-4aab-9ecc-acd1004ed991) (Panopto, ND Users)

## Acknowledgements

Information and exercises in this lab are adapted from:
- Al Sweigart [*Automate the Boring Stuff With Python*](https://nostarch.com/automatestuff2) (No Starch Press, 2020).
  * Chapter 13, "Working With Excel Spreadsheets" (302-328)
  * Chapter 16 "Working With CSV Files and JSON Data" (371-388)
- Wes McKinney, "Chapter 6.1, Reading and Writing Data in Text Format" in [*Python for Data Analysis*](https://www.oreilly.com/library/view/python-for-data/9781491957653/) (O'Reilly, 2017): 169-184.
- Charles Severance, "Chapter 13, Using Web Services" in [*Python for Everybody*](https://www.py4e.com/book.php) (Charles Severance, 2009): 155-170.
- Eric Matthes, Chapter 17 "Working With APIs" from [*Python Crash Course*](https://nostarch.com/pythoncrashcourse2e) (No Starch Press, 2019): 359-375
- Charles Severance, Chapter 13 "Using Web Services" from [*Python for Informatics*](https://www.py4e.com/book.php) (2009): 155-168
- Wes McKinney, Chapter 6 "Data Loading, Storage, and File Formats" from [*Python for Data Analysis*](https://www.oreilly.com/library/view/python-for-data/9781491957653/) (O'Reilly, 2018): 169-193
- Patrick Smyth, "Creating Web APIs with Python and Flask," *The Programming Historian* 7 (2018), https://doi.org/10.46430/phen0072.
- Ritvik Kharkar, ["Getting Census Data in 5 Easy Steps"](https://towardsdatascience.com/getting-census-data-in-5-easy-steps-a08eeb63995d) *Towards Data Science* (29 April 2019).


# Table of Contents
- [Data](#data)
- [CSV](#csv-data-in-python)
  * [What is a `.csv` file?](#what-is-a-csv-file)
  * [Reading a `.csv` file into Python](#reading-a-csv-file-into-Python)
    * [Reading `.csv` data using a `for` loop](#reading-csv-data-using-a-for-loop)
  * [Other delimiters](#other-delimiters)
  * [Escape characters](#escape-characters)
  * [Reading in `.csv` files using dictionaries](#reading-in-csv-files-using-dictionaries)
  * [CSV Project Prompt](#csv-project-prompt)
- [JSON](#json)
  * [What is JSON and why are we learning about it](#what-is-json-and-why-are-we-learning-about-it)
  * [Reading JSON into Python](#reading-json-into-python)
  * [Working with JSON in Python](#working-with-json-in-python)
  * [Writing to JSON from Python](#writing-to-json-from-python)
  * [JSON Project Prompt](#json-project-prompt)
- [APIs](#what-are-apis-and-how-do-they-work)
  * [API terminology](#api-terminology)
  * [What can data from an API look like](#what-can-data-from-an-api-look-like)
  * [Making an API call in Python](#making-an-api-call-in-python)
  * [Working with the API response in Python](#working-with-the-api-response-in-python)
  * [Writing an API response to a JSON file](#writing-an-api-response-to-a-json-file)
  * [Example: U.S. Census Bureau Data](#example-us-census-bureau-data)
  * [API Project Prompt](#api-project-prompt)
- [Lab notebook questions](#lab-notebook-questions)

# Data

You'll need four data files for this lab.
- `example.csv`
- `example.txt`
- `example.xlsx`
- `exampleWithHeader.csv`

You can download the files from this GitHub repository as individual files or a zip folder.

You can also access them [via Google Drive](https://drive.google.com/drive/folders/1Sp_N34753ONJRU2AFKcocQ2DhCEhyL-m?usp=sharing) (ND users only).

# `.csv` data in Python

## What is a `.csv` file? 

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

## Reading a `.csv` file into Python

10. To read data from a `.csv` file into Python, we will use the `csv` module.

<blockquote>Check out <a href = "https://docs.python.org/3/library/csv.html#module-csv">Python's documentation</a> to learn more about the <code>csv</code> module.</blockquote>

11. The `csv` module allows us to create a `reader` object that iterates over lines in a `.csv` file.

12. What does this workflow look like? 
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

13. You'll notice that the `exampleData` output is a list of lists, or a list that contains sub-lists. 

14. Each row of data from the original `example.csv` file is a sub-list (with field values separated by commas) within the `exampleData` list.

15. Now we can access the value at a particular row and column using the expression `exampleData[row][col]`, where `row` is the index position of one of the lists in `exampleData`, and `col` is the index position of the item located in that list.

16. For example, `exampleData[0][0]` would give us the first string from the first list. `exampleData[0][1]` would give us the second string from the first list.

## Reading `.csv` data using a `for` loop

17. The method we just used to read data from a `.csv` file into Python loads the entire file into memory at once.

18. If we use this method on a large `.csv` file, Python is going to try to load the entire file into memory at once. Which does not bode well for Python or your computer's performance.

19. We can use a `reader` object as part of a `for` loop to iterate through the lines in a `.csv` file and load the file line-by-line.

<blockquote>Remember <code>for</code> loops iterate through each item in a series or list of items and performs the content of the loop on each item.</blockquote>

20. What does this workflow look like?
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

21. This program imports the `csv` module, makes a `reader` object from the `example.csv` file, and loops through each of the rows in the `reader` object.

22. Each row is a list of values, and each value represents a cell.

23. The `print()` function prints the current row number and that row's contents. 

24. The `reader` object includes a `line_num` variable, which contains the number of the current line.

25. NOTE: The `reader` object can only be looped over once. If you need to re-read the same `.csv` file, you'll use `csv.reader` to create a new `reader` object.

## Other delimiters

26. But what happens if you need to load in structured data that uses another delimiter, not a comma? 

27. Remember when we opened a `.csv` file in a plain-text editor, the value fields are separated by a comma.

28. But commas are not the only possible delimiter. Tabs, spaces, pipes, or other characters can be used to separate or delimit fields in a dataset.

29. The `csv` module includes a range of formatting parameters, known as a `Dialect` class. 

30. The `Dialect` class includes a range of methods you can use to specify alternate delimiters and (as we'll discover shortly), handle situations like special characters, line breaks, etc.

31. The `delimiter` attribute in the `Dialect` class lets us specify what delimiter is being used in the data we want to load.
```Python
# import csv module
import csv

# load tab-separated value file
tsv_file = open('example.txt')

# create a reader object and specify the new delimiter
read_tsv = csv.reader(tsv_file, delimiter="\t")

# use a for loop to read in the data
for row in read_tsv:
  print(row)
```

<blockquote>Q4: Modify the code provided above to load the example.txt file.</blockquote>

## Escape characters

32. But what happens if the values in your dataset include the same character that's being used as a delimiter?

33. For example, let's say you have address data in the following structure:

Name | Age | Address
--- | --- | ---
Jerry | 10 | 2776 McDowell Street, Nashville, Tennessee
Tom | 20 | 3171 Jessie Street, Westerville, Ohio
Mike | 30 | 1818 Sherman Street, Hope, Kansas

34. In this example, we want to keep `Address` as an intact field and not separate based on the commas located within the address.

35. In order to do this, we need to specify how Python parses fields that include the delimiter character.

36. The `quotechar` attribute in the `Dialect` class specifies what character will be used to enclose fields that should be treated as distinct entities and not be split into columns or fields based on the presence of the delimiter character within the field.

37. The default for `quotechar` is `"` (double quotation marks).

38. So what does that mean? We put double quotation marks around the field that includes the delimiter character.

39. Modified data structure:

Name | Age | Address
--- | --- | ---
Jerry | 10 | "2776 McDowell Street, Nashville, Tennessee"
Tom | 20 | "3171 Jessie Street, Westerville, Ohio"
Mike | 30 | "1818 Sherman Street, Hope, Kansas"

40. Then we can read the modified data into Python.

41. But what happens if we have quotation marks within a field that needs to be treated as a distinct entity?

42. For example, the following data structure would run into problems when read into Python.

Id | User | Comment
--- | --- | ---
1 | Bob | "John said "Hello World""
2 | Tom | ""The Magician""
3 | Harry | ""walk around the corner" she explained to the child"
4 | Louis | "He said, "stop pulling the dog's tail""

43. See our problem? The `Comment` field is enclosed with double quotation marks but also includes quotation marks in the field. 

44. We need Python to understand the enclosing double quotation marks serve a different purpose than the double quotation marks contained within the `Comment` field.

45. We can use a blackslash `\` character to escape the embedded double quotes.

46. Modified data structure:

Id | User | Comment
--- | --- | ---
1 | Bob | "John said \"Hello World\""
2 | Tom | "\"The Magician\""
3 | Harry | "\"walk around the corner\" she explained to the child"
4 | Louis | "He said, \"stop pulling the dog's tail\""

47. Since the default for `quotechar` is `"`, we need to modify that default to reflect the new data structure.
```Python
# import csv module
import csv

# read csv using quote quotechar
with open('data.csv', 'rt') as f:
  csv_reader = csv.reader(f, skipinitialspace=True, quotechar='\\')
  
  for line in csv_reader:
    print(line)
```

<blockquote>Q5: Define escape characters in your own words. Describe a situation in which escape characters would be needed, and how you would address that challenge using Python syntax.</blockquote>
  
# Reading in `.csv` files using dictionaries

48. For `.csv` files that contain header rows, we might want to connect the header row values with subsequent row values.

49. We can do this by reading the `.csv` file as a dictionary, rather than a list containing row sub-lists.

50. Remember dictionaries have key-value pairs, where we can access a value by using its key name.

51. For tabular data, we can think of the key as the field name contained in the header row and the value as column or field values.

52. We read a `.csv` file to a dictionary using a `DictReader` object (versus the `csv.reader` object).
```Python
# import csv module
import csv

# open csv file
exampleFile = open('exampleWithHeader.csv')

# reading exampleFile to a dictionary
exampleDictReader = csv.DictReader(exampleFile)

# set keys for key-value pairs
for row in exampleDictReader:
  print(row['Timestamp'], row['Fruit'], row['Quantity'])
```

53. Within the `for` loop, the `DictReader` object sets `row` to a dictionary object with keys derived from the headers in the first row.

54. The `DictReader` object means we don't have to separate the header information from the rest of the data contained in the file, because the `DictReader` object does this for us.

55. But what can we do if we want to read to a dictionary a `.csv` file that doesn't incldue a header row?

56. We can pass a second argument to the `DictReader()` function to manually set header names.
```Python
# import csv module
import csv

# open csv file
exampleFile = open('example.csv')

# reading exampleFile to a dictionary with added field names
exampleDictReader = csv.DictReader(exampleFile, ['time', 'name', 'amount'])

# set keys for key-value pairs
for row in exampleDictReader:
  print(row['Timestamp'], row['Fruit'], row['Quantity'])
```

<blockquote>Q6: Describe in your own words how csv_DictReader interacts with structured data.</blockquote>

# Writing to a `.csv` file

57. We'll do more with writing to a `.csv` file later in the semester.

58. But for now, we can create a `writer` object using the `csv.writer()` function to write data to a `.csv` file.
```Python
# import csv module
import csv

# create and open output.csv file in write mode
outputFile = open('output.csv', 'w', newline='')

# create writer object
outputWriter = csv.writer(outputFile)

# write first row
outputWriter.writerow(['spam', 'eggs', 'bacon', 'ham'])

# write another row
outputWriter.writerow(['Hello, world!', 'eggs', 'bacon', 'ham'])

# write a third row
outputWriter.writerow(['1, 2, 3.141592, 4])

# close the output file
outputFile.close()
```

59. The `writerow()` method takes a list argument and writes that to a new row in the `writer` object, that is added to the `.csv` file.

## Writing from a dictionary to a `.csv` file

60. We can use the `DictWriter` object to write data in a dictionary to a `.csv` file.
```Python
# import csv module
import csv

# create and open output.csv file in write mode
outputFile = open('output.csv', 'w', newline='')

# create writer object
outputDictWriter = csv.Dictwriter(outputFile, ['Name', 'Pet', 'Phone'])

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

61. Note that the order of the key-value pairs in the dictionaries created manually using `writerow()` doesn't matter.

62. Python writes the dictionaries to the `.csv` file using the order of the keys given to `DictWriter()`.

63. Missing keys will be empty in the newly-created `.csv` file.

<blockquote>Q7: Create a small dictionary and write it to a CSV file. Include code + comments.</blockquote>

## CSV Project Prompt

Navigate to an open data portal and download a `.csv` or `.xlsx` file. 

A few places to start:
- [Data.gov](https://www.data.gov/)
- [City of Chicago Data Portal](https://data.cityofchicago.org/)
- [City of South Bend Open Data](https://data-southbend.opendata.arcgis.com/)
- [Sports Reference](https://www.sports-reference.com/)

Open the data in a spreadsheet program and/or text editor
- What do you see?
- How can we start to make sense of the data based on available documentation?

Load the data in Python as list/sublists and as dictionary. What challenges did you encounter? How did you address or solve them? 

# JSON

## What is JSON and why are we learning about it

64. JavaScript Object Notation (JSON) is as popular way to format data as a single (purportedly human-readable) string. 

65. JavaScript programs use JSON data structures, but we can frequently encounter JSON data outside of a JavaScript environment.

66. Websites that make machine-readable data available via an application programming interface (API- more on these in an upcoming lab) often provide that data in a JSON format. Examples include Twitter, Wikipedia, Data.gov, etc. Most live data connections available via an API are provided in a JSON format.

67. JSON structure can vary WIDELY depending on the specific data provider, but this lab will cover some basic elements of working with JSON in Python.

68. The easiest way to think of JSON data as a plain-text data format made up of something like key-value pairs, like we've encountered previously in working with dictionaries.

69. Example JSON string: `stringOfJsonData = '{"name": Zophie", "isCat": true, "miceCaught": 0, "felineIQ": null}'`

70. From looking at the example string, we can see field names or keys (`name`, `isCat`, `miceCaught`, `felineIQ`) and values for those fields.

71. To use more precise terminology, JSON data has the following attributes:
- uses name/value pairs
- separates data using commas
- holds objects using curly braces `{}`
- holds arrays using square brackets `[]`

72. In our example `stringOfJsonData`, we have an object contained in curly braces. 

73. An object can include multiple name/value pairs. Multiple objects together can form an array.

74. Values stored in JSON format must be one of the following data types:
- string
- number
- object (JSON object)
- array
- boolean
- null

75. How is data stored in a JSON format different than a CSV? 

76. A `.csv` file uses characters as delimiters and has more of a tabular (table-like) structure.

77. JSON data uses characters as part of the syntax, but not in the same way as delimited data files. 

78. Additionally, the data stored in a JSON format has values that are attached to names (or keys).

79. JSON can also have a hierarchical or nested structure, in that objects can be stored or nested inside other objects as part of the same array.

80. For example, take a look at sapmle JSON data from Twitter's API:
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

<blockquote>Q8: Decipher what we're seeing in the JSON here. What are the name/value pairs, and how are they organized in this object?</blockquote>

## Reading JSON into Python

81. We can read JSON into Python using the `json` module.

<blockquote><a href="https://docs.python.org/3/library/json.html">Click here</a> to learn more about the <code>json</code> module.</blockquote>

82. The `json.loads()` and `json.dumps()` functions translate JSON data and Python values.

83. Translation table:

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

84. To translate a string of JSON data into a Python value, we pass it to the `json.loads()` function.
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

85. This block of code imports the `json` module, calls the `loads()` function and passes a string of JSON data to the `loads()` function.

86. NOTE: JSON strings always use double quotes, which is rendered in Python as a dictionary. Because Python dictionaries are not ordered, the order of the Python dictionary may not match the original JSON string order.

## Working with JSON in Python

87. Now that the JSON data is stored as a dictionary in Python, we can interact with it via the functionality avaialble via Python dictionaries.

88. We could get all of the keys in the dictionary using the `keys()` method.
```Python
# import json module
import json

# string of JSON data
stringOfJsonData = '{"name": "Zophie", "isCat": true, "miceCaught": 0, "felineIQ": null}'

# load JSON data as Python value 
jsonDataAsPythonValue = json.loads(stringOfJsonData)

# print list of keys
print(jsonDataAsPython.keys())
```

89. We could get all of the values in the dictionary using the `values()` method.
```Python
# import json module
import json

# string of JSON data
stringOfJsonData = '{"name": "Zophie", "isCat": true, "miceCaught": 0, "felineIQ": null}'

# load JSON data as Python value 
jsonDataAsPythonValue = json.loads(stringOfJsonData)

# print list of values
print(jsonDataAsPython.values())
```

90. We could iterate by keys over the items in the dictionary.
```Python
# import json module
import json

# string of JSON data
stringOfJsonData = '{"name": "Zophie", "isCat": true, "miceCaught": 0, "felineIQ": null}'

# load JSON data as Python value 
jsonDataAsPythonValue = json.loads(stringOfJsonData)

# iterate by keys using for loop
for key in jsonDataAsPython.keys():
  print(key, jsonDataAsPython[key])
```

91. We could also iterate over items in dictionary using key-value pairs.
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

92. We can read the value for a particular key using the index operator. The command `jsonDataAsPythonValue['name']` will return `Zophie`.

93. In situations where JSON data includes nested or hierarchical objects and arrays, we will end up with a list of dictionaries in Python.

94. For example, let's say we have a different JSON example and want to use more complex expressions in Python.
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

95. For more on working with dictionaries in Python:
- [Elements of Computing I lab](https://github.com/kwaldenphd/python-lab6/blob/master/README.md#working-with-dictionaries)
- [W3 Schools tutorial](https://www.w3schools.com/python/python_dictionaries.asp)

## Writing to JSON from Python

96. The `json.dumps()` function will translate a Python dictionary into a string of JSON-formatted data.
```Python
# import json module
import json

# Python dictionary
pythonValue = {'isCat': True, 'miceCaught': 0, 'name': 'Zophie', 'felineIQ': None}

# translate Python value to JSON string
stringOfJsonData = json.dumps(pythonValue)

stringOfJsonData
```

97. We can also write data in a Python dictionary to a JSON file also using `json.dump()`.
```Python
# import json module
import json

# Python dictionary
pythonValue = {'isCat': True, 'miceCaught': 0, 'name': 'Zophie', 'felineIQ': None}

# create new JSON file and write dictionary to file
with open('output.json', 'w') as json_file:
	json.dump(pythonValue, json_file)
```

98. Later in the semester we will talk about how to read JSON data into Python and convert it to a tabular data structure (called a data frame in Python), using a library called `pandas`. Stay tuned!

## JSON Project Prompt

Navigate to an open data portal and download a JSON file. 

Some options that can get you started:
- [Data.gov](https://www.data.gov/)
- [City of Chicago Data Portal](https://data.cityofchicago.org/)
- [City of South Bend Open Data](https://data-southbend.opendata.arcgis.com/)

Open the data in a spreadsheet program and/or text editor 

Describe what are you seeing. How can we start to make senes of this data? What documentation is available?

Read the JSON data into Python and convert to a Python value.

# What are APIs and how do they work

99. For a brief introduction to APIS, view Danielle Thé, ["API's Explained (with LEGO)"](https://youtu.be/qW1qhb8r8xI), *YouTube Video* (1 November 2016).

<p align="center"><a href="https://github.com/kwaldenphd/apis-python/blob/main/Figure_1.jpg?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/apis-python/blob/main/Figure_1.jpg?raw=true" /></a></p>

100. There are many different kinds of Application Programming Interfaces (APIs). In general, an API is the part of a computer program designed to be used or manipulated by another computer program. 

101. We can contrast this with interacting with a computer program via the user interface, which most often is a type of graphical user interface (GUI).

102. We're focusing on web APIs, which allow for information or functionality to be manipulated by other programs via the internet. 

103. For example, with Twitter’s web API, you can write a Python program to perform tasks such as favoriting tweets or collecting tweet metadata.

104. Other large-scale data repositories tend to make data available via an API.

105. For example, the U.S. National Archives and Records Administration (NARA) makes the National Archives catalog, Executive Orders, and photographic image content available [via an API](https://www.archives.gov/developer#toc--datasets).

107. The Smithsonian Institution allows open access to museum collection metadata [via an API](https://www.si.edu/openaccess/devtools).

108. The U.S. Library of Congress provides access to digital collection metadata, digitized historical newspaper images, public radio and television programs, and World Digital Library collections [via APIs](https://labs.loc.gov/lc-for-robots/). 

109. The U.S. Census Bureau makes as wide range of public data available [via API](https://www.census.gov/data/developers/data-sets.html).

110. APIs let us bring a live data connection into a programming environment and interact or work with it based on the format and protocols established as part of the API.

111. So we can imagine a scenario in which you wanted to build an application or visualization based on the location of [Iowa Department of Transportation's nearly 901 snow plows](https://iowadot.gov/tap.html).

112. Downloading a static dataset isn't going to work for this specific use case--you need a live data feed with up-to-date information.

113. Thus the beauty of APIs.
- [Link to IDOT's plow truck data](https://data.iowadot.gov/datasets/20a0c10c06a54240b5f2893e0187e22c_0?orderBy=OBJECTID&orderByAsc=false&page=6)

## API terminology

114. Some terminology that goes along with APIs.
- ***HTTP (HyperText Transfer Protocol)***: primary means of communicating or transferring data on the world wide web. 
- ***URL (Uniform Resource Locator)***: an address or location information for information on the web. A URL describes the location of a specific resource.
- ***JSON (JavaScript Object Notation)***: plain-text data storage format
- ***REST (REpresentational State Transfer)***: best practices for implementing APIs. APIs that follow these principles are called REST APIs.

## What can data from an API look like?

115. Navigate to https://api.github.com/search/repositories?q=language:python&sort=stars in a web browser.

116. We're looking at public projects hosted on GitHub that are written in the Python programming language.

117. Select the option to Expand All items, or click on the drop-down arrows to expand the data at this URL.
```JSON
{
  "total_count": 6343245,
  "incomplete_results": true,
  "items": [
    {
      "id": 123458551,
      "node_id": "MDEwOlJlcG9zaXRvcnkxMjM0NTg1NTE=",
      "name": "Python-100-Days",
      "full_name": "jackfrued/Python-100-Days",
      "private": false,
      "owner": {
        "login": "jackfrued",
        "id": 7474657,
        "node_id": "MDQ6VXNlcjc0NzQ2NTc=",
        "avatar_url": "https://avatars0.githubusercontent.com/u/7474657?v=4",
        "gravatar_id": "",
        "url": "https://api.github.com/users/jackfrued",
        "html_url": "https://github.com/jackfrued",
        "followers_url": "https://api.github.com/users/jackfrued/followers",
        "following_url": "https://api.github.com/users/jackfrued/following{/other_user}",
        "gists_url": "https://api.github.com/users/jackfrued/gists{/gist_id}",
        "starred_url": "https://api.github.com/users/jackfrued/starred{/owner}{/repo}",
        "subscriptions_url": "https://api.github.com/users/jackfrued/subscriptions",
        "organizations_url": "https://api.github.com/users/jackfrued/orgs",
        "repos_url": "https://api.github.com/users/jackfrued/repos",
        "events_url": "https://api.github.com/users/jackfrued/events{/privacy}",
        "received_events_url": "https://api.github.com/users/jackfrued/received_events",
        "type": "User",
        "site_admin": false
      },
      "html_url": "https://github.com/jackfrued/Python-100-Days",
      "description": "Python - 100天从新手到大师",
      "fork": false,
      "url": "https://api.github.com/repos/jackfrued/Python-100-Days",
      "forks_url": "https://api.github.com/repos/jackfrued/Python-100-Days/forks",
      "keys_url": "https://api.github.com/repos/jackfrued/Python-100-Days/keys{/key_id}",
      "collaborators_url": "https://api.github.com/repos/jackfrued/Python-100-Days/collaborators{/collaborator}",
      "teams_url": "https://api.github.com/repos/jackfrued/Python-100-Days/teams",
      "hooks_url": "https://api.github.com/repos/jackfrued/Python-100-Days/hooks",
      "issue_events_url": "https://api.github.com/repos/jackfrued/Python-100-Days/issues/events{/number}",
      "events_url": "https://api.github.com/repos/jackfrued/Python-100-Days/events",
      "assignees_url": "https://api.github.com/repos/jackfrued/Python-100-Days/assignees{/user}",
      "branches_url": "https://api.github.com/repos/jackfrued/Python-100-Days/branches{/branch}",
      "tags_url": "https://api.github.com/repos/jackfrued/Python-100-Days/tags",
      "blobs_url": "https://api.github.com/repos/jackfrued/Python-100-Days/git/blobs{/sha}",
      "git_tags_url": "https://api.github.com/repos/jackfrued/Python-100-Days/git/tags{/sha}",
      "git_refs_url": "https://api.github.com/repos/jackfrued/Python-100-Days/git/refs{/sha}",
      "trees_url": "https://api.github.com/repos/jackfrued/Python-100-Days/git/trees{/sha}",
      "statuses_url": "https://api.github.com/repos/jackfrued/Python-100-Days/statuses/{sha}",
      "languages_url": "https://api.github.com/repos/jackfrued/Python-100-Days/languages",
      "stargazers_url": "https://api.github.com/repos/jackfrued/Python-100-Days/stargazers",
      "contributors_url": "https://api.github.com/repos/jackfrued/Python-100-Days/contributors",
      "subscribers_url": "https://api.github.com/repos/jackfrued/Python-100-Days/subscribers",
      "subscription_url": "https://api.github.com/repos/jackfrued/Python-100-Days/subscription",
      "commits_url": "https://api.github.com/repos/jackfrued/Python-100-Days/commits{/sha}",
      "git_commits_url": "https://api.github.com/repos/jackfrued/Python-100-Days/git/commits{/sha}",
      "comments_url": "https://api.github.com/repos/jackfrued/Python-100-Days/comments{/number}",
      "issue_comment_url": "https://api.github.com/repos/jackfrued/Python-100-Days/issues/comments{/number}",
      "contents_url": "https://api.github.com/repos/jackfrued/Python-100-Days/contents/{+path}",
      "compare_url": "https://api.github.com/repos/jackfrued/Python-100-Days/compare/{base}...{head}",
      "merges_url": "https://api.github.com/repos/jackfrued/Python-100-Days/merges",
      "archive_url": "https://api.github.com/repos/jackfrued/Python-100-Days/{archive_format}{/ref}",
      "downloads_url": "https://api.github.com/repos/jackfrued/Python-100-Days/downloads",
      "issues_url": "https://api.github.com/repos/jackfrued/Python-100-Days/issues{/number}",
      "pulls_url": "https://api.github.com/repos/jackfrued/Python-100-Days/pulls{/number}",
      "milestones_url": "https://api.github.com/repos/jackfrued/Python-100-Days/milestones{/number}",
      "notifications_url": "https://api.github.com/repos/jackfrued/Python-100-Days/notifications{?since,all,participating}",
      "labels_url": "https://api.github.com/repos/jackfrued/Python-100-Days/labels{/name}",
      "releases_url": "https://api.github.com/repos/jackfrued/Python-100-Days/releases{/id}",
      "deployments_url": "https://api.github.com/repos/jackfrued/Python-100-Days/deployments",
      "created_at": "2018-03-01T16:05:52Z",
      "updated_at": "2020-12-16T16:09:01Z",
      "pushed_at": "2020-12-16T03:01:52Z",
      "git_url": "git://github.com/jackfrued/Python-100-Days.git",
      "ssh_url": "git@github.com:jackfrued/Python-100-Days.git",
      "clone_url": "https://github.com/jackfrued/Python-100-Days.git",
      "svn_url": "https://github.com/jackfrued/Python-100-Days",
      "homepage": "",
      "size": 272084,
      "stargazers_count": 97101,
      "watchers_count": 97101,
      "language": "Python",
      "has_issues": true,
      "has_projects": true,
      "has_downloads": true,
      "has_wiki": true,
      "has_pages": false,
      "forks_count": 38952,
      "mirror_url": null,
      "archived": false,
      "disabled": false,
      "open_issues_count": 513,
      "license": null,
      "forks": 38952,
      "open_issues": 513,
      "watchers": 97101,
      "default_branch": "master",
      "score": 1.0
    }
 ```

<blockquote>Q9: What are we seeing in the browser or in this sample JSON? Some of the specific fields? What do we think this might look like when we bring it into Python?</blockquote>

## Making an API call in Python

118. First we use the `requests` module to send HTTP requests (i.e. request data via the world wide web) using Python.
- [Requests: HTTP for Humans documentation](https://requests.readthedocs.io/en/master/)
- [Python documentation on `requests` module](https://pypi.org/project/requests/)
- [Python Requests Module, W3 Schools](https://www.w3schools.com/python/module_requests.asp)

119. The HTTP request returns a response object that includes whatever data is returned as part of the API call.

120. The `requests` module includes a range of methods that let us interact with elements of the API.

Method | Description
--- | ---
`delete(url, args)` | Sends as DELETE request to the specified URL
`get(url, params, args)` | Sends a GET request to the specified URL
`head(url, args)` | Sends a HEAD request to the specified URL
`patch(url, data, args)` | Sends a PATCH request to the specified URL
`post(url, data, json, args)` | Sends a POST request to the specified URL
`put(url, data, args)` | Sends a PUT request to the specified URL
`request(method, url, args)` | Sends a request of the specified method to the specified URL

121. A very basic example of the `requests` module in action.
```Python
# import requests module
import requests

# store URL
x = requests.get('url')

# print URL  text
print(x.text)
```

122. This basic syntax might look familiar for those who took Elements of Computing I in the Fall 2020 semester.
```Python
import urllib
import urllib.request

url = 'https://en.wikisource.org/wiki/John_F._Kennedy%27s_Third_State_of_the_Union_Address'

response = urllib.request.urlopen(url)
webContent = response.read()

f = open('Kennedy_Third_SOTU.html', 'wb')
f.write(webContent)
f.close
```

123. Let's look at how we would call the GitHub API in Python.
```Python
# import requests module
import requests

# store API url
url = 'https://api.github.com/search/repositories?q=language:python&sort=stars'

# assign the headers
headers = {'Accept': 'application/vnd.github.v3+json'}

# assign the requests method
r = requests.get(url, headers=headers)

# print a status update for the requests command
print(f"Status code: {r.status_code}")

# store API response to variable
response_dict = r.json()

# process results
print(response_dict.keys())
```

124. The first `print()` statement returns a status message for the `requests.get()` API call.

125. Once we know the API call is working, we can go ahead and request the JSON data available via the API.

126. Then we can store that JSON data as a Python dictionary.

<blockquote>Q10: Describe how a web API works in your own words.</blockquote>

## Working With the API Response in Python

127. If our API call has been successful, we now have JSON or XML data in Python.

128. Now we can start to explore the data returned by the API in Python.

129. We can call this type of preliminary exploration and analysis EDA, or exploratory data analysis.</blockquote>

130. Let's say we wanted to know more about these Python repositories.
```Python
# import requests module
import requests

# store API url
url = 'https://api.github.com/search/repositories?q=language:python&sort=stars'

# assign the headers
headers = {'Accept': 'application/vnd.github.v3+json'}

# assign the requests method
r = requests.get(url, headers=headers)

# print a status update for the requests command
print(f"Status code: {r.status_code}")

# store API response to variable
response_dict = r.json()

# print the total number of repositories
print(f"Total repositories: {response_dict['total_count']}")

# store list of dictionaries with information about GitHub repositories
repo_dicts = response_dict['items']

# print length of repo_dicts
print(f"Repositories returned: {len(repo_dicts)}")

# select first repository using index
repo_dict = repo_dicts[0]

# print number of keys in individual repository dictionary
print(f"\nKeys: {len(repo_dict)}")

# print all keys in the dictionary using a for loop to iterate over keys in the dictionary
for key in sorted(repo_dict.keys()):
  print(key)
```

131. Now that we know what keys are in this dictionary, we can pull out the values for some of these keys.
```Python
# import requests module
import requests

# store API url
url = 'https://api.github.com/search/repositories?q=language:python&sort=stars'

# assign the headers
headers = {'Accept': 'application/vnd.github.v3+json'}

# assign the requests method
r = requests.get(url, headers=headers)

# print a status update for the requests command
print(f"Status code: {r.status_code}")

# store API response to variable
response_dict = r.json()

# print the total number of repositories
print(f"Total repositories: {response_dict['total_count']}")

# store list of dictionaries with information about GitHub repositories
repo_dicts = response_dict['items']

# print length of repo_dicts
print(f"Repositories returned: {len(repo_dicts)}")

# select first dictionary for first repository using index
repo_dict = repo_dicts[0]

# print header information before key values return
print("\nSelected information about first repository:")

# print repo name
print(f"Name: {repo_dict['name']}")

# print repository owner information
print(f"Owner: {repo_dict['owner']['login']}")

# print repository number of stars
print(f"Stars: {repo_dict['stargazers_count']}")

# print project URL
print(f"Repository URL: {repo_dict['html_url']}")

# print repository creation date
print(f"Created: {repo_dict['created_at']}")

# print repository last update time
print(f"Updated: {repo_dict['updated_at']}")

# print repository description
print(f"Description: {repo_dict['description']}")
```

132. Visit [GitHub's REST API documentation](https://docs.github.com/en/free-pro-team@latest/rest) to learn more about its API.

## From API to JSON file

133. In many situations, we would stay within a programming environment when working with the data returned by an API call.

134. But let's say you wanted to write the data returned by an API call to a JSON or XML file.

135. We can write the JSON data loaded as a Python dictionary to a JSON file using `json.dump()`.
```Python
# import json module
import json

# import request module
import request

# store API url
url = 'https://api.github.com/search/repositories?q=language:python&sort=stars'

# assign the headers
headers = {'Accept': 'application/vnd.github.v3+json'}

# assign the requests method
r = requests.get(url, headers=headers)

# print a status update for the requests command
print(f"Status code: {r.status_code}")

# store API response to variable
response_dict = r.json()

# print the total number of repositories
print(f"Total repositories: {response_dict['total_count']}")

# store list of dictionaries with information about GitHub repositories
repo_dicts = response_dict['items']

# print length of repo_dicts
print(f"Repositories returned: {len(repo_dicts)}")

# select first dictionary for first repository using index
repo_dict = repo_dicts[0]

# create new JSON file and write repo_dict object to file
with open('output.json', 'w') as json_file:
  json.dump(repo_dict, json_file)
```

## Example: U.S. Census Bureau Data

136. Let's say we want to work with the U.S. Census Bureau's API.

137. First step is to navigate to the Census Bureau's ["About"](https://www.census.gov/data/developers/about.html) page for developers and click the "Request a Key" icon.

138. Once you've completed the "Request a Key" form, you should receive an API key via email. This will look like a long string of letters and numbers.

139. Next step is to identify which Census Bureau dataset you want to work with.

140. Lots of options, ranging from the facets of data from the American Community Survey to data from the Decennial Census.

141. Explore the list of options (["Available APIs"](https://www.census.gov/data/developers/data-sets.html)) and decide on a specific dataset.

142. For the purposes of this example, I'm going to work with [five-year data from the American Community survey](https://www.census.gov/data/developers/data-sets/acs-5year.html) to find a recent population count for all US states.

143. First thing I want to do is explore the documentation available for this dataset so I know what might (or should) return from the API call.
- [Link to documentation for 2019 subset of this dataset](https://www.census.gov/data/developers/data-sets/acs-5year.html)

144. As you can see from the documentation, there are MANY variables and data points contained in this dataset. 

145. For this example, I'm going to stick to the original question of wanting a recent population count for all states.

146. From looking at the documentation, I know my API call will start with `https://api.census.gov/data/2017/acs/acs5?key=[YOUR_API_KEY]`

147. And from looking at the full list of variables, I know my variable name for "Total Population is `B01003_001E`.

148. So my API call for the "Total Population" variable will look like `https://api.census.gov/data/2017/acs/acs5?key=[YOUR_API_KEY]&get=B01003_001E`.

149. This API call will return total population for all geographies in the ACS dataset.

150. I can modify the API call to only return "Total Population" for the zip code I am interested in.

151. The modified API call will look like `https://api.census.gov/data/2017/acs/acs5?key=[YOUR_API_KEY]&get=B01003_001E&for=state:*`.

152. You can paste this URL into your browser to check to make sure the API call is using the correct URL.

153. Check out the [Census Bureau's API documentation and sample queries](https://www.census.gov/data/developers/guidance/api-user-guide/query-examples.html) to learn more about how to customize your API call.

154. Now to bring this into Python.
```Python
# import requests module
import requests

# import json module
import json

# set census API key
apiKey = "YOUR_API_KEY"

# construct API
calledAPI = "https://api.census.gov/data/2017/acs/acs5?key=[YOUR_API_KEY]&get=B01003_001E&for=state:*`.

# call the API and collect the response
response = requests.get(calledAPI)

# load response into JSON object, removing first element which is field labels
formattedResponse = json.loads(response.text)[1:]

# write that JSON object to a file
with open('output.json', 'w') as json_file:
  json.dump(formattedResponse, json_file)
```

<blockquote>Q11: Describe your experience working with the Census Bureau API. What was rewarding? What was challenging? How did you solve those challenges?</blockquote>

<blockquote>OPTIONAL: Modify the API call to access another subset of data. Include code + comments.</blockquote>

## API Project Prompt

Navigate to an open data portal and construct an API call.

A few sources that might get you started:
- [GitHub repository with extensive inventory of free public APIs](https://github.com/public-apis/public-apis)
- [U.S. National Archives and Records Administration, NARA](https://www.archives.gov/developer#toc--datasets)
- [Smithsonian Institution](https://www.si.edu/openaccess/devtools)
- [Library of Congress](https://labs.loc.gov/lc-for-robots/)
- [U.S. Census Bureau](https://www.census.gov/data/developers/data-sets.html)
- [The Sports DB](https://www.thesportsdb.com/api.php)

View the API source in a browser. What are you seeing? How can we start to make sense of this data using available documentation?

Construct an API call in Python.

Interact with the data in Python to identify/pull out relevant key-value pairs

Take a subset of the data and write to a JSON file.

Include code + comments.

# Lab Notebook Questions

Q1: Open the <code>example.xlsx</code> file in a text editor. Describe what you see.

Q2: How does your answer to Q1 compare to what you see when you open the <code>example.csv</code> file in a text editor?

Q3: Open the <code>example.xlsx</code> file in a spreadsheet program. Save the file as a <code>.csv</code> format. What happens? Or what happens when you open the newly-created <code>.csv</code> file in a spreadsheet program or text editor?

Q4: Modify the code provided above to load the example.txt file.

Q5: Define escape characters in your own words. Describe a situation in which escape characters would be needed, and how you would address that challenge using Python syntax.

Q6: Describe in your own words how csv_DictReader interacts with structured data.

Q7: Create a small dictionary and write it to a CSV file. Include code + comments.

Q8: Decipher what we're seeing in the JSON here. What are the name/value pairs, and how are they organized in this object?

Q9: What are we seeing in the browser or in this sample JSON? Some of the specific fields? What do we think this might look like when we bring it into Python?

Q10: Describe how a web API works in your own words.

Q11: Describe your experience working with the Census Bureau API. What was rewarding? What was challenging? How did you solve those challenges?

OPTIONAL: Modify the API call to access another subset of data. Include code + comments.
