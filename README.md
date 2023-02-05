# Data_Preprocessing
 ![render](https://user-images.githubusercontent.com/99830416/216795669-08509910-1347-478a-afe5-a408a2a84746.gif)


<b> It's commonly said that data scientists spend 80% of their time preprocess, cleaning and manipulating data and only 20% of their time analyzing it.The time spent cleaning is vital since analyzing dirty data can lead you to draw inaccurate conclusions.
Data cleaning is an essential task in data science. Without properly preprocessed, cleaned data, the results of any data analysis or machine learning model could be inaccurate. In this repo, you will learn how to identify, diagnose, and treat a variety of data preprocessing & data cleaning problems in Python, ranging from simple to advanced. You will deal with improper data types, check that your data is in the correct range, handle missing data, perform record linkage, and more!</b>

# Data Cleaning 
Data cleaning means fixing bad data in your data set.<br>
Bad data could be: 
- Empty cells
- Wrong format
- Wrong data
- Duplicates
- Outlires

## 1- Empty Cells

- Empty Cell can potentially give you a wrong result when you analyze data.
- Ways to deal with empty cells:

   ❱ Remove rows that contain empty cells.<br> 
   ❱ Replace all empty cells with values <br> 

### ❱ Remove rows that contain empty cells
  ```py
  # not affect the original dataframe
  newdf = df.dropna()

  # affect the original dataframe
  df.dropna(inplcae=True)
  ```
### ❱ Replace empty cells with values
```py
# fill all empty cells in dataframe with value 130 (in the original dataframe)
df.fillna(130, inplace=True)

# fill all empty cells in specific column with value 130 (in the original dataframe)
df["Quantity"].fillna(130, inplace=True)

# Replacing using mean, median, mode
column_mean = df['Quantity'].mean() # make sure that Quantity is column is int data type
df["Quantity"].fillna(column_mean, inplace=True)
```

## 2- Wrong fromat
- Cells with data of wrong format can make it difficult, or even impossible, to analyze data. For example this record "20201226" in date column is wrong format data 
  that should be 2020-12-26
- Wayes to fix wrong format data:
    
   ❱ convert all cells in the columns into the same format   
   ❱ remove the rows that has wrong format   
   
### ❱ convert all cells in the columns into the same format
```py
import pandas as pd
df = pd.read_csv('data.csv')
df['Date'] = pd.to_datetime(df['Date'])
print(df.to_string())
```
### ❱ Replace empty cells with values

- The result from the converting the column to datatime  gave us a NaT value, which can be handled as a NULL value, and we can remove the row by using the dropna()       method.

```py
df.dropna(subset=['Date'], inplace = True)
```

## 3- Wrong data
- "Wrong data" does not have to be "empty cells" or "wrong format", it can just be wrong,
-  like if someone registered "199" instead of "1.99".
-  If you have a data set for courses in the college. You have class duration is 2 or 3 hours. While you check the data set you find out that there is a classes have      duration 30 hours! 
- Sometimes you can spot wrong data by looking at the data set, because you have an expectation of what it should be.
- Wayes to fix wrong format data:

   ❱ Replacing Values<br> 
   ❱ Removing Rows

### ❱ Replacing Values
- One way to fix wrong values is to replace them with something suitable else.
- Set "Duration" = 45 in row 7:
 
   ```py
   df.loc[7, 'Duration'] = 45
   ```
   
- For small data sets you might be able to replace the wrong data one by one, but not for big data sets. To replace wrong data for larger data sets you can create some   rules, e.g. set some boundaries for legal values, and replace any values that are outside of the boundaries.

   ```py
   # set all values that are greater than 120 to 120 in Duration column
   df.loc[df['Duration'] > 120,'Duration'] = 120 
   ```
   
   ```py
   # the same function using loop 
   for x in df.index:
       if df.loc[x, "Duration"] > 120:
            df.loc[x, "Duration"] = 120
   ```
   
### ❱ Remove rows
   
- Another way of handling wrong data is to remove the rows that contains wrong data.
- This way you do not have to find out what to replace them with, and there is a good chance you do not need them to do your analyses.

   ```py
   for x in df.index:
     if df.loc[x, "Duration"] > 120:
       df.drop(x, inplace = True)
   ```
   
## 4- Duplicates
- Discovering Duplicates
  
  ```py
  print(df.duplicated()) # Returns True for every row that is a duplicate, othwerwise False
  ```
 
 - Removing Duplicates
 
   ```py
   df.drop_duplicates(inplace = True)
   ```

# Checking for the correction columns data types  

# Data scaling
