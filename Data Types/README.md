# Data Types

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
  df["marriage_status"] = df["marriage_status"].astype('category')
  ```
## Nominal
- string without priority. 
- e.g: eye color: Green, Red, Blue

## 
- marriage status
