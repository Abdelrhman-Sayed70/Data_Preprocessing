# Drop 

## Drop rows based on condition
```py
# Show recordes with avd_rating <= 5
movies = movies[movies['avg_rating'] <= 5]

# Drop values using .drop()
movies.drop(movies[movies['avg_rating'] > 5].index, inplace = True)

# Assert results
assert movies['avg_rating'].max() <= 5
```

