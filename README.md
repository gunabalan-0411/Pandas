# Pandas

### Group By Function

* Use apply for custom group by calculation for better code readability
* Return pd.Series
* you can also use filtered data inside it
* before returning the result handle the edge cases like empty df or get back the groupby column name

```python
    # Calculating: Cancellation Rate
    result = filtered_trips.groupby('request_at').apply(
        lambda group: pd.Series(
            {
                "Cancellation Rate": round(
                    (group['status'] != 'completed').sum()/ len(group), 2
                )
            }
        )
    )
    if result.empty:
        return pd.DataFrame(columns=['Day', 'Cancellation Rate'])
    result.index.name = None
    return result.reset_index().rename(columns= {'index': 'Day'})
```

### Group By Range Condition

```python
df['age_group'] = pd.cut(
    df['age'],
    bins=[0, 18, 30, 50, 100],
    labels=['Teen', 'Young Adult', 'Adult', 'Senior']
)
```
