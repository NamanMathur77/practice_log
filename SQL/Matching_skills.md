## Question
https://datalemur.com/questions/matching-skills

## Aproach
1. First obtain the candidates with skills that match
```sql
SELECT * FROM candidates where skill in ('Python', 'Tableau', 'PostgreSQL');
```

2. count the skills as all the data is unique so count should be 3 for our result
```sql
select candidate_id FROM candidates where skill in ('Python', 'Tableau', 'PostgreSQL') group by candidate_id
```

3. Use having clause to filter candidates with 3 skills
```sql
select candidate_id FROM candidates where skill in ('Python', 'Tableau', 'PostgreSQL') group by candidate_id having count(skill)=3 order by candidate_id;
```