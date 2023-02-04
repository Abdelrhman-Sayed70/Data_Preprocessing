# Data Types
- Manipulating and analyzing data with incorrect data types could lead to compromised analysis as you go along the data science workflow.
  When working with new data, you should always check the data types of your columns using the .dtypes attribute or the .info() method. Often times, you'll run into     columns that should be converted to different data types before starting any analysis.
-  Code
 
    ```py
      # Print the information of df
      print(df.info())

      # Print summary statistics of user_type column
      print(df['user_type'].describe())
    
      # Get the data type of column 
      print(df['user_type'].dtype)
      
      # Write an assert statement confirming the change
      assert df['user_type_cat'].dtype == 'category'
    ```


## Continues (Nmerical) 
- numbers
- In Python takes int, float data types

  ```py
  # remove $ sign then convert to int
  sales['Revenue'] = sales['Revenue'].str.strip('$') 
  sales['Revenue'] = sales['Revenue'].astype('int')
  ```

## Categorical (Ordinal)
- String with priority.
- Orderd in a meaningful way.
- Ordinal data is classified into categories within a variable that have a natural rank order. However, the distances between the categories are uneven or unknown.
- e.g
  ![Screenshot 2023-02-04 185000](https://user-images.githubusercontent.com/99830416/216779498-62e16c79-af89-475e-a9b3-9d0ac6e0c655.png)
- you can assign number for each value ascendingly
- In Python takes category data type

    ```py
    # Print new summary statistics 
    print(df['user_type_cat'].describe())
    
    # Convert user_type from integer to category
    df["marriage_status"] = df["marriage_status"].astype('category')
    
    # Print new summary statistics 
    print(df['user_type_cat'].describe())
    ```
## Nominal
- string without priority. 
- e.g: eye color: Green, Red, Blue

## 
- marriage status
