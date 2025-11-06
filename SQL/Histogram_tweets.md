## Question 
https://datalemur.com/questions/sql-histogram-tweets


## Approach
1. First obtain the number and user tweets each user did in 2022

```sql
select user_id, count(tweet_id) as tweet_count from tweets where year(tweet_date)='2022' group by user_id 
```

Now we will get a table as 
user_id | tweet_count
1       |   2
2       |   3

2. Now we need to group the users who have 1 tweet, 2 tweet ...

```sql
select tweet_count as tweet_bucket, count(user_id) from (
    select user_id, count(tweet_id) as tweet_count from tweets where year(tweet_date)='2022' group by user_id 
) as total_tweets group by tweet_count
```