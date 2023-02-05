# Data Types
> - Manipulating and analyzing data with incorrect data types could lead to compromised analysis as you go along the data science workflow.
>   When working with new data, you should always check the data types of your columns using the .dtypes attribute or the .info() method. Often times, you'll run into     columns that should be converted to different data types before starting any analysis.
>  
>     ```py
>       # Print the information of df
>       print(df.info())
> 
>       # Print summary statistics of user_type column
>       print(df['user_type'].describe())
>     
>       # Get the data type of column 
>       print(df['user_type'].dtype)
>
>     ```
![separator2](https://i.imgur.com/4gX5WFr.png)

# Quantitve Data & Qualitive Data
  ![image](https://user-images.githubusercontent.com/99830416/216848775-ac6126e1-e0e5-45b0-9e7a-d1f1250bdd34.png)

## Quantitve Data
> ### 1. Discrete
>  - Finite int values.
>  - ❱ No.Goals ❱ No.childrens ❱ No.rooms    
> ### 2. Continues
>  - Infinite values. in ranges
>  - ❱ Hight ❱ Temp

> ```py
> # remove $ sign then convert to int
> sales['Revenue'] = sales['Revenue'].str.strip('$') 
> sales['Revenue'] = sales['Revenue'].astype('int')
> ```

## Qualitive Data (Categorical)
> ### 1. Ordinal
>  - Orderd in a meaningful way.
>  - we can assign values (in order) to each element
>  - ❱ Classes (Low, Medium, High)
>  - ❱ Grades  (Ex, V.good, Good)
>     
> ### 2. Nominal
>  - Order is not important
>  - We cannot assign values in order to each element
>  - ❱ Eye color (Green, Red, Blue)
>  - ❱ Marital statues (Single, Devorced, Married)  
  
>    ```py
>    # Print new summary statistics 
>    print(df['user_type_cat'].describe())
>
>    # Convert user_type from integer to category
>    df["marriage_status"] = df["marriage_status"].astype('category')
>
>    # Write an assert statement confirming the change
>    assert df['user_type_cat'].dtype == 'category'
>
>    # Print new summary statistics 
>    print(df['user_type_cat'].describe())
>    ```

![separator2](https://i.imgur.com/4gX5WFr.png)  
  

 
