# Data_Preprocessing

> <b> It's commonly said that data scientists spend 80% of their time preprocessing, cleaning and manipulating data and only 20% of their time analyzing it.The time spent   cleaning is vital since analyzing dirty data can lead you to draw inaccurate conclusions.
> Data cleaning is an essential task in data science. Without properly preprocessed, cleaned data, the results of any data analysis or machine learning model could be  inaccurate. In this repo, you will learn how to identify, diagnose, and treat a variety of data preprocessing & data cleaning problems in Python, ranging from simple to advanced. You will deal with improper data types, check that your data is in the correct range, handle missing data, perform record linkage, and more!</b>

## Pre_processing performed through those steps :
> ### 1. [Split data into dependent and independent variables](#1-split-data-into-dependent-and-independent-variables-1 )
> ### 2. [Columns Processing](#2-columns-processing-1 )
> ### 3. [Data Cleaning](#3-data-cleaning-1)
> ### 4. [Data Normalization](#data-normalization)
> ### 5. [Encoding categorical data]()


![separator2](https://i.imgur.com/4gX5WFr.png)
# 1. Split Data Into Dependent And Independent Variables
> ![OIP](https://user-images.githubusercontent.com/99830416/216852188-72679712-6709-4317-ae6f-ddba9fb33160.jpg)
> #### The hight of the plant depends on the amount of water & amount of fertilizer so :
> - dependent variable **(does not depend on column which all values are unique)** : the hight of the plant
> - independent varibales **(Responsible for determining the dependent variable)** : amount of water, amount of fertilizer

> ![image](https://user-images.githubusercontent.com/99830416/216852482-4f1bb67b-4c06-4bf4-9156-8e8d493e92b3.png)
> - dependent variable : Purshased_Any_Item
> - independent variables : State, Profission, age, monthly_income
> - Name does not determine the dependent variable (as all values in this column are unique). So it is not an independent variables. **So it should be removed** 
  
> ```py
> independent = df[ ['State', 'Profession', 'Age', 'Monthly_income'] ]
> dependent = df[ ['Purshased_Any_Item'] ] 
> ```
> ```py
> # another way to split data
> X = df.drop(columns=['Name','Purshased_Any_Item'])
> Y = df['Purshased_Any_Item']
> ```

![separator2](https://i.imgur.com/4gX5WFr.png)
# 2. Columns Processing

- ## Drop unwanted columns :
>   - #### Columns that does not affect the prediction (get them from the first step). <br>
>        ```py
>        newdf = df.drop(columns=['Name'])
>        # or df.drop(columns=['Name'], inplace=True)
>        ```

- ## Analysis Columns
>   ```py
>   # display number of rows and columns of the data set
>   df.shape
>   
>   # display number of non null values for each column. 
>   df.info()
>   # from this step i can determine if the column has a lot of nulls or not comparing with number of original rows
>   
>   # print count of nulls for each column and percentage of them
>   missing_data = pd.DataFrame({'total_missing': df.isnull().sum(), 'perc_missing': (df.isnull().mean())*100})
>   missing_data
>   
>   # Statistical description of numerical variables
>   df.describe()
>   ```

- ## Deal with columns after this info
>  - #### If column has very large average of missing data Drop it.
>  - #### If the average of missing data is small then fill the empty cells
>  - #### Check this [Notebook]()

- ## Validate columns data types
> - #### What are [Data Types](https://github.com/Abdelrhman-Sayed70/Data_Preprocessing/tree/main/Data%20Types)? 
> - #### Check those [Notebooks](https://github.com/Abdelrhman-Sayed70/Data_Preprocessing/tree/main/Columns%20Data%20Types) 

![separator2](https://i.imgur.com/4gX5WFr.png)
# 3. Data Cleaning 
 Data cleaning means fixing bad data in your data set.<br>
 Bad data could be: 

   - #### a. Null values
   - #### b. Wrong format
   - #### c. Wrong data
   - #### d. Duplicates
   - #### e. Handling unwanted features

## *a- Null values*
>
> - If you want to assign some missing values as null ? assume that some cells have '?', 'UNDEFINED' i want to make them read as Null values
>    ```py
>    df = pd.read_csv('data.csv', na_values=['?','UNDEFINED'])
>    ```
> - Deal with empty cells:
>
>   ❱ Calculate total number of rows that has missing values then calc its mean.<br>
>   ❱ If the average of missing rows is very small so we can **Drop those rows** else we can **Fill the empty cells with value**<br>
>   ❱ Remove rows that contain empty cells.<br> 
>   ❱ Replace all empty cells with values <br> 
> ### 
> ### ❱ Drop rows that contain empty cells
>  ```py
>  # not affect the original dataframe
>  newdf = df.dropna()
>
>  # affect the original dataframe
>  df.dropna(inplcae=True)
>  ```
> ### ❱ Fill empty cells with values
> ```py
> # fill all empty cells in dataframe with value 130 (in the original dataframe)
> df.fillna(130, inplace=True)
>
> # fill all empty cells in specific column with value 130 (in the original dataframe)
> df["Quantity"].fillna(130, inplace=True)
>
> # Replacing using mean, median, mode
> column_mean = df['Quantity'].mean() # make sure that Quantity is column is int data type
> df["Quantity"].fillna(column_mean, inplace=True)
> ```
> ### ❱ Check this [Notebook]()

## *b- Wrong fromat*
> - Cells with data of wrong format can make it difficult, or even impossible, to analyze data. For example this record "20201226" in date column is wrong format data 
>   that should be 2020-12-26
> - Wayes to fix wrong format data :
>
>     ❱ convert all cells in the columns into the same format<br> 
>     ❱ remove the rows that has wrong format 
>     
> ### ❱ convert all cells in the columns into the same format
> ```py
> import pandas as pd
> df = pd.read_csv('data.csv')
> df['Date'] = pd.to_datetime(df['Date'])
> print(df.to_string())
> ```
> ### ❱ Replace empty cells with values
>
> - The result from the converting the column to datatime  gave us a NaT value, which can be handled as a NULL value, and we can remove the row by using the dropna()       method.
>
> ```py
> df.dropna(subset=['Date'], inplace = True)
> ```

## *c- Wrong data*
> -  Wrong data does not have to be empty cells or wrong format, it can just be wrong,
>
> -  like if someone registered "199" instead of "1.99".
>
> -  If you have a data set for courses in the college. You have class duration is 2 or 3 hours. While you check the data set you find out that there is a classes have      duration 30 hours! 
>
> - Sometimes you can spot wrong data by looking at the data set, because you have an expectation of what it should be.
>
> - Wayes to fix wrong format data: <br>
>     ❱ Replacing Values<br> 
>     ❱ Removing Rows
>
> ### ❱ Replacing Values
> - One way to fix wrong values is to replace them with something suitable else.
> - Set "Duration" = 45 in row 7:
>  
>   ```py
>   df.loc[7, 'Duration'] = 45
>   ```
>   
> - For small data sets you might be able to replace the wrong data one by one, but not for big data sets. To replace wrong data for larger data sets you can create       some   rules, e.g. set some boundaries for legal values, and replace any values that are outside of the boundaries.
>
>   ```py
>   # set all values that are greater than 120 to 120 in Duration column
>   df.loc[df['Duration'] > 120,'Duration'] = 120 
>   ```
>   
>   ```py
>   # the same function using loop 
>   for x in df.index:
>       if df.loc[x, "Duration"] > 120:
>            df.loc[x, "Duration"] = 120
>   ```
>   
>### ❱ Remove rows
>   
>- Another way of handling wrong data is to remove the rows that contains wrong data.
>- This way you do not have to find out what to replace them with, and there is a good chance you do not need them to do your analyses.
>
>   ```py
>   for x in df.index:
>     if df.loc[x, "Duration"] > 120:
>       df.drop(x, inplace = True)
>   ```
   
## *d- Duplicates*
> - Discovering Duplicates
>  
>   ```py
>   print(df.duplicated()) # Returns True for every row that is a duplicate, othwerwise False
>   ```
> 
> - Removing Duplicates
> 
>   ```py
>   df.drop_duplicates(inplace = True)
>   ```
   
## *e. Handling unwanted features*
> - Words that starts with the symbol '@', e.g., @AnnaMedaris, are removed.
> - Hashtag symbols are removed, e.g., #depression is converted to depression.
>  
>     ```py
>     df['name'] = df['name'].str.strip('@')
>     df['titles'] = df['titles'].str.strip('#')
>     # this function make the data type of column string
>     ```
>
> - Delete any URL

![separator2](https://i.imgur.com/4gX5WFr.png)

# 4. Deal With Categorical Data 
- ### What are [Data Types](https://github.com/Abdelrhman-Sayed70/Data_Preprocessing/tree/main/Data%20Types)?
- ### Check this [Notebook](https://github.com/Abdelrhman-Sayed70/Data_Preprocessing/tree/main/Categorical%20Data)

![separator2](https://i.imgur.com/4gX5WFr.png)
# 5. Feature Scaling [Normalizatio]
- ### Will be available soon  

![separator2](https://i.imgur.com/4gX5WFr.png)
# 6. Additional features
- ### Every word is converted to lowercase

![separator2](https://i.imgur.com/4gX5WFr.png)
