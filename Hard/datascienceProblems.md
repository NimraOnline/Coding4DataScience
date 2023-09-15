# Hard Level


### Algorithm Performance
> Meta/Facebook is developing a search algorithm that will allow users to search through their post history. You have been assigned to evaluate the performance of this algorithm.

> We have a table with the user's search term, search result positions, and whether or not the user clicked on the search result.

> Write a query that assigns ratings to the searches in the following way:
>> If the search was not clicked for any term, assign the search with rating=1
>> 
>> If the search was clicked but the top position of clicked terms was outside the top 3 positions, assign the search a rating=2
>> 
>> If the search was clicked and the top position of a clicked term was in the top 3 positions, assign the search a rating=3

> As a search ID can contain more than one search term, select the highest rating for that search ID. Output the search ID and its highest rating.

[Problem](https://platform.stratascratch.com/coding/10350-algorithm-performance?code_type=2)

```python
# Import your libraries
import pandas as pd

# Start writing code
fb_search_events.head()

#New column where:
#if clicked = 0, Rating=1
#if clicked = 1, Rating=2 or 3
fb_search_events['rating'] = fb_search_events['clicked'].apply(lambda x: 1 if x==0 else 2)

#if clicked = 1 AND search_results_position <= 3, Rating=3
fb_search_events['3rating'] = fb_search_events['rating']
fb_search_events['3rating'] = fb_search_events.apply(lambda x: 3 if (x['search_results_position']<=3 and x['rating']==2) else 0, axis=1)

#Replace all ratings if 3
fb_search_events['rating'] = fb_search_events.apply(lambda x: x['rating'] if x['3rating']==0 else x['3rating'], axis=1)

#Over all matching search_id, find max(Rating)
grouped = fb_search_events.groupby('search_id')['rating'].max()

#Output: search_id | max(Rating)
dic = {'search_id':grouped.index, 'rating':grouped.values}
output = pd.DataFrame(dic)

output.head()  
```




