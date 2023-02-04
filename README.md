# Data_Cleaning
![R](https://user-images.githubusercontent.com/99830416/216778235-0f435edf-d3ba-4881-af42-4f425c03a2c2.gif)

<b> It's commonly said that data scientists spend 80% of their time cleaning and manipulating data and only 20% of their time analyzing it.The time spent cleaning is vital since analyzing dirty data can lead you to draw inaccurate conclusions.
Data cleaning is an essential task in data science. Without properly cleaned data, the results of any data analysis or machine learning model could be inaccurate. In this repo, you will learn how to identify, diagnose, and treat a variety of data cleaning problems in Python, ranging from simple to advanced. You will deal with improper data types, check that your data is in the correct range, handle missing data, perform record linkage, and more!</b>

# Bad data
Data cleaning means fixing bad data in your data set.

Bad data could be:
- Empty cells
- Wrong format
- Wrong data
- Duplicates
- Outlires

# Empty Cells

- Empty Cell can potentially give you a wrong result when you analyze data.
- Ways to deal with empty cells:

   ❱ Remove rows that contain empty cells.<br> 
   ❱ Replace empty values <br> 

### ❱ Remove rows that contain empty cells
  ```py
  # not affect the original dataframe
  newdf = df.dropna()

  # affect the original dataframe
  df.dropna(inplcae=True)
  ```
### ❱ Replace empty values
```py
# fill all empty cells in dataframe with value 130 (in the original dataframe)
df.fillna(130, inplace=True)

# fill all empty cells in specific column with value 130 (in the original dataframe)
df["Quantity"].fillna(130, inplace=True)

# Replacing using mean, median, mode
column_mean = df['Quantity'].mean() # make sure that Quantity is column is int data type
df["Quantity"].fillna(column_mean, inplace=True)
```

# Wrong fromat
 
