# Medium Level


### Activity Rank
> Find the email activity rank for each user. Email activity rank is defined by the total number of emails sent. The user with the highest number of emails sent will have a rank of 1, and so on. Output the user, total emails, and their activity rank. Order records by the total emails in descending order. Sort users with the same number of emails in alphabetical order.
In your rankings, return a unique value (i.e., a unique rank) even if multiple users have the same number of emails. For tie breaker use alphabetical order of the user usernames.

[Problem](https://platform.stratascratch.com/coding/10351-activity-rank?code_type=2)

```python
# Import your libraries
import pandas as pd

#Gather set of all users
all_users = set(google_gmail_emails['from_user'])

#Create a dictionary to count the occurrences of each user
d = {}
for user in all_users:
    d[user] = [1 if x == user else 0 for x in google_gmail_emails['from_user']]
    d[user] = sum(d[user])

#Sort the dictionary by Count (high to low) then by user ID
info = dict(sorted(d.items(), key=lambda items : (-items[1], items[0])))

#Assign a rank score based on sorted dictionary
rank = 1
for k,v in info.items():
    info[k] = [v]
    info[k].append(rank)
    rank+=1

#Create Column Values for Output
google_gmail_emails['total_emails'] = google_gmail_emails['from_user'].apply(lambda x: info[x][0])
google_gmail_emails['rank'] = google_gmail_emails['from_user'].apply(lambda x: info[x][1])

#Return final subDF
google_gmail_emails[['from_user', 'total_emails', 'rank']].drop_duplicates().sort_values(by='rank')    
```




